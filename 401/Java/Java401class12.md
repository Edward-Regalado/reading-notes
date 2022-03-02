# Accessing Data with JPA

- annotate the class with JPA's `@Entity`
- classes need to have two constructors- the default constructor only exists for JPA and it's `protected`.
- the `id` property is annoted with `@id` so that JPA recognizes it as the object's ID.
- `id` is also annotated with `@GeneratedValue` to indicatet that the id should be auto generated.

## Create Simple Queries

- Spring Data JPA focuses on using JPA to store data in a relational database.
- creates a repository implementation automatically at runtime from a repo interface.

``` 
package com.example.accessingdatajpa;

import java.util.List;

import org.springframework.data.repository.CrudRepository;

public interface CustomerRepository extends CrudRepository<Customer, Long> {

  List<Customer> findByLastName(String lastName);

  Customer findById(long id);
}
```
- `CustomerRepository` extends `CrudRepository` interface.
- the type of entity and ID that works with `Customer` and `Long` are specified in the generic params on `CrudRepository`.
- Spring Data JPA lets you define other query methods by declaring their method signature.


### Create an Application Class

- `@SpringBootApplication` adds the following:
    - `@Configuration`: tags teh class as a source of bean def for the app context.
    - `@EnableAutoConfiguration`: tells SB to start adding bean based on classpath settings and various property settings.
    - `@ComponentScan`: tells SB to look for other components, configs and services in the `com/example` package, letting it find controllers.

- The `main()` uses SB `SpringApplication.run()` to launch an application.

```
package com.example.accessingdatajpa;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;

@SpringBootApplication
public class AccessingDataJpaApplication {

  private static final Logger log = LoggerFactory.getLogger(AccessingDataJpaApplication.class);

  public static void main(String[] args) {
    SpringApplication.run(AccessingDataJpaApplication.class);
  }

  @Bean
  public CommandLineRunner demo(CustomerRepository repository) {
    return (args) -> {
      // save a few customers
      repository.save(new Customer("Jack", "Bauer"));
      

      // fetch all customers
      log.info("Customers found with findAll():");
      log.info("-------------------------------");
      for (Customer customer : repository.findAll()) {
        log.info(customer.toString());
      }
      log.info("");

      // fetch an individual customer by ID
      Customer customer = repository.findById(1L);
      log.info("Customer found with findById(1L):");
      log.info("--------------------------------");
      log.info(customer.toString());
      log.info("");

      // fetch customers by last name
      log.info("Customer found with findByLastName('Bauer'):");
      log.info("--------------------------------------------");
      repository.findByLastName("Bauer").forEach(bauer -> {
        log.info(bauer.toString());
      });
      // for (Customer bauer : repository.findByLastName("Bauer")) {
      //  log.info(bauer.toString());
      // }
      log.info("");
    };
  }

}
```
- The `@AccessingDataJpaApplication` class includes a `demo()` that puts the `CustomerRepository` through a few tests.
- fetches the `CustomerRepository` from the spring app context, then saves a few random `Customer` object to thest the `save()` and setting up some data to work with.
- `findall()` fecthes all `Customer` objects from the DB
- `findById()` to fetch a single `Customer` by its ID.
- `findByLastName()` to search for a customer by their last name.

### Build an exe JAR

- you can build a single exe JAR fiel that contains all teh necessary dependencies, classes and resources and run that.
- JAR file make the application easy to ship, version and deploy the service as an app throughout the dev lifecycle.
- for gradle run: `./gradlew bootRun`
- buld a JAR file: `./gradlew build` and run the JAR file.
- `java -jar build/libs/gs-accessing-data-jpa-0.1.0.jar`

## Spring Data Repositories

- CudeRepository provides CRUD functions
- PagingAndSorting provides methods to do pagination and sort records
- JpaRepositories provides JPA related methods such as flushing the persistaenct context and delete records in a batch.
- JpaRepo contains the full API of both crud and paging/sorting


## CrudRepository

- `save()` saves an Iterable of objects. Here, we can pass multiple objects to save them in a batch
- `findOne(…)` gets a single entity based on passed primary key value
- `findAll()` gets an Iterable of all available entities in database
- `count()`  returns the count of total objects in a table
- `delete(…)` delete an object based on the passed object
- `exists(…)` verify if an object exists based on the passed primary key value


### Sources

[Spring](https://spring.io/guides/gs/accessing-data-jpa/)  
[Baeldung](https://www.baeldung.com/spring-data-repositories)