# QA-Engine - Gherkin / BDD Test Automation
==============================

QA-Engine uses the English language to describe executable test cases - particularly for web apps and APIs. 

QA-Engine supports a BDD/Gherkin syntax with many useful built-in phrases. You see them [here](PHRASES.md) 

Gherkin is human and machine readable - so business analysts, testers, developers and robots can collaborate.

Since tests are written in English - almost every stakeholder can make sense of them.

Each test is defined using declarative style, meaning you say what you want it to, but not how to do it. 

I want to automate testing
==========================

With QA-Engine, you write your test cases in a simplified dialect of English - called Gherkin. 

Traditional test scripts are often unreadable by our stakeholders and even ourselves.

QA-Engine uses executable English instructions - actions and assertions - that are easy to read, write and socialise.

Features are lists of related scenarios. It's the scenario's that do all the heavy lifting.

A scenario describes your pre-conditions, actions and outcomes in a way that is both human and machine friendly.

I want to understand Gherkin
============================

The Gherkin (BDD) notation for a feature / scenario is:

	Feature: Basic Examples

	Scenario: An example
		GIVEN   some context
		WHEN    an action is performed
		THEN    an outcome is expected

The text following the keyword (GIVEN | WHEN | THEN) needs to match a phrase/pattern from a vocabulary.

New features can be created using any simple text editor - where you'd use QA-Engine's extensible vocabulary to write them.

You can download pre-packaged vocabularies (called Dialects) and/or roll your own with simple Javascript.

I want to see a working example
===============================

QA-Engine's features are collections of individual test scenarios. 

To improve readability, the keyword AND can be used instead in place of the verbs above.

You can influence what QA-Engine understands using @dialect annotations.

	Feature: Verify that Google is accessible
	
	Background: Google Scenarios
	
	    Given I am googling
	
	 Scenario: Request Google homepage - with redirects
	
	    Given I enable redirects
	    When I GET http://google.com
	    Then response code should be 200
	
	 Scenario: Request Google homepage - no redirect
	
	    Given I disable redirects
	    When I GET /
	    Then response code should be 3xx

I want to test-drive QA-Engine
======================================

QA-Engine is built using NodeJS. 

You install QA-Engine as a system-wide CLI command:

	$ npm install qa-engine-cli -g

To run it simply type:

	$ qa

However, It won't do much else until we provide some feature scenarios.

By default, QA-Engine looks for ".feature" files recursively, starting in the current directory.

I want to create my first feature
=================================

This will create the ./features folder and copy some simple examples.

It will also write your default configuration to ./QA-Engine.json

It won't damage if you run it again, except re-save your ./QA-Engine.json config.

To execute your example ".feature" files, type:

```
	qa
```

I want to learn more about QA-Engine
====================================

For runtime options, type:

	$ qa  -h
 
For a list of [supported phrases](PHRASES.md), type:

	$ qa  -p

I want to write some examples
===============================

Let's create a trivial example of a hypothetical test case.

	Scenario: Trivial Test

        Given I am testing debug
        When debug works
		And I succeed

The steps are executed in sequence.

The GIVEN steps setup pre-conditions. The "Given I am $acting" phrase doesn't do much - except communicate intentions.

The "WHEN ... " steps do useful work that result in desirable outcomes. For example: writing a file, requesting a web page, etc.

In this example, we simply write a debug message to the console, so let's turn on debug output.

	$ qa -v

The "THEN ..." steps make assertions, that is they test that conditions are met. For example, you can use arbitrary Javascript if necessary:

        Then I assert $some_javascript

The "I succeed", "I pass" always meet their conditions. The inverse "I fail" forces the scenario to abort and report it's failure.

I want to organise my work into folders
=======================================

If your features are in a different location then use the "--features" or "--epics" option to locate them. 

	$ qa -f ./features

These folders are not automatically created, they return an error if they're not found.

I want to re-use my features in other projects
==============================================

QA-Engine was designed to support a declarative style so that features are portable. 

Supplying a different "config" file for each environment allows features to be re-used across multiple environments.

For example, features can adapt to dev, QA and live environments - injecting hostnames, credentials, etc as required.

Most Dialects configure themselves automatically. 

If yours doesn't then there is alternative - use {{mustache}} templates to modify statements prior to execution.

	Given I login as {{actor}}

In this way, your BDD features are neatly abstracted from your runtime configuration.

To specify a runtime configuration for your features, type:

	$ qa -c ./my-context.json

By default, QA-Engine will try to load a configuration file called "QA-Engine.json" from your current directory. 

If no file is found, then sensible default values are defined.

I want to know how it works
===========================

First, QA-Engine parses the command line and initializes the Dialect, Features and Engine components.

Next it loads the default dialects. These can be specified on using the QA-Engine_DIALECT environment variable. Dialects can also be
specified using --dialect option and within Feature: definitions using the @dialect annotation.

Each Dialect instructs the parser (Yadda) to match a set of Gherkin phrases to their related function.

The Feature manager converts features and scenarios into executable units. 

User defined variables are scoped at the feature-level meaning they are shared between scenarios within the same feature. 

The --config file is used as the basis for internal context variables. They are scoped to each scenario.

These variables - such as web requests/responses - can be accessed using the "this." qualifier - with due caution.

Next, the Engine runs each feature using the built-in Mocha runner. Results are correlated and output according to your CLI options.

I want to add comments
======================

It's useful to document your intentions or to prevent a statement from running, for example during development.

Simple, place a # before any line and it will be ignored by QA-Engine.

	# This is ignored by the parser
```
	Scenario: Comments Example

		Given I am using comments
		# Then I fail
		Then I succeed
```

I want to use QA-Engine
================================

This software is licensed under the Apache 2 license, quoted below.

Copyright &copy Troven 2009-2020

Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License. You may obtain a copy of
the License at

    [http://www.apache.org/licenses/LICENSE-2.0]

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations under
the License.

