# Spring Data REST

## One-to-One Relationship

### The Data Model

- the two classes `Library` and `Address` have a one-to-one relationship, using teh `@OneToOne` annotation.

```
@Entity
public class Library {

    @Id
    @GeneratedValue
    private long id;

    @Column
    private String name;

    @OneToOne
    @JoinColumn(name = "address_id")
    @RestResource(path = "libraryAddress", rel="address")
    private Address address;
    
    // standard constructor, getters, setters
}
```

```
@Entity
public class Address {

    @Id
    @GeneratedValue
    private long id;

    @Column(nullable = false)
    private String location;

    @OneToOne(mappedBy = "address")
    private Library library;

    // standard constructor, getters, setters
}
```
- `@RestResource` annotation is optional but can be used to customize the endpoint.
- be careful when having different names for each association as you might encounter a `JsonMappingException`
- The association name defaults to the property name and can be customized using the `rel` attribute of `@RestResource`

```
@OneToOne
@JoinColumn(name = "secondary_address_id")
@RestResource(path = "libraryAddress", rel="address")
private Address secondaryAddress;
```

- specify a different value for the `rel` attribute or by omitting the `RR` annotation so that the resource name defaults to `secondaryAddress`.

### The Repositories

- create two repository interfaces for each of the classes by extending the `CrudRepository` interface.

```
public interface LibraryRepository extends CrudRepository<Library, Long> {}

public interface AddressRepository extends CrudRepository<Address, Long> {}
```

### Creating the Resources

- getting the `Library` instance to work:

```
curl -i -X POST -H "Content-Type:application/json" 
  -d '{"name":"My Library"}' http://localhost:8080
  libraries`
```

- The API return the JSON object

```
{
  "name" : "My Library",
  "_links" : {
    "self" : {
      "href" : "http://localhost:8080/libraries/1"
    },
    "library" : {
      "href" : "http://localhost:8080/libraries/1"
    },
    "address" : {
      "href" : "http://localhost:8080/libraries/1/libraryAddress"
    }
  }
}
```
### Creating the Associations

- this is done using the HTTP method PUT, which supports  a media type of text/uri-list and a body containing the URI of the resource to bind to the association.
- returns a status 204 if successful

```
curl -i -X PUT -d "http://localhost:8080/addresses/1" 
  -H "Content-Type:text/uri-list" http://localhost:8080/libraries/1/libraryAddress
```

### Data Model

```
@Entity
public class Book {

    @Id
    @GeneratedValue
    private long id;
    
    @Column(nullable=false)
    private String title;
    
    @ManyToOne
    @JoinColumn(name="library_id")
    private Library library;
    
    // standard constructor, getter, setter
}
```

- relationship to the Library class

```
public class Library {
 
    //...
 
    @OneToMany(mappedBy = "library")
    private List<Book> books;
 
    //...
 
}
```

- creating a BookRepository - `public interface BookRepository extends CrudRepository<Book, Long> { }`
- **add a book to the library** by creating a Book instance first:

```
curl -i -X POST -d "{\"title\":\"Book1\"}" 
  -H "Content-Type:application/json" http://localhost:8080/books
```

### Many-to-Many Relationship

- is defined using @ManyToMany annotation.

### The Data Model

- adds a new model class Author that will have a many-to-many relationship with the Boook entity:

```
@Entity
public class Author {

    @Id
    @GeneratedValue
    private long id;

    @Column(nullable = false)
    private String name;

    @ManyToMany(cascade = CascadeType.ALL)
    @JoinTable(name = "book_author", 
      joinColumns = @JoinColumn(name = "book_id", referencedColumnName = "id"), 
      inverseJoinColumns = @JoinColumn(name = "author_id", 
      referencedColumnName = "id"))
    private List<Book> books;

    //standard constructors, getters, setters
}
```

### The Repository

- create a repo interface to manage the Author entity:

```
public interface AuthorRepository extends CrudRepository<Author, Long> { }

```

## Intergration Testing in Spring

### Enable Test with JUnit5

- JUnit 5 define an extension interface through which classes can intergreate with the JUnit test
- enable this extension by adding the @ExtendWith annotation to our test classes and specifying the extenion clas to load.
- To run the Spring test, we use `SpringExtension.class`

```
@ExtendWith(SpringExtension.class)
@ContextConfiguration(classes = { ApplicationConfig.class })
@WebAppConfiguration
public class GreetControllerIntegrationTest {
    ....
}
```

- add the `ApplicationConfig.class` to the `@ContextConfiguration` which will load the configs for that particular test.
- `WebAppConfiguration` will load the web application context.

### WebApplicationContext Object

- provide a web application configuration.
- loads all the application bans and controllers into the context.

```
@Autowired
private WebApplicationContext webApplicationContext;
```

### Mocking Web Context Beans

- provides support for Spring MVC testing.
- encapsulates all web application beans and makes them available for testing.
- initialze the mockMvc object in the `@BeforeEach` annoation method

```
private MockMvc mockMvc;
@BeforeEach
public void setup() throws Exception {
    this.mockMvc = MockMvcBuilders.webAppContextSetup(this.webApplicationContext).build();
}
```

### Writing Integration Test

####  Verify View Name

```
@Test
public void givenHomePageURI_whenMockMVC_thenReturnsIndexJSPViewName() {
    this.mockMvc.perform(get("/homePage")).andDo(print())
      .andExpect(view().name("index"));
}
```

#### Verify Response Body

```
@Test
public void givenGreetURI_whenMockMVC_thenVerifyResponse() {
    MvcResult mvcResult = this.mockMvc.perform(get("/greet"))
      .andDo(print()).andExpect(status().isOk())
      .andExpect(jsonPath("$.message").value("Hello World!!!"))
      .andReturn();
    
    Assert.assertEquals("application/json;charset=UTF-8", 
      mvcResult.getResponse().getContentType());
}
```

### MockMvc Limitations

- provides an easy-to-use API to call web endpoints and to inspect and assert their response at the same time.
- uses a sublcass of the `DispatcherServlet` to handle test requests
- `TestDispatcherServlet` is responsible for calling contollers and performing all the familiar Spring magic.
- MockMvc class warps this TDS interally and so there are no real network connections made and it won't test the whole network stack

### Sources

[Spring Data REST](https://www.baeldung.com/spring-data-rest-relationships)   
[Integration Testing in Spring](https://www.baeldung.com/integration-testing-in-spring)  