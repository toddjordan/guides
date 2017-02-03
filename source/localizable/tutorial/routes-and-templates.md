In Super Rentals we want to arrive at a home page which shows a list of rentals.
From there, we should be able to navigate to an about page and a contact page.

Ember provides a [robust routing mechanism](../../routing/) to define logical, addressable pages within our application.

## An About Route

Let's start by building our "about" page.
To create a new, URL addressable page in the application, we need to generate a route using Ember CLI.

If we run `ember help generate`, we can see a variety of tools that come with Ember for automatically generating files for various Ember resources.
Let's use the route generator to start our `about` route.

```shell
ember generate route about
```

or for short,

```shell
ember g route about
```

The output of the command displays what actions were taken by the generator:

```shell
installing route
  create app/routes/about.js
  create app/templates/about.hbs
updating router
  add route about
installing route-test
  create tests/unit/routes/about-test.js
```

A route is composed of the following parts:

1. An entry in `/app/router.js`, mapping the route name to a specific URI. _`(app/router.js)`_
2. A route handler JavaScript file, instructing what behavior should be executed when the route is loaded. _`(app/routes/about.js)`_
3. A route template, describing the page represented by the route. _`(app/templates/about.hbs)`_

Opening `/app/router.js` shows that there is a new line of code for the _about_ route, calling `this.route('about')` in the `map` function.

Calling the function `this.route(routeName)`, tells the Ember router to run the specified route handler when the user navigates to the URI with the same name.
In this case when the user navigates to `/about`, the route handler represented by `/app/routes/about.js` will be run.

See the guide for [defining routes](../../routing/defining-your-routes/) for more details.

```app/router.js
import Ember from 'ember';
import config from './config/environment';

const Router = Ember.Router.extend({
  location: config.locationType,
  rootURL: config.rootURL
});

Router.map(function() {
  this.route('about');
});

export default Router;
```

By default, the `about` route handler loads the `about.hbs` template.
We don't actually have to change anything in the new `app/routes/about.js` route handler file,
as all we are doing is displaying static content in our `about.hbs` template.

With all of the routing in place from the generator, we can get right to work on coding our template.
For our `about` page, we'll add some HTML that has a bit of information about the site:

```app/templates/about.hbs
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>About Super Rentals</h2>
  <p>
    The Super Rentals website is a delightful project created to explore Ember.
    By building a property rental site, we can simultaneously imagine traveling
    AND building Ember applications.
  </p>
</div>
```

Run `ember server` (or `ember serve` or even `ember s` for short) from the shell to start the Ember development server,
and then go to [`http://localhost:4200/about`](http://localhost:4200/about) to see our new app in action!

## A Contact Route

Let's create another route with details for contacting the company.
Once again, we'll start by generating a route, a route handler, and a template.

```shell
ember g route contact
```

The output from this command shows a new `contact` route in `app/router.js`,
and a corresponding route handler in `app/routes/contact.js`.

In the route template `/app/templates/contact.hbs`, we can add the details for contacting our Super Rentals HQ:

```app/templates/contact.hbs
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>Contact Us</h2>
  <p>Super Rentals Representatives would love to help you<br>choose a destination or answer
    any questions you may have.</p>
  <p>
    Super Rentals HQ
    <address>
      1212 Test Address Avenue<br>
      Testington, OR 97233
    </address>
    <a href="tel:503.555.1212">+1 (503) 555-1212</a><br>
    <a href="mailto:superrentalsrep@emberjs.com">superrentalsrep@emberjs.com</a>
  </p>
</div>
```

Now we have completed our second route.
If we go to the URL [`http://localhost:4200/contact`](http://localhost:4200/contact), we'll arrive on our contact page.

## Navigating with Links and the {{link-to}} Helper

We'd like to avoid our users having knowledge of our URLs in order to move around our site,
so let's add some navigational links at the bottom of each page.
Let's make a contact link on the about page and an about link on the contact page.

Ember has built-in template **helpers** that provide functionality for interacting with the framework.
The [`{{link-to}}`](../../templates/links/) helper provides special ease of use features in linking to Ember routes.
Here we will use the `{{link-to}}` helper in our code to perform a basic link between routes:

```app/templates/about.hbs{+9,+10,+11}
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>About Super Rentals</h2>
  <p>
    The Super Rentals website is a delightful project created to explore Ember.
    By building a property rental site, we can simultaneously imagine traveling
    AND building Ember applications.
  </p>
  {{#link-to 'contact' class="button"}}
    Contact Us
  {{/link-to}}
</div>
```

The `{{link-to}}` helper takes an argument with the name of the route to link to, in this case: `contact`.
When we look at our about page at [`http://localhost:4200/about`](http://localhost:4200/about), we now have a working link to our contact page.

![super rentals about page screenshot](../../images/routes-and-templates/ember-super-rentals-about.png)

Now, we'll add a link to our contact page so we can navigate back and forth between `about` and `contact`.

```app/templates/contact.hbs{+15,+16,+17}
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>Contact Us</h2>
  <p>Super Rentals Representatives would love to help you<br>choose a destination or answer
    any questions you may have.</p>
  <p>
    Super Rentals HQ
    <address>
      1212 Test Address Avenue<br>
      Testington, OR 97233
    </address>
    <a href="tel:503.555.1212">+1 (503) 555-1212</a><br>
    <a href="mailto:superrentalsrep@emberjs.com">superrentalsrep@emberjs.com</a>
  </p>
  {{#link-to 'about' class="button"}}
    About
  {{/link-to}}
</div>
```

## A Rentals Route
We want our application to show a list of rentals that users can browse.
To make this happen we'll add a third route and call it `rentals`.

```shell
ember g route rentals
```

Let's update the newly generated `app/templates/rentals.hbs` with some basic markup to add some initial content our rentals list page.
We'll come back to this page later to add in the actual rental properties.

```app/templates/rentals.hbs
<div class="jumbo">
  <div class="right tomster"></div>
  <h2>Welcome!</h2>
  <p>We hope you find exactly what you're looking for in a place to stay.</p>
  {{#link-to 'about' class="button"}}
    About Us
  {{/link-to}}
</div>
```

## An Index Route

With our three routes in place, we are ready to add an index route, which will handle requests to the root URI (`/`) of our site.
We'd like to make the rentals page the main page of our application, and we've already created a route.
Therefore, we want our index route to simply forward to the `rentals` route we've already created.

Using the same process we did for our about and contact pages, we will first generate a new route called `index`.

```shell
ember g route index
```

We can see the now familiar output for the route generator:

```shell
installing route
  create app/routes/index.js
  create app/templates/index.hbs
installing route-test
  create tests/unit/routes/index-test.js
```

Unlike the other route handlers we've made so far, the `index` route is special:
it does NOT require an entry in the router's mapping.
We'll learn more about why the entry isn't required later on when we look at [nested routes](../subroutes) in Ember.

All we want to do when a user visits the root (`/`) URL is transition to `/rentals`.
To do this we will add code to our index route handler by implementing a route lifecycle hook,
called `beforeModel`.

Each route handler has a set of "lifecycle hooks", which are functions that are invoked at specific times during the loading of a page.
The [`beforeModel`](http://emberjs.com/api/classes/Ember.Route.html#method_beforeModel)
hook gets executed before the data gets fetched from the model hook, and before the page is rendered.
See [the next section](../model-hook) for an explanation of the model hook.

In our index route handler, we'll call the [`replaceWith`](http://emberjs.com/api/classes/Ember.Route.html#method_replaceWith) function.
The `replaceWith` function is similar to the route's `transitionTo` function,
the difference being that `replaceWith` will replace the current URL in the browser's history,
while `transitionTo` will add to the history.
Since we want our `rentals` route to serve as our home page, we will use the `replaceWith` function.

In our index route handler, we add the `replaceWith` invocation to `beforeModel`.

```app/routes/index.js{+4,+5,+6}
import Ember from 'ember';

export default Ember.Route.extend({
  beforeModel() {
    this.replaceWith('rentals');
  }
});
```

Now visiting the root URL `/` will result in the `/rentals` URL loading.

## Adding a Banner with Navigation

In addition to providing button-style links in each route of our application, we would like to provide a common banner to display both the title of our application, as well as its main pages.

To show something in every page of your application, you can use the application template.
The application template is generated when you create a new project.
Let's open the application template at `/app/templates/application.hbs`, and add the following banner navigation markup:


```app/templates/application.hbs
<div class="container">
  <div class="menu">
    {{#link-to 'index'}}
      <h1 class="left">
        <em>SuperRentals</em>
      </h1>
    {{/link-to}}
    <div class="left links">
      {{#link-to 'about'}}
        About
      {{/link-to}}
      {{#link-to 'contact'}}
        Contact
      {{/link-to}}
    </div>
  </div>
  <div class="body">
    {{outlet}}
  </div>
</div>
```

Notice the inclusion of an `{{outlet}}` within the body `div` element.
The [`{{outlet}}`](http://emberjs.com/api/classes/Ember.Templates.helpers.html#method_outlet)
in this case is a placeholder for the content rendered by the current route, such as _about_, or _contact_.

At this point you should have the ability to navigate between your _about_, _contact_, and _rentals_ pages.

From here you may move on to the [next page](../model-hook/), or walk through how to test the new functionality you've added.

## Implementing Acceptance Tests

Now that we have created routes to load various pages of our application, lets walk through how to create tests to exercise them.

As we learned in [Planning the Application](../acceptance-test/),
an acceptance test in Ember is an automated test that starts up the application and interacts with it in a way similar to what a user would do.

If you open the acceptance test we created in that section, you'll see our list of goals represented as tests,
including the ability to navigate to an about page and a contact page.

Ember provides a variety of default test helpers for acceptance tests that can be used to perform common tasks,
such as visiting routes, filling in fields, clicking on elements, and waiting for pages to render.

A few helpers are at play in the tests we are about to write:

* The [`visit`](http://emberjs.com/api/classes/Ember.Test.html#method_visit) helper loads the route specified for the given URL.
* The [`click`](http://emberjs.com/api/classes/Ember.Test.html#method_click) helper simulates a user clicking on specific parts of the screen.
* The [`andThen`](../../testing/acceptance/#toc_wait-helpers)
  helper waits for all previously called test helpers to complete before executing the function you provide it.
  In this case, we need to wait for the page to load after `click`, so that we can assert that the new page is loaded.
* [`currentURL`](http://emberjs.com/api/classes/Ember.Test.html#method_currentURL) returns the URL that test application is currently visiting.

First, we want to test the index route we created, that redirects traffic directed at the root URL `/`, to `/rentals`.
In this test case we'll simply visit the root URL and assert that the current URL is `/rentals` once the page is loaded.

```/tests/acceptance/list-rentals-test.js
test('should show rentals as the home page', function (assert) {
  visit('/');
  andThen(function() {
    assert.equal(currentURL(), '/rentals', 'should redirect automatically');
  });
});
```

Now run the tests by typing `ember test --server` in the command line (or `ember t -s` for short).

Instead of 7 failures there should now be 6 (5 acceptance failures and 1 jshint).
Note that you can narrow down the tests being run to just our acceptance test by selecting the entry called,
"Acceptance | list rentals" in the drop down input labeled "Module" on the test UI.

Also remember to toggle "Hide passed tests" to show your passing test case along with the failures that you haven't yet implemented.

Next, to test the about and contact pages,
we will add code that simulates a user clicking on these links from the home page and verifies that the new page is loaded.

In each test, visit the app at its root, click on the link based on its name, and then assert that the new URL is loaded.

```/tests/acceptance/list-rentals-test.js
test('should link to information about the company.', function (assert) {
  visit('/');
  click('a:contains("About")');
  andThen(function() {
    assert.equal(currentURL(), '/about', 'should navigate to about');
  });
});

test('should link to contact information', function (assert) {
  visit('/');
  click('a:contains("Contact")');
  andThen(function() {
    assert.equal(currentURL(), '/contact', 'should navigate to contact');
  });
});
```

If your ember test process is still running it should update to reflect your newly passed tests.

Note that we can call the two helpers, `visit` and `click` back to back without the need to wait for the page to load after visit.
This is because `visit` and `click` are [asynchronous test helpers](../../testing/acceptance/#toc_asynchronous-helpers).
Asynchronous test helpers are made to wait until other asynchronous test helpers are complete before executing.

The three acceptance tests we created for navigating to our routes should now pass.
In the screen recording below, we run the tests, deselect "Hide passed tests", and set the module to our acceptance test,
revealing the 3 tests we got passing.

![passing navigation tests](../../images/routes-and-templates/ember-route-tests.gif)

