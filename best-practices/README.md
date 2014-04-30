Best Practices
==============

A guide for programming well.

General
-------

* Don't duplicate the functionality of a built-in library.
* Don't swallow exceptions or "fail silently."
* Don't write code that guesses at future functionality.
* [Exceptions should be exceptional].
* [Keep the code simple].

[Exceptions should be exceptional]: http://www.readability.com/~/yichhgvu
[Keep the code simple]: http://www.readability.com/~/ko2aqda2

Object-Oriented Design
----------------------

* Avoid global variables.
* Avoid long parameter lists.
* Limit collaborators of an object (entities an object depends on).
* Limit an object's dependencies (entities that depend on an object).
* Prefer composition over inheritance.
* Prefer small methods. Between one and five lines is best.
* Prefer small objects with a single, well-defined responsibility. When an
  object exceeds 100 lines, it may be doing too many things.
* [Tell, don't ask].

[Tell, don't ask]: http://robots.thoughtbot.com/post/27572137956/tell-dont-ask

Ruby
----

* Avoid optional parameters. Does the method do too much?
* Avoid monkey-patching.
* Prefer classes to modules when designing functionality that is shared by
  multiple models.
* Prefer `private` when indicating scope. Use `protected` only with comparison
  methods like `def ==(other)`, `def <(other)`, and `def >(other)`.

Ruby Gems
---------

* Declare dependencies in the `<PROJECT_NAME>.gemspec` file.
* Reference the `gemspec` in the `Gemfile`.
* Use [Appraisal] to test the gem against multiple versions of gem dependencies
  (such as Rails in a Rails engine).
* Use [Bundler] to manage the gem's dependencies.
* Use [Travis CI] for Continuous Integration, indicators showing whether GitHub
  pull requests can be merged, and to test against multiple Ruby versions.

[Appraisal]: https://github.com/thoughtbot/appraisal
[Bundler]: http://bundler.io
[Travis CI]: http://travis-ci.org

Rails
-----

* Avoid bypassing validations with methods like `save(validate: false)`,
  `update_attribute`, and `toggle`.
* Avoid instantiating more than one object in controllers.
* Avoid naming methods after database columns in the same class.
* Don't change a migration after it has been merged into master if the desired
  change can be solved with another migration.
* Don't reference a model class directly from a view.
* Don't use instance variables in partials. Pass local variables to partials
  from view templates.
* Don't use SQL or SQL fragments (`where('inviter_id IS NOT NULL')`) outside of
  models.
* If there are default values, set them in migrations.
* Keep `db/schema.rb` or `db/development_structure.sql` under version control.
* Use only one instance variable in each view.
* Use SQL, not `ActiveRecord` models, in migrations.
* Use the [`.ruby-version`] file convention to specify the Ruby version and
  patch level for a project.
* Use `_url` suffixes for named routes in mailer views and [redirects].  Use
  `_path` suffixes for named routes everywhere else.
* Validate the associated `belongs_to` object (`user`), not the database column
  (`user_id`).
* Use `db/seeds.rb` for data that is required in all environments.
* Use `dev:prime` rake task for development environment seed data.
* Don't use a migration to manipulate database data, instead use a rake task.
* Use `db:setup` rake task when you are setting up the database for the first time on an existing project.

[`.ruby-version`]: https://gist.github.com/fnichol/1912050
[redirects]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.30

Testing
-------

* Avoid `any_instance` in rspec-mocks and mocha. Prefer [dependency injection].
* Avoid `its`, `let`, `let!`, `specify`, `before`, and `subject` in RSpec.
* Avoid using instance variables in tests.
* Disable real HTTP requests to external services with
  `WebMock.disable_net_connect!`.
* Don't test private methods.
* Test background jobs with a [`Delayed::Job` matcher].
* Use [stubs and spies] \(not mocks\) in isolated tests.
* Use a single level of abstraction within scenarios.
* Use an `it` example or test method for each execution path through the method.
* Use [assertions about state] for incoming messages.
* Use stubs and spies to assert you sent outgoing messages.
* Use a [Fake] to stub requests to external services.
* Use integration tests to execute the entire app.
* Use non-[SUT] methods in expectations when possible.

[dependency injection]: http://en.wikipedia.org/wiki/Dependency_injection
[`Delayed::Job` matcher]: https://gist.github.com/3186463
[stubs and spies]: http://robots.thoughtbot.com/post/159805295/spy-vs-spy
[assertions about state]: https://speakerdeck.com/skmetz/magic-tricks-of-testing-railsconf?slide=51
[Fake]: http://robots.thoughtbot.com/post/219216005/fake-it
[SUT]: http://xunitpatterns.com/SUT.html

Bundler
-------

* Specify the [Ruby version] to be used on the project in the `Gemfile`.
* Use a [pessimistic version] in the `Gemfile` for gems that follow semantic
  versioning, such as `rspec`, `factory_girl`, and `capybara`.
* Use a [versionless] `Gemfile` declarations for gems that are safe to update
  often, such as pg, thin, and debugger.
* Use an [exact version] in the `Gemfile` for fragile gems, such as Rails.

[Ruby version]: http://bundler.io/v1.3/gemfile_ruby.html
[exact version]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[pessimistic version]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle
[versionless]: http://robots.thoughtbot.com/post/35717411108/a-healthy-bundle

Postgres
--------

* Avoid multicolumn indexes in Postgres. It [combines multiple indexes]
  efficiently. Optimize later with a [compound index] if needed.
* Consider a [partial index] for queries on booleans.
* Constrain most columns as [`NOT NULL`].
* [Index foreign keys].

[`NOT NULL`]: http://www.postgresql.org/docs/9.1/static/ddl-constraints.html#AEN2444
[combines multiple indexes]: http://www.postgresql.org/docs/9.1/static/indexes-bitmap-scans.html
[compound index]: http://www.postgresql.org/docs/9.2/static/indexes-bitmap-scans.html
[partial index]: http://www.postgresql.org/docs/9.1/static/indexes-partial.html
[Index foreign keys]: https://tomafro.net/2009/08/using-indexes-in-rails-index-your-associations

Background Jobs
---------------

* Store IDs, not `ActiveRecord` objects for cleaner serialization, then re-find
  the `ActiveRecord` object in the `perform` method.

Email
-----

* Use [SendGrid] or [Amazon SES] to deliver email in staging and production
  environments.
* Use a tool like [MailView] to look at each created or updated mailer view
  before merging.

[Amazon SES]: http://robots.thoughtbot.com/post/3105121049/delivering-email-with-amazon-ses-in-a-rails-3-app
[SendGrid]: https://devcenter.heroku.com/articles/sendgrid
[MailView]: https://github.com/37signals/mail_view

JavaScript
----------

* Use Strict Mode: `'use strict';`
* Use CoffeeScript.

HTML
----

* Don't use a reset button for forms.
* Prefer cancel links to cancel buttons.

CSS
---

* Use Sass.

Sass
----

* Use `image-url` and `font-url`, not `url`, so the asset pipeline will re-write
  the correct paths to assets.

Browsers
--------

* Don't support clients without Javascript.
* Don't support IE6 or IE7.

Objective-C
-----------

* Prefer categories on `Foundation` classes to helper methods.
* Prefer string constants to literals when providing keys or key paths to methods.

Integration Testing For iOS
-----------

These are general guidelines and best practices you should follow when developing Integration Test for iOS apps

* Integration test is about the correctness of interacting object with each other, it’s about testing behavior, not functions.

* Testing on simulators is not the same as testing on actual devices - test your apps on actual devices under real-life conditions (like loss of internet connection, no gps signal in case your app uses them)

* Test your apps using Automate tool embedded in Instruments. Make sure it does object allocations judiciously and your code doesn't have leaks.

* The Automation instrument only works with apps that have been code signed with a development provisioning profile. Apps signed with a distribution provisioning profile can not be automated with the UI Automation programming interface.

* Simulated actions may not prevent the test device from auto-locking. Before running tests on a device, you should set the Auto-Lock preference to Never.

* Your test script must be a valid executable JavaScript file accessible to the instrument on the host computer. It runs outside your app, so the tested version of your app can be the same version that you submit to the iTunes App store.

* UI Automation uses the accessibility label (if it’s set) to derive a name property for each element.  You must use the UIViewController name followed by the name of the item.

* Test the app on all OS versions and device types your app supports.

* Test the app in different screen orientation, When performing a test that involves changing the orientation of the device, it is a good practice to set the rotation at the beginning of the test, then set it back to the original rotation at the end of your test. This practice ensures that your script is always back in a known state.

* Bundle the tests into related modules and run steps to log the test user out and clear the data between modules. The tests have to be decoupled from each other. If you run 50 integration tests one after the other and make a change to the fourth test that alters the app's state in a persistent way, you risk breaking the next 46 tests.

* It is impossible to test every possible user input, but you want to hit all your major error states as well as at least one valid input. It is impossible to test every path through the code, but you want to reasonably simulate the things a user is likely to do and spend a little more effort on the parts of the code that matter most to the user experience.

* Check the state of the screen (mostly via the accessibilityLabel and accessibilityValue properties of screen elements), interact with screen elements, check the state, interact, and so on. 

* The API does offer a #import directive that allows you to write smaller, reusable discrete test scripts. For example, if you were to define commonly used functions in a file named TestUtilities.js, you could make those functions available for use in your test script by including in that script the line

``` 
#import "<path-to-library-folder>/TestUtilities.js"
``` 

* You must explicitly stop recording. Completion or termination of your script does not turn off recording, If your app crashes or goes to the background, your script is blocked until the app is frontmost again, at which time the script continues to run.

* Handling Externally Generated Alerts to test push notifications, sms, and call
``` 
  UIATarget.onAlert = function onAlert(alert) {

    var title = alert.name();

    UIALogger.logWarning("Alert with title '" + title + "' encountered.");

    // return false to use the default handler

    return false;

    }
``` 

* Simplifying Element Hierarchy Navigation, use global variables to save the instance of most common used attributes like, target, app, tab bar, tableview 

// Switch screen (mode) based on value of variable
var target = UIATarget.localTarget();
var app = target.frontMostApp();
var tabBar = app.mainWindow().tabBar();

* Logging Test Results and Data: you should log as much information as you can, At a bare minimum, you should log when each test begins and ends, identifying the test performed and recording pass/fail status, you can even supplement the textual data with screenshots.


``` 
var testName = "Module 001 Test";

UIALogger.logStart(testName);

//some test code

UIALogger.logMessage("Starting Module 001 branch 2, validating input.");

//capture a screenshot with a specified name

UIATarget.localTarget().captureScreenWithName("SS001-2_AddedIngredient");

//more test code

UIALogger.logPass(testName);

``` 


Shell
-----

* Don't parse the output of `ls`. See [here][parsingls] for details and 
  alternatives.
* Don't use `cat` to provide a file on `stdin` to a process that accepts 
  file arguments itself.
* Don't use a `/bin/sh` [shebang][] unless you plan to test and run your 
  script on at least: Actual Sh, Dash in POSIX-compatible mode (as it 
  will be run on Debian), and Bash in POSIX-compatible mode (as it will 
  be run on OSX).
* Don't use any non-POSIX [features][bashisms] when using a `/bin/sh` 
  [shebang][].
* If calling `cd`, have code to handle a failure to change directories.
* If calling `rm` with a variable, ensure the variable is not empty.
* Prefer "$@" over "$\*" unless you know exactly what you're doing.
* Prefer `awk '/re/ { ... }'` to `grep re | awk '{ ... }'`.
* Prefer `find -exec {} +` to `find -print0 | xargs -0`.
* Prefer `for` loops over `while read` loops.
* Prefer `grep -c` to `grep | wc -l`.
* Prefer `mktemp` over using `$$` to "uniquely" name a temporary file.
* Prefer `printf` over `echo`.
* Prefer `sed '/re/!d; s//.../'` to `grep re | sed 's/re/.../'`.
* Prefer `sed 'cmd; cmd'` to `sed -e 'cmd' -e 'cmd'`.
* Prefer checking exit statuses over output in `if` statements (`if grep 
  -q ...; `, not `if [ -n "$(grep ...)" ];`).
* Prefer reading environment variables over process output (`$TTY` not 
  `$(tty)`, `$PWD` not `$(pwd)`, etc).
* Use `$( ... )`, not backticks for capturing command output.
* Use `$(( ... ))`, not `expr` for executing arithmetic expressions.
* Use `1` and `0`, not `true` and `false` to represent boolean 
  variables.
* Use `find -print0 | xargs -0`, not `find | xargs`.
* Use quotes around every `"$variable"` and `"$( ... )"` expression 
  unless you want them to be word-split and/or interpreted as globs.
* Use the `local` keyword with function-scoped variables.
* Identify common problems with [shellcheck][].

[shebang]: http://en.wikipedia.org/wiki/Shebang_(Unix)
[parsingls]: http://mywiki.wooledge.org/ParsingLs
[bashisms]: http://mywiki.wooledge.org/Bashism
[shellcheck]: http://www.shellcheck.net/

Bash
----

In addition to Shell best practices,

* Prefer `${var,,}` and `${var^^}` over `tr` for changing case.
* Prefer `${var//from/to}` over `sed` for simple string replacements.
* Prefer `[[` over `test` or `[`.
* Prefer process substitution over a pipe in `while read` loops.
* Use `((` or `let`, not `$((` when you don't need the result



