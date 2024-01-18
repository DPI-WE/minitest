# Testing your code with [`MiniTest`](https://github.com/minitest/minitest)

Testing is a critical skill in software development. It helps ensure your code works as expected and remains reliable as it evolves. In this lesson, we'll introduce [`MiniTest`](https://github.com/minitest/minitest), a testing framework incldued with Ruby, to write our first unit tests.

## What is Unit Testing?
Unit testing involves writing automated tests for small, isolated parts of your application, typically individual methods or functions. These tests validate that your code behaves as expected under various conditions.

## Why [`MiniTest`](https://github.com/minitest/minitest)?
[`MiniTest`](https://github.com/minitest/minitest) is a simple yet powerful testing framework that comes bundled with Ruby. It's great for beginners due to its straightforward syntax and minimal setup.

## Setting Up a [`MiniTest`](https://github.com/minitest/minitest) Project
- Create a new directory for your project.
- Inside this directory, create two files: `calculator.rb` (our code) and `tests/test_calculator.rb` (our tests).

## Writing Our First Ruby Class
Let's start by writing a simple Ruby class in calculator.rb:

```ruby
# calculator.rb

class Calculator
  def add(a, b)
    a + b
  end
end

```

## Writing Tests with [`MiniTest`](https://github.com/minitest/minitest)
Now, we'll write tests for our Calculator class in test_calculator.rb:

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
- `require 'minitest/autorun'`: This line loads the MiniTest framework.
- `require './calculator'`: This line loads our Calculator class.
- `class TestCalculator < Minitest::Test`: We define a test class that inherits from Minitest::Test.
- `def test_addition`: Our first test method. In `MiniTest`, any method that begins with `test_` is automatically run as a test.
- `assert_equal 4, calculator.add(2, 2)`: The assertion. We're checking if the add method returns 4 when given 2 and 2.

## Running the Tests
Run your tests with the following command in your terminal:

```bash
ruby test_calculator.rb
```

You should see output indicating that 1 test has been run and passed.

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

## Resources


## Conclusion
Congratulations! You've just written your first unit tests in Ruby using MiniTest. This is just the beginning. As you write more complex Ruby programs, your tests will become an invaluable tool to ensure your code remains correct and maintainable.

Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }
