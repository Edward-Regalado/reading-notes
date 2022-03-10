# Spring Security Architecture

## Authentication and Access Control

- app security boils down to two independent problems: authentication (who are you?) and authorization (what are you allowed to do?).
- SS has an architecture that is designed to separarte authentication from authorization.

## Authentication

- the main strategy interface for authentication is `AuthenticationManager`, which only has one method.

```
public interface AuthenticationManager {

  Authentication authenticate(Authentication authentication)
    throws AuthenticationException;
}
```
- `AuthenticationManager` can do one of 3 things in its `authenticate()`:
  - return an `Authentication` (`authenticated=true`) if it can verify that the input represents a valid principle.
  - Throw an `AuthenticationException` if the input was invalid.
  - Return `null` if it cannot decide.

- `AuthenticationException` is a runtime exception and usually handled by an application in a generic way.
- The most commonly used implementation of `AuthenticationManager` is `ProvidedManager`, which delegates to a chain of `AuthenticationProvider` instanced.

### Customizing Authentication Managers

- SS provides some config helpers to quickly get common authentication manager features set up in your app.
- `AuthenticationManagerBuilder` is the most coommon and is great for setting up in-memory, JDBC, or LDAP user details or for adding a custom `UserDetailsService`.
- The following example shows an application that configs the global parent `Authenticationmanager`

```
@Configuration
public class ApplicationSecurity extends WebSecurityConfigurerAdapter {

   ... // web stuff here

  @Autowired
  public void initialize(AuthenticationManagerBuilder builder, DataSource dataSource) {
    builder.jdbcAuthentication().dataSource(dataSource).withUser("dave")
      .password("secret").roles("USER");
  }

}
```

### Authorization or Access Control

- when authenticaion is successful, we can move on to authorization, and the core strategy here is `AccessDecisionManager`
- There are 3 implementations provided by the framework and all 3 delegate to a chain of `AccessDecisionVoter` instnances, a bit like the `ProviderManager` deledates to `AuthenticaionProviders`
- An `AccessDecisionVoter` considers an `Authenticaion` and a secure `Object` which has been decorated with `ConfigAttributes`

```
boolean supports(ConfigAttribute attribute);

boolean supports(Class<?> clazz);

int vote(Authentication authentication, S object,
        Collection<ConfigAttribute> attributes);
```

- the `Object` represents anything that a user might want to access (a web resource or a method in a Java class are the two most common cases).
- `ConfigAttributes` are also fairly generic, representing a decoration of the secure `Object` with some metadata that determines the level of permission required to access it.
- `ConfigAttribute` is an interface- it has only one generic method, which returns a String, and these Strings encode in some way the intention of the owner of teh resource, expression ruless about who is allowed to access it.
-Typicall, `ConfigAttributes` is the name of a user role like `ROLE_ADMIN` or `ROLE_AUDIT`.


## Web Security

- SS in the web tier is based on Servlet `Filters`.
- Client -> Filter -> Filter -> Filter -> Servlet
- The client sends a request to the application and the container decides which filters and which servlet apply to it based on teh path of the request URL
- Filters form a chain, so they are ordered, and a filter can veto the rest of the chain if needed.
- filters can also modify the request or response used in the downstream filters and servlet.
- Filter order is very important- Spring Boot manages it through `@Beans` of type of `Filter` can have an `@Order` or implement `Ordered`, and they can be part of `FilterRegistrationBean`
- Spring Security is a single filter, but has additional filters, each playing a special role.
- The `FilterChainProxy` contains all the security logic arranged internally as a chain of filters.

## Creating and Customizing Filter Chains

- the default fallback filter chain in a SB app has a predefined order of `SecurityPRoperties.BASIC_AUTH_ORDER`
- can switch it off completely by setting `security.basic.enable=false`

```
@Configuration
@Order(SecurityProperties.BASIC_AUTH_ORDER - 10)
public class ApplicationConfigurerAdapter extends WebSecurityConfigurerAdapter {
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http.antMatcher("/match1/**")
     ...;
  }
}
```
## Request Matching for Dispatch and Authorization

- A security filter chain (or, equivalently, a `WebSecurityConfigurerAdapter` has a request matcher that is used to decide whether to apply it to an HTTP request.
- once a decision is made to apply a filter, no others are applied.
- one of the easiest mistakes to make is to forget taht these matches apply to different processes.

```
@Configuration
@Order(SecurityProperties.BASIC_AUTH_ORDER - 10)
public class ApplicationConfigurerAdapter extends WebSecurityConfigurerAdapter {
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http.antMatcher("/match1/**")
      .authorizeRequests()
        .antMatchers("/match1/user").hasRole("USER")
        .antMatchers("/match1/spam").hasRole("SPAM")
        .anyRequest().isAuthenticated();
  }
}
```
## Combining App Security Rules with Actuator Rules

- f you want your application security rules to apply to the actuator endpoints, you can add a filter chain that is ordered earlier than the actuator one and that has a request matcher that includes all actuator endpoints.

```
@Configuration
@Order(ManagementServerProperties.BASIC_AUTH_ORDER + 1)
public class ApplicationConfigurerAdapter extends WebSecurityConfigurerAdapter {
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http.antMatcher("/foo/**")
     ...;
  }
}
```
## Method Security

- Spring Security offers support for applying access rules to Java method executions. 
-  For users, it means the access rules are declared using the same format of `ConfigAttribute strings`

```
@SpringBootApplication
@EnableGlobalMethodSecurity(securedEnabled = true)
public class SampleSecureApplication {
}
Then we can decorate the method resources directly:

@Service
public class MyService {

  @Secured("ROLE_USER")
  public String secure() {
    return "Hello Security";
  }
}
```
## Working with Threads

- Spring Security is fundamentally thread-bound, because it needs to make the current authenticated principal available to a wide variety of downstream consumers. 
- The basic building block is the `SecurityContext`, which may contain an `Authentication` (and when a user is logged in it is an `Authentication` that is explicitly `authenticated`).

```
SecurityContext context = SecurityContextHolder.getContext();
Authentication authentication = context.getAuthentication();
assert(authentication.isAuthenticated);
```
- If you need access to the currently authenticated user in a web endpoint, you can use a method parameter in a @RequestMapping, as follows:

```
@RequestMapping("/foo")
public String foo(@AuthenticationPrincipal User user) {
  ... // do stuff with user
}
```

## Processing Secure Methods Asynchronously

- Since the `SecurityContext` is thread-bound, if you want to do any background processing that calls secure methods (for example, with `@Async`), you need to ensure that the context is propagated. This boils down to wrapping the `SecurityContext` with the task (`Runnable`, `Callable`) that is executed in the background.
- Spring Security provides some helpers to make this easier, such as wrappers for `Runnable` and `Callable`.
- To propagate the `SecurityContext` to `@Async` methods, you need to supply an `AsyncConfigurer` and ensure the `Executor` is of the correct type:

```
@Configuration
public class ApplicationConfiguration extends AsyncConfigurerSupport {

  @Override
  public Executor getAsyncExecutor() {
    return new DelegatingSecurityContextExecutorService(Executors.newFixedThreadPool(5));
  }

}
```


## Resources

[Spring](https://spring.io/guides/topicals/spring-security-architecture/)
[Spring Auth Cheat Sheet](https://github.com/codefellows/seattle-java-401d2/blob/master/SpringAuthCheatSheet.md)
