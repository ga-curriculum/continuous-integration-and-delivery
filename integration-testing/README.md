<h1>
  <span class="headline">Continuous Integration and Delivery</span>
  <span class="subhead">Integration Testing</span>
</h1>

**Learning objective:** By the end of this lesson, students will be able to evaluate how integration testing fits into a CI/CD workflow and identify common tools and frameworks for implementing it.


## Integration testing

<div class="activity knowledge-check">
  <h2 class="title">What's the difference between unit tests and integration tests?</h2>
  <span class="minutes"></span>
</div>

- **Unit tests** are designed to test small pieces of your code, such as individual functions or components, in isolation. These tests often use "mocked dependencies" to simulate external systems (like databases or APIs) so they run very quickly.

- **Integration tests** go a step further by testing how different parts of your application work together. For example, they might ensure that your application can connect to a real database or properly integrate with an external API. Because these tests involve initializing and using actual dependencies, they usually take longer to run.

To balance speed and thoroughness, CI pipelines typically have **stages**:

1. **Unit tests** run first to provide quick feedback if something is broken in the code logic.
2. **Integration tests** run later, often in a separate testing or QA environment, to verify that the full system works as expected.

## Finding bugs that unit tests won't find

Even if every individual part of your application works perfectly on its own, problems can still arise when you combine them. Unit tests are excellent for ensuring that individual components work as expected, but they don’t catch issues that occur when those components are integrated into the larger system.

For example, when changes from multiple developers are merged, or when different parts of the application interact, new bugs can emerge. This is why integration testing is essential: it verifies that the components work together as intended, even if all the unit tests pass.

<div class="activity knowledge-check">
  <h2 class="title">What might be some common sources of integration bugs?</h2>
  <span class="minutes"></span>
</div>

1. **Merge conflicts**: When merging code from several developers into a single branch, there are sometimes conflicts that can't be merged automatically. A human will need to step in and merge manually. This manual step can lead to bugs if not done perfectly. The larger the change, the more likely you are to encounter merge conflicts, so try to keep commits and PRs small.

2. **Using real components as dependencies** : Integration tests will usually aim to use _real components as dependencies_ instead of mocking the dependencies like we do in unit tests. By using real components, such as databases, application servers, containers, etc., integration tests are likely to surface problems that unit tests (with mocked components) simply wouldn't be capable of exposing.

3. **Incompatible interfaces or component behaviors** : This is the broadest category of integration bugs. Unit tests may pass for individual components, but integration tests (operating across multiple components) may fail if the components simply weren't designed to play well with each other. For example, one component (a REST endpoint) may accept dashes/hyphens in a user's last name, while another (a database table) might only accept alphanumeric characters. Passing a user's last name with hyphens to the REST endpoint and then to the database would fail an integration test.

## Integration testing frameworks and tools

Integration testing can be challenging because it often involves setting up and managing many components at once: databases, servers, containers, and more. To make this process smoother, there are tools and frameworks designed specifically to handle these complexities. 

They help you:

- Start up the needed environment (like databases or servers) before tests run.
- Run the tests against a real or simulated version of your application.
- Tear down and clean up everything after the tests finish.

Some common integration testing tools and frameworks include:

- [DbUnit](http://dbunit.sourceforge.net/) - Helps manage databases for testing by loading and comparing data.
- [TestNG](https://testng.org/doc/) - A testing framework that supports flexible configurations and advanced test structures.
- [Selenium](https://www.selenium.dev/) - Automates browser interactions to test web applications.
- [Arquillian](http://arquillian.org/) - Simplifies testing Java applications by handling container management and deployment details.
- [Spring Testing](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html#integration-testing) - Offers built-in support for testing Spring applications, including starting application contexts, managing transactions, and more.

We won’t dive deep into each of these here, but knowing they exist and what they generally do can guide you when you need more advanced integration testing solutions. Use the links above to further explore these resources. 
