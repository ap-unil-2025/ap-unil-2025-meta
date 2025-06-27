---
marp: true
theme: default
paginate: true
header: "Session 7: Trusting Your Code"
footer: "An Introduction to Automated Testing with `pytest`"
size: 16:9

class:
  - lead
  - invert
---

<!-- _class: lead -->

# Session 7: Trusting Your Code

**An Introduction to Automated Testing with `pytest`**

---

# Today's Goals

*   Understand **why** we need to write tests for our code.
*   Learn the difference between **manual** and **automated** testing.
*   Get introduced to `pytest`, the standard Python testing framework.
*   Write our first simple tests for our "Companion Project".
*   Learn how to test for expected failures (exceptions).

---
<!-- _class: invert -->

# Part 1: Why Test?

---

# The Problem: How Do You Know Your Code Works?

So far, we've been testing our code **manually**:
1.  Write a function.
2.  Run the script.
3.  Look at the `print()` output.
4.  Decide if it "looks right".

**What's wrong with this?**
*   **It's slow and repetitive.** You have to do it every time you make a change.
*   **It's error-prone.** You might forget to test a specific case.
*   **It doesn't scale.** What if you have 50 functions? You can't manually check all of them after every single change.

---

# The Solution: Automated Testing

**Automated Testing** is the practice of writing code to test your other code.

You create a "test suite"—a collection of test functions that:
1.  Run a piece of your code with a specific input.
2.  **Assert** that the output is exactly what you expect.
3.  Are run automatically every time you want to verify your project.

**This gives you a "safety net".** When you change something, you can run your tests and be confident you didn't break anything.

---
<!-- _class: invert -->

# Part 2: Your First Tests with `pytest`

---

# Introducing `pytest`

`pytest` is a powerful, yet simple, testing framework for Python.

**Why `pytest`?**
*   **Simple Syntax:** Writing tests feels very natural.
*   **Powerful Features:** Easily handles complex testing scenarios.
*   **Great Reporting:** Gives you clear, readable output when tests fail.
*   **Auto-discovery:** It automatically finds your test files and functions.

---

# Setting Up for Testing

Let's get our companion project ready for testing.

1.  **Install `pytest` as a dev dependency:**
    ```bash
    uv pip install --dev pytest
    ```

2.  **Create a `tests/` directory:**
    By convention, all test files live in a separate `tests/` directory at the root of your project.
    ```bash
    mkdir tests
    ```

---

# The Anatomy of a `pytest` Test

`pytest` follows simple conventions for discovering tests:

1.  Test filenames must start or end with `test_`.
    *   Good: `test_analyzer.py`, `analyzer_test.py`
2.  Test function names must start with `test_`.
    *   Good: `def test_word_count(): ...`

Inside a test function, you use the plain `assert` keyword to check for correctness.

---

# Let's Code: Writing Our First Test

**Goal:** Write a test for the `count_words` method in our `TextAnalyzer` class.

**Open a new file: `tests/test_analyzer.py`**

```python
# tests/test_analyzer.py

# We need to import the class we want to test
from src.text_analyzer import TextAnalyzer

def test_word_count_simple_case():
    """
    Tests the word_count method with a simple sentence.
    """
    # 1. SETUP: Create an instance with known data
    analyzer = TextAnalyzer("hello world")

    # 2. EXECUTION: Call the method we want to test
    result = analyzer.count_words()

    # 3. ASSERTION: Check if the result is what we expect
    assert result == 2
```

---

# Running Your Tests

This is the easy part! Navigate to the root directory of your project in the terminal and simply run:

```bash
uv run pytest
```

`pytest` will automatically find your `tests/` directory, find the `test_analyzer.py` file, find the `test_word_count_simple_case` function, run it, and report the results.

**If everything passes, you'll see a green output!**

---

# What Happens When a Test Fails?

Let's write a test we know will fail to see `pytest`'s excellent error reporting.

```python
# In tests/test_analyzer.py

def test_word_count_with_empty_string():
    analyzer = TextAnalyzer("")
    result = analyzer.count_words()
    # This assertion is wrong on purpose!
    assert result == 1
```

Now run `uv run pytest` again. `pytest` will give you a detailed **red** report showing:
*   Which test failed.
*   Which `assert` statement failed.
*   The values of the variables at the time of failure (e.g., `assert 0 == 1`).

This makes debugging a failed test incredibly easy.

---
<!-- _class: invert -->

# Part 3: More Advanced Testing Scenarios

---

# Testing for Expected Errors

What if you have a function that is *supposed* to raise an error? For example, our `calculate_mean` method should raise a `ValueError` if there are no results.

How do you test that the error was correctly raised? With `pytest.raises`.

---

# Let's Code: Testing for a `ValueError`

**Goal:** Ensure our `calculate_mean` method correctly raises a `ValueError` when the results list is empty.

```python
# tests/test_analyzer.py
import pytest # Need to import pytest for this

from src.text_analyzer import TextAnalyzer

# ... other tests ...

def test_calculate_mean_raises_error_on_empty_results():
    """
    Tests that calculate_mean raises a ValueError for an empty dataset.
    """
    # Create an analyzer with no results added
    analyzer = TextAnalyzer("some text but no results yet")
    
    # Use a context manager to say "I expect an error inside this block"
    with pytest.raises(ValueError):
        # This line SHOULD raise a ValueError.
        # If it does, the test passes. If it doesn't, the test fails.
        analyzer.calculate_mean()
```

---

# The "Arrange, Act, Assert" Pattern

Good tests are easy to read and follow a standard pattern:

1.  **Arrange**: Set up all the necessary preconditions and inputs. Create your objects, prepare your data.
    *   `analyzer = TextAnalyzer("hello world")`

2.  **Act**: Execute the single piece of code (the method or function) that you are testing.
    *   `result = analyzer.count_words()`

3.  **Assert**: Check that the outcome of the "Act" phase is what you expected.
    *   `assert result == 2`

Structuring your tests this way makes them much clearer and more maintainable.

---

<!-- _class: lead -->

# Session 7 Recap

*   **Automated testing** provides a "safety net" that allows you to change your code with confidence.
*   **`pytest`** is the standard tool for writing simple and powerful tests in Python.
*   Tests are functions that start with `test_` in files named `test_*.py`.
*   The `assert` keyword is used to check if a condition is true.
*   Use `pytest.raises` to test that your code correctly raises exceptions when it should.
*   Writing tests is a fundamental part of writing professional, reliable software for your research.