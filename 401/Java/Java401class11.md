# Spring

## Serving Web Content with Spring MVC

### How to complete this guide

- To start from scratch, move on to the [Starting with Spring Initializer](https://spring.io/guides/gs/serving-web-content/#scratch)
- To skip the basics, do the following:
  - [Download](https://github.com/spring-guides/gs-serving-web-content/archive/main.zip) and unzip the source repo for this guide or clone using git.
  - cd into `gs-serving-web-content/initials`
  - jump head to [Create a Web Controller](https://spring.io/guides/gs/serving-web-content/#initial)
- check your result against the code in the `gs-serving-web-content/complete`

### Starting with Spring Initializer

- can use this [pre-initialized project](https://start.spring.io/#!type=maven-project&language=java&platformVersion=2.5.5&packaging=jar&jvmVersion=11&groupId=com.example&artifactId=serving-web-content&name=serving-web-content&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.serving-web-content&dependencies=web,thymeleaf,devtools) and click to generate to download a ZIP file. This project is configured to fit the examples in this tutorial.

- To manually initialize project:
  - navigate [here](https://start.spring.io/). This service pulls in all the dependencies you need for an app and does most of the setup for you.
  - choose either Gradle or Maven and the language you want to use.
  - click **Dependencies** and select **Spring Web, 
    Tymeleaf** and **Spring Boot DevTools**.
  - click **Generate**
  - Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.
- If IDE has the Spring Initializer intergration, you can complete the process from there.
- can also fork the project from Github and open it in your IDE.

### Create a Web Controller

package com.example.servingwebcontent;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class GreetingController {

	```
        @GetMapping("/greeting")
	public String greeting(@RequestParam(name="name", required=false, defaultValue="World") String name, Model model) {
		model.addAttribute("name", name);
		return "greeting";
	}```

- HTTP request are handled by a controller identified as `@Controller` annotation.
- A `View` is responsible for rendering the HTML content.
- The `@GetMapping` annotation ensures that HTTP GET request are mapped to the correct `greeting()`.
- The `@RequestParam` binds the value of the query string parameter `name` into the `name` param of the `greeting()`
- if not query string was provided, the defualt value will be applied.
- Tymeleaf parses the `greeting.html` template and evaluates the `th:text` expression to render the value of teh `${name}` para.

### Spring Boot Devtools

- enables [hot swapping](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto-hotswapping)
- switches template engines to disable caching
- enables LiveReload to auto refresh browser
- other defualts based on dev instead of production

### Run the App

- spring initializer creates an app class for you.
- `@SpringBootApplication` is a convenience annotation that adds the following:
  - `@Configuration`: tags the class as a source of bean definitions for the application context.
  - `@EnableAutoConfig`: tells SB to start adding beans based on classpath settings, other beans and various property settings.
  - `@ComponentScan`: tells SB to look for other components, configs and services letting it find the controllers
- `main()` uses SB's `SpringApplication.run()` to launch an app.

### Build an executable JAR

- can run the app from command line with Gradel or Maven.
- can build a single executable JAR file that contains all the necessary depends, classes and resources and run that.
- building a exe JAR makes it easy to ship, version and deploy the service as an application throughout dev lifecycle.
- Gradle run: `./gradlew bootRun`
- Alternatively, build JAR file: `./gradlew build`, then run the JAR `java -jar build/libs/gs-serving-web-content-0.1.0.jar`
- Maven run: `./mvnw spring-boot:run`
- build JAR: `./mvnw clean package`, then run the JAR `java -jar target/gs-serviing-web-content-0.1.0.jar`

### Testing the App

- website should be running at `http://localhost:8080/greeting`

### Add a Home Page

- SB serves static content from resources in the classpath `/static` or `/public`
- the `index.html` resource is used as a welcome page and is used as the root resource.
- create the file at `src/main/resources/static/index.html`:

```<!DOCTYPE HTML>
<html>
<head> 
    <title>Getting Started: Serving Web Content</title> 
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p>Get your greeting <a href="/greeting">here</a></p>
</body>
</html>
```

### Spring MVC and Thymeleaf: how to access data from templates

- `@Controller` classes are responsible for preparing a model map with data and selecting a view to be rendered.
- The model map allows for the complete abstraction of the view tech and it is transformed inot a Thymeleaf context object.

### 1. Spring model attributes

- Spring MVC calls the pieces of data that can be accessed during the execution of vies model attribues.
- Tymeleaf language is context variables.
- there are several ways of adding model attributes to a view in MVC.
- `model.addAttribute()`
- `ModelAndView mav = new ModelAndView("message/list");`
- `@ModelAttribute()` as method annotations.
- all of the above add the messages attribute to the model and will be available in Thymeleaf views.
- access the model attributes with following Spring EXpression Language (EL) syntax: `${attributeName}`
- EL supports querying and manipulating an object graph at runtime.

### 2. Request Params

- passed from the client to server `https://example.com/query?q=Thymeleaf+Is+Great!`
- to access the `q` param use the param prefix: `<p th:text="${param.q}">Test</p>`
- multivalued params with `${param.q}` will return serialized array as a value.

### 3. Session attributes

- session attribs can be accessed using the`${session}` prefix.

### 4. ServletContext attribs

- shared between requests adn sessions.
- prefix: `${#servletContext.getAttributes()}`

### 5. Spring beans

- Thymeleaf allows accessing beans registered at the Spring App Context with the `@beanName` syntax.

## Sources

[Spring](https://spring.io/guides/gs/serving-web-content/)
[Thymeleaf](https://www.thymeleaf.org/doc/articles/springmvcaccessdata.html)
