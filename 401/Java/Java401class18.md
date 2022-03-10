# Hibernate Many to Many

- Many-to-Many relationships is a connection between two types of entities. Both sidse can relate to mutiple instances of the other side.
- Annotate the class with @Entity and the primary key with @id to them proper JPA entities.
- Use the @JoinTable or @JoinColumn attribute connects the owner side of the relatioinship and the inverse colum to the other side.
- On the target side, you only need to provide the name of the field with maps to the relationship @Many-to-Many(mappBy = "name_here")

## Common Spring Annotations

- @id - marks a field in a model class as the primary key
- @Transient - marks a field in a model class as transient.
- @CreatedBy, @LastModifiedBy, @CreatedDate, @LastModifiedDate - can audit our model classes: spring automatically populates the annotaed fields with the principle who created the object, last modified it, and the date of creation and last modified.
- @Param - can pass named parameters to our queries.
- @EnableJpaRepositories - indicates to spring that we intend to use this as a repo.(have to use @Configuration with it)
- @Configuration - used on classes which defines bean as the source of the bean as the source of the bean file. A java class that is annotated with this will configure itself and import the methods to instantiate and config the dependencies.
- @Controller - used with Spring MVC and Webflux. Detects the component class form the classpath and autoregister the bean definition.
- @Requestmapping - used to map the web request. It can hold several optional components such as consumes, header, method names, params, path, etc.
- @GetMapping - used to map the HTTP GET request on the specific handler method.
- @PostMapping - used for mapping HTTP POST requests onto the specific handler method.
- @PutMapping - maps the HTTP PUT request.
- @ DeleteMappig - maps the HTTP DELETE request.
- @RequestBody - used to bind the HTTP request with an object in a method paramter.
- @ResponeBody - used to bind the method return value to the response body.
- @PathVariable - extracts the values from the URL
- @RequestParam - queury parameter used to extract teh query parameters from the URL.
- @RequestHeader - gets the details about the HTTP request headers. It can be used as a method param.
- @RestController - combination of @Controller and @ResponseBody annotations. 
- @RequestAttribute - wraps a method parameter to the request attribute.
- @CookieValue - used at the method parameter level. It's used as request mapping method's argument.
- @CrossOrigin - used both at the class & method level. It's sued to enable cross-origin request.