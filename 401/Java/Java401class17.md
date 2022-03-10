# Spring Boot and OAuth2

## Creating a New Project

- use `Spring Initializr`
- add a home page: create an `index.html` in the `src/main/resources/static` folder

`index.html`

```
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <title>Demo</title>
    <meta name="description" content=""/>
    <meta name="viewport" content="width=device-width"/>
    <base href="/"/>
    <link rel="stylesheet" type="text/css" href="/webjars/bootstrap/css/bootstrap.min.css"/>
    <script type="text/javascript" src="/webjars/jquery/jquery.min.js"></script>
    <script type="text/javascript" src="/webjars/bootstrap/js/bootstrap.min.js"></script>
</head>
<body>
	<h1>Demo</h1>
	<div class="container"></div>
</body>
</html>
```

### Securing the App with Github and Spring Securtiy

- add `Spring Security` as a dependency.
- include `Spring Security OAuth2.0` client starter
- By added this, you will secure the app with OAuth 2.0 by default

```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```

## Add a New Github App

- To use GitHub’s OAuth 2.0 authentication system for login, you must first Add a new [GitHub app](https://github.com/settings/developers).
- Select "New OAuth App" and then the "Register a new OAuth application" page is presented. 
- Enter an app name and description. Then, enter your app’s home page, which should be http://localhost:8080.
- Indicate the Authorization callback URL as http://localhost:8080/login/oauth2/code/github and click Register Application.
- The default redirect URI template is `{baseUrl}/login/oauth2/code/{registrationId}`. The registrationId is a unique identifier for the `ClientRegistration`.
- Configure `application.yml`, then make the link to Github, add teh following to your `applicaiton.yml`:

```
spring:
  security:
    oauth2:
      client:
        registration:
          github:
            clientId: github-client-id
            clientSecret: github-client-secret
```

### Boot Up the App

- Now instead of visiting the home page at `http://localhost:8080` you should be redirected to login with Github.
- If you stay logged into Github, you won't have to re-authenticate with this local app, even if you open it in a fresh browser with no cookies and no cached data.


## Add a Welcome page

- add the new Github link to the home page of your app.

```
<div class="container unauthenticated">
    With GitHub: <a href="/oauth2/authorization/github">click here</a>
</div>
<div class="container authenticated" style="display:none">
    Logged in as: <span id="user"></span>
</div>
```
- render content on the condition that the user is authenticaed, either server-side or client-side rendering.
- add the following JavaScript, which will hit that endpoint.

```
index.html
<script type="text/javascript">
    $.get("/user", function(data) {
        $("#user").html(data.name);
        $(".unauthenticated").hide()
        $(".authenticated").show()
    });
</script>

```

### The `/user` Endpoint

- add the server-side endpoint, call it `/user`.
- It will send back the currently logged-in user, which we can do quite easily in our main class:
- Note the use of `@RestController`, `@GetMapping`, and the `OAuth2User` injected into the handler method.

```
@SpringBootApplication
@RestController
public class SocialApplication {

    @GetMapping("/user")
    public Map<String, Object> user(@AuthenticationPrincipal OAuth2User principal) {
        return Collections.singletonMap("name", principal.getAttribute("name"));
    }

    public static void main(String[] args) {
        SpringApplication.run(SocialApplication.class, args);
    }

}
```
## Making the Home Page Public

- To make the link visible, we also need to switch off teh security on the home page by extending `WebSecurityConfigurereAdapter`

```
@SpringBootApplication
@RestController
public class SocialApplication extends WebSecurityConfigurerAdapter {

    // ...

    @Override
    protected void configure(HttpSecurity http) throws Exception {
    	// @formatter:off
        http
            .authorizeRequests(a -> a
                .antMatchers("/", "/error", "/webjars/**").permitAll()
                .anyRequest().authenticated()
            )
            .exceptionHandling(e -> e
                .authenticationEntryPoint(new HttpStatusEntryPoint(HttpStatus.UNAUTHORIZED))
            )
            .oauth2Login();
        // @formatter:on
    }

}
```

- Spring Boot attaches special meaning to a `WebSecurityConfigurerAdapter` on the class annotated with `@SpringBootApplication` and uses it to configure the security filter chain that carries the OAuth 2.0 authentication processor.
- The above configuration indicates a whitelist of permitted endpoints, with every other endpoint requiring authentication.
- `/` since that’s the page you just made dynamic, with some of its content visible to unauthenticated users

- `/error` since that’s a Spring Boot endpoint for displaying errors, and

- `/webjars/**` since you’ll want your JavaScript to run for all visitors, authenticated or not

## Add a Logout Button

- add a button to allow users to logout of the app.
- requires a bit of care to implement.
- transforming the app from a read-only resource to a read-write one (logging out requres a state change).

### Client Side Changes

-  On the client side, we just need to provide a logout button and some JS to call back to the server to ask for the authentication to be cancelled.

```
<div class="container authenticated">
  Logged in as: <span id="user"></span>
  <div>
    <button onClick="logout()" class="btn btn-primary">Logout</button>
  </div>
</div>

```
- then provide the `logout()` function that it referes to in the JS.
- The `logout()` function does a `POST` to `/logout` and then clears the dynamic content. 
- Now we can switch over to the server side to implement that endpoint.

```
var logout = function() {
    $.post("/logout", function() {
        $("#user").html('');
        $(".unauthenticated").show();
        $(".authenticated").hide();
    })
    return true;
}
```

- The `/logout` endpoint requires us to `POST` to it, and to protect the user from Cross Site Request Forgery (CSRF, pronounced "sea surf"), it requires a token to be included in the request.
- do the following in the `WebSecurityConfigurerAdapter`:

```
@Override
protected void configure(HttpSecurity http) throws Exception {
	// @formatter:off
    http
        // ... existing code here
        .csrf(c -> c
            .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
        )
        // ... existing code here
    // @formatter:on
}
```

### Adding the CSRF Token in the Client

- you’ll need to explicitly add the CSRF token, which you just made available as a cookie from the backend
- then you can reference it in your HTML:

```
pom.xml
<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>js-cookie</artifactId>
    <version>2.1.0</version>
</dependency>

index.html
<script type="text/javascript" src="/webjars/js-cookie/js.cookie.js"></script>
```
- finally, use the `Cookies` convenience methods in XHR:

```
$.ajaxSetup({
  beforeSend : function(xhr, settings) {
    if (settings.type == 'POST' || settings.type == 'PUT'
        || settings.type == 'DELETE') {
      if (!(/^http:.*/.test(settings.url) || /^https:.*/
        .test(settings.url))) {
        // Only send the token to relative URLs i.e. locally.
        xhr.setRequestHeader("X-XSRF-TOKEN",
          Cookies.get('XSRF-TOKEN'));
      }
    }
  }
});
```

### Login with Github

- work in progress... 

## Resources

[Spring](https://spring.io/guides/tutorials/spring-boot-oauth2/)