Testing is a core part of the Ember framework and its development cycle.

Let's assume you are writing an Ember application which will serve as a blog.
This application would likely include models such as `user` and `post`. It would
also include interactions such as _login_ and _create post_. Let's finally
assume that you would like to have [automated tests] in place for your application.

There are three different classifications of tests that you will need:
**Acceptance**, **Unit**, and **Integration**.

### Acceptance Tests

Acceptance tests are used to test the application end to end.  The tests interact
with the application in the same ways that a user would, by doing things like filling out
form fields and clicking buttons.  Acceptance tests ensure that the features within
a project are basically functional, and are valuable in ensuring the core features of a
project have not regressed, and that the project's goals are being met.

In the example scenario above, some acceptance tests one might write are:

* A user is able to log in via the login form.
* A user is able to create a blog post.
* Saving a post successfully shows the list of prior posts.
* A visitor does not have access to the admin panel.

### Unit Tests

Unit tests are used to drive isolated chunks of functionality, or "units". They are
often most effective when written within an interactive TDD cycle, where the developer writes
a failing test, develops the functionality to get the test passing, and then circles back to
clean the code by doing things like removing duplication and poor naming
(red->green->refactor).

While unit tests are written against any isolated application logic, some specific
examples for the scenario above might be:

* A fullname attribute is computed which is the aggregate of its first and last.
* The serialized properly converts the blog request payload into a blog post model object.
* Blog dates are properly formatted.

### Integration Tests

Integration tests serve as a middle ground between acceptance tests, who only interact with the
full system through user endpoints, and unit tests, who interact with specific code algorithms
on a micro level. Integration tests verify interactions between various parts of the
application, such as behavior between various UI controls.  They are valuable in ensuring
data and actions are properly passed between various parts of the system, and provide
confidence that parts of the system will work within the application under various scenarios.

It is recommended that components be tested with integration tests because the component
interacts with the system in the same way that it will within the context of the application,
including being rendered from a template and receiving Ember's lifecycle hooks.

Examples of integration tests from the above example might include:

* An author's full name and date are properly displayed in a blog post.
* A user is prevented from typing more than 50 characters into post's title field.
* Submitting a post without a title displays a red validation state on the field and gives
the user text indicating that the title is required.
* The blog post list scrolls to position a new post at the top of the viewport.

### Testing Frameworks

[QUnit] is the default testing framework for this guide, but others are supported through
third-party addons.

### How to Run Your Tests

Run your tests with `ember test` on the command-line. You can re-run your tests on every
file-change with `ember test --server`. Another way to run the tests when you are running
a local server (started by running `ember server`), is to navigate your browser to the address
of your local server, which by default is `http://localhost:4200/tests`.
These commands run your tests using [Testem] to make testing multiple browsers very easy. You
can configure Testem using the `testem.json` file in your application root.

[automated tests]: http://en.wikipedia.org/wiki/Test_automation
[QUnit]: http://qunitjs.com/
[Testem]: https://github.com/airportyh/testem
