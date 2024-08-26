# Testing your code
Testing is a critical skill in software development. It helps ensure your code works as expected and remains reliable as it evolves. In this lesson, we'll start by discussing the fundamentals of software testing, starting with how to gather and write functional requirements. Then, we'll introduce the [`MiniTest`](https://github.com/minitest/minitest) gem to write our first unit tests.

## The Importance of Testing
Before diving into specific tools and techniques, it's essential to understand why testing is crucial:

- **Quality Assurance**: Testing helps ensure the software meets the desired quality standards, reducing bugs and enhancing user satisfaction.
- **Reliability**: By catching issues early, testing ensures that the software remains stable and reliable over time.
- **Maintainability**: Well-tested code is easier to maintain and extend because tests provide a safety net for changes.
- **Efficiency**: Automated tests can save time and effort compared to manual testing.

## Gathering Requirements
The first step in any software development process is gathering requirements. This involves understanding what the users and stakeholders need from the software. Requirements can be divided into two categories:

- **Functional Requirements**: Define what the software should do. These are typically written in the form of user stories.
- **Technical Requirements**: Sometimes called "Non-Functional Requirements", define how the software should perform, including aspects like security, usability, and performance.

## Writing Functional Requirements with User Stories
User stories are simple descriptions of a feature told from the perspective of the person who desires the new capability, usually a user or customer of the system. A typical user story format is:

> "As a [role], I want to be able to [capability], so that [benefit]."

### Example User Story
"As a user of a calculator application, I want to be able to add two numbers, so that I can see the sum."

User stories are the foundation for writing tests because they describe the expected behavior of the software from the user's perspective.

<!-- TODO: add example functional spec with user stories for the calculator cli app -->
### Example Functional Requirements Document

```md
# Calculator CLI Functional Specification
The Calculator CLI app provides users with a simple, command-line interface to perform basic arithmetic operations.

## User Stories

### Basic Operations
- As a user, I want to add two numbers, so that I can calculate their sum.
- As a user, I want to subtract one number from another, so that I can calculate the difference.


### Continuous Operations
- As a user, I want to perform multiple calculations without restarting the application, so that I can use the calculator efficiently.

### Functional Requirements
- The calculator must prompt the user for an operation (addition and subtraction).
- The calculator must prompt the user for two numbers to perform the operation on.
- The calculator must display the result of the operation.
- The calculator must handle invalid input gracefully (e.g., non-numeric input).
- The calculator must allow the user to perform another calculation after one completes.
```

## What is Unit Testing?
Unit testing involves writing automated tests for small, isolated parts of your application, typically individual methods or functions. These tests validate that your code behaves as expected under various conditions. You know all those tests you've been running to get full credit on the Ruby assignments? Those are unit tests in action!

## Why MiniTest?
[`MiniTest`](https://github.com/minitest/minitest) is a simple yet powerful testing framework that comes bundled with Ruby. It's great for beginners due to its straightforward syntax and minimal setup.

## Setting Up a MiniTest Project
- Create a new directory for your project. You may want to create a new repository from the [Ruby Sandbox](https://github.com/new?template_name=ruby-sandbox&template_owner=appdev-projects) named something like `minitest-calculator` and open up a codespace.
- Inside this directory, create two files: `calculator.rb` (our code) and `tests/test_calculator.rb` (our tests). It's a standard practice to keep your test files organized inside a `tests` directory.

## Writing Our First Ruby Class
Let's start by writing a simple Ruby class in `calculator.rb`:

```ruby
# calculator.rb

class Calculator
  def add(a, b)
    a + b
  end
end

```

## Bringing in the MiniTest gem
Refresh your memory from the [previous lesson where we learned about gems](https://learn.firstdraft.com/lessons/80-ruby-intro-running-real-programs#gems). Before we can start using `minitest` in our codespace, we need to either:

Run this at the bash prompt in your terminal:

```
gem install minitest
```

_or_, the better idea is to create a new `Gemfile` in your file explorer, and fill it with:

<aside>

As an alternative to manually creating the `Gemfile`, try to run the command `bundle init` in your terminal at the bash prompt. This command will create a new `Gemfile` and add the `source` line at the top to avoid any typos!
</aside>

```rb
# Gemfile

source "https://rubygems.org"

gem "minitest"
```

Then, [run `bundle install` at the bash prompt](https://learn.firstdraft.com/lessons/80-ruby-intro-running-real-programs#bundler), which will install the gem and create a `Gemfile.lock` for you to keep track of the gem version!

- Did you add a `Gemfile`, fill it in, run `bundle install`, and make a git commit to take a snapshot of your new `Gemfile.lock`?
- Yes.
  - Great! Carry on then.
- Not yet.
  - Please do so before you proceed.
{: .choose_best #gemfile_for_minitest title="Gemfile for minitest" points="1" answer="1" }

## Writing Tests with MiniTest
Now that we have the gem installed, we'll write tests for our Calculator class in `tests/test_calculator.rb`:

```ruby
# tests/test_calculator.rb

require 'minitest/autorun'
require './calculator'

class TestCalculator < Minitest::Test
  def test_addition
    calculator = Calculator.new
    assert_equal 4, calculator.add(2, 2), "Addition method failed"
  end
end
```

## Understanding the Test Code
- `require 'minitest/autorun'`: This line loads the MiniTest framework, which we `bundle install`ed to make it available in our codespace.
- `require './calculator'`: This line loads our Calculator class.
- `class TestCalculator < Minitest::Test`: We define a test class that inherits from Minitest::Test.
- `def test_addition`: Our first test method. In `MiniTest`, any method that begins with `test_` is automatically run as a test.
- `assert_equal 4, calculator.add(2, 2)`: The assertion. We're checking if the add method returns 4 when given 2 and 2.

## Running the Tests
Run your tests with the following command in your terminal:

```bash
ruby tests/test_calculator.rb
```

You should see output indicating that 1 test has been run and passed.

```bash
Run options: --seed 23211

# Running:

.

Finished in 0.001780s, 561.9101 runs/s, 561.9101 assertions/s.

1 runs, 1 assertions, 0 failures, 0 errors, 0 skips
```

## Expanding Our Tests
Let's add more functionality to our Calculator class and test it:

```ruby
# calculator.rb

class Calculator
  def add(a, b)
    a + b
  end

  def subtract(a, b)
    a - b
  end
end
```

And the corresponding test:

```ruby
# tests/test_calculator.rb

# ... existing code ...

  def test_subtraction
    calculator = Calculator.new
    assert_equal 0, calculator.subtract(2, 2), "Subtraction method failed"
  end
end
```

Run your tests again to see both tests pass.

```bash
Run options: --seed 10737

# Running:

..

Finished in 0.001611s, 1241.2554 runs/s, 1241.2554 assertions/s.

2 runs, 2 assertions, 0 failures, 0 errors, 0 skips
```

Check out the code used in this lesson [here](https://github.com/DPI-WE/calculator-cli)

## Test Driven Development (TDD)
Test Driven Development (TDD) is a software development approach where you write tests before the actual code. This can be a beneficial approach when dealing with highly complex business logic or when refactoring a large codebase to make sure you don't break anything 😅. This approach might be overkill for many small projects or prototypes that are constantly changing.

## Quiz

- What is the purpose of gathering requirements in software development?
- To understand what the users and stakeholders need from the software.
  - Correct! Gathering requirements helps to identify and document the needs and expectations of users and stakeholders.
- To write code that meets all technical specifications.
  - Not quite. Gathering requirements is about understanding needs, not writing code.
- To determine the exact timeline for software development.
  - Not quite. While requirements gathering can influence timelines, its primary purpose is to understand needs and expectations.
{: .choose_best #gathering_requirements_purpose title="Purpose of Gathering Requirements" points="1" answer="1" }

- Which of the following best describes a user story?
- A detailed technical specification document.
  - Not quite. A user story is a simple, non-technical description of a feature from the user's perspective.
- A simple description of a feature from the perspective of the user.
  - Correct! User stories focus on what the user wants to achieve with the software, providing a high-level overview of features.
- A list of all the tasks the development team needs to complete.
  - Not quite. A user story describes desired features, not tasks.
{: .choose_best #user_story_description title="What is a User Story?" points="1" answer="2" }

- Which of the following is a key component of a user story?
- As a [user type], I want [goal], So that [reason].
  - Correct! This format captures the user's needs and the value they expect to gain from the feature.
- If [condition], Then [action].
  - Not quite. This is more like a conditional statement, not a user story.
- Do [task], Then [result].
  - Not quite. This is more like a procedure or task, not a user story.
{: .choose_best #user_story_component title="Components of a User Story" points="1" answer="1" }

- Why is testing important in software development?
- To ensure the software is built quickly.
  - Not quite. While testing can streamline development in the long run, its primary purpose is to ensure quality and reliability.
- To ensure that the software works as expected and meets quality standards.
  - Correct! Testing verifies that the software behaves correctly under various conditions and meets user and stakeholder expectations.
- To make the software more complex.
  - Not quite. Testing aims to ensure quality, not increase complexity.
{: .choose_best #importance_of_testing title="Importance of Testing" points="1" answer="2" }

- Which of the following is a benefit of automated testing?
- It allows tests to be run automatically, saving time and reducing manual effort.
  - Correct! Automated testing helps execute tests quickly and consistently.
- It replaces the need for any manual testing.
  - Not quite. Automated testing complements manual testing but does not entirely replace it.
- It makes writing tests unnecessary.
  - Not quite. Automated testing involves writing tests that are then executed automatically.
{: .choose_best #automated_testing_benefit title="Benefits of Automated Testing" points="1" answer="1" }

- What is the primary purpose of unit testing?
- To test large parts of the application.
  - Not quite. Unit testing focuses on small, isolated parts of an application.
- To validate that individual methods or functions work as expected.
  - Correct! Unit testing ensures that each part of the application behaves correctly under various conditions.
- To test the performance of the application.
  - Not quite. Unit testing is more about functionality than performance.
{: .choose_best #unit_testing_purpose title="Purpose of Unit Testing" points="1" answer="2" }

- Which of the following is a benefit of Test Driven Development (TDD)?
- Ensures the code is written to pass the tests, leading to more robust code.
  - Correct! TDD encourages writing tests first, which helps ensure code is thoroughly tested and meets requirements.
- Makes the code run faster.
  - Not quite. TDD does not directly impact the runtime performance of the code.
- Removes the need for writing any tests after the code is complete.
  - Not quite. TDD involves writing tests first, but it doesn't mean you won't write more tests later.
{: .choose_best #tdd_benefit title="Benefits of TDD" points="1" answer="1" }

- What command do you run to execute your MiniTest tests?
- `ruby tests/test_calculator.rb`
  - Correct! This command runs all tests in the specified file using Ruby's MiniTest framework.
- `minitest tests/test_calculator.rb`
  - Not quite. The correct command is ruby tests/test_calculator.rb.
- `run tests/test_calculator.rb`
  - Not quite. The correct command is ruby tests/test_calculator.rb.
{: .choose_best #run_tests_command title="Running MiniTest Tests" points="1" answer="1" }

## Conclusion
Congratulations! You've just written your first unit tests in Ruby using [`MiniTest`](https://github.com/minitest/minitest). This is just the beginning. As you write more complex Ruby programs, your tests will become an invaluable tool to ensure your code remains correct and maintainable.

---

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }


## Resources
- [Calculator CLI](https://github.com/DPI-WE/calculator-cli)
