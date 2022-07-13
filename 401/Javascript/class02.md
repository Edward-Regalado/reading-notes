# Express, NPM, TDD, CI/CD

## NodeJS and Express

1. Explain middleware, answer as though I were a non-technical recruiter. Gives you access to the req and res in the apps request -> response cycle. Middleware functions are a great place to modify the req and res objects with relevant information.
2. Express the most popular `Node Web Framework`.
3. Express is “un-opinionated.” What does that mean? there is no one right way to do things. This give devs less restrictions on the best way to put components together to achieve a goal. Makes it easier for developers to use the most suitable tools to complete a particular task. By contrast an opinionated framework forces/guides you into a specific way to do something.
4. What is a module and why is modularity useful to us as developers? It's a JS library/file that you can import into other code using Node's `require()` function. Modularity minimizes the risks of ending up with programming errors and also makes it easier to spot errors.

### What is NPM?

1. What version of npm are you running on your machine? 8.12.1
2. What command would you type to install a library/package called ‘jshint’ into your node project? `npm install -g jshint` or `npm install jshint`

### What is TDD?

1. Explain why tests are important. Please explain as though I were your non technical elder. I think tests are important because you'll end up with fewer bugs and errors in your code. When you spend less time fixing bugs, you can use that time to increase the quality of the final product.
2. What are three expected benefits of testing. reduction in defect rates, reduction in effort in project's final phases, improved design qualities in the code.
3. Name at lest 2 individual pitfalls and at least 2 team pitfalls commonly encountered while writing tests. Personal: not running test frequently & writing too many tests at once. Team: partial adoption- not everyone on the team uses TDD. Poor maintenance of the test suite.

### CI/CD

1. What are three benefits of Continuous Integration? ensure everyone's changes integrate, catch bugs and reduce merge conflicts.
2. What is the difference between Continuos Delivery and Continuous Deployment? Continuous Delivery is the practice of developing software to release at any time. CD + CI lets you to develop features with modular code in a much more manageable increments. Continuous Deployment is an extension of Continuous Delivery as allows you to deploy new features immediately.
3. Explain how GitHub fits into this process assuming the listener comes from a non-technical background. Github acts like a clearing house for your code, tracks changes to your code and communicates with other systems about those changes using webhooks and APIs.

## Things I want to know more about

- what are best practices in agile Test-driven development.

## Sources

[Express/Node](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction)  
[TDD](https://www.agilealliance.org/glossary/tdd/#q=~(infinite~false~filters~(postType~(~'page~'post~'aa_book~'aa_event_session~'aa_experience_report~'aa_glossary~'aa_research_paper~'aa_video)~tags~(~'tdd))~searchTerm~'~sort~false~sortDirection~'asc~page~1))  
[CI/CD](https://www.youtube.com/watch?v=xSv_m3KhUO8)