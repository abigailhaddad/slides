# Improving Your Code with Functions in Python and R: What to Do and How Large Language Models Can Help

- [Improving Your Code with Functions in Python and R](#improving-your-code-with-functions-in-python-and-r)
  * [Introduction](#introduction)
  * [Benefits of Using Functions](#benefits-of-using-functions)
  * [Structuring a Function](#structuring-a-function)
  * [Avoiding Multiple Levels of Indentation and Long Functions](#avoiding-multiple-levels-of-indentation-and-long-functions)
    + [Tips for reducing indentation levels:](#tips-for-reducing-indentation-levels)
    + [Tips for avoiding long functions:](#tips-for-avoiding-long-functions)
  * [Documenting a Function](#documenting-a-function)
  * [Structuring a Program with a Main Function](#structuring-a-program-with-a-main-function)
  * [Unit Testing with Functions](#unit-testing-with-functions)
  * [Effectively Using GPT to Restructure Code and Follow Best Practices Around Functions](#effectively-using-large-language-models)
  * [Conclusion](#conclusion)


## Introduction

Functions are pieces of code that take inputs and return outputs, much like mathematical functions. If you're coming from a more procedural programming background, where you think of code as a series of steps executed in a sequence, using functions in Python and R may represent a significant conceptual shift. However, many of the benefits of these languages come from adopting this approach, which emphasizes modularity, reusability, and readability. In this guide, we will discuss how using functions can improve your code in Python and R. 

At the end, we'll also discuss using Large Language Models like GPT to help you adopt these practices.

## Benefits of Using Functions

1. **Easier to understand**: Functions allow you to break your code into smaller, more manageable pieces. This makes it easier for you (and others) to understand what your code is doing.
2. **Avoiding side effects**: A side effect is when a function changes something you didn't mean for it to change. This can make code hard to reason about and introduce bugs. By using functions that only depend on their inputs and only modify the variables that you're returning explicitly as outputs, you can avoid side effects and make your code more predictable.
3. **Modularity**: Functions let you organize your code into modular pieces. This means that you can easily rearrange or reuse parts of your code without affecting the rest of the program.
4. **Reusability**: Well-written functions can be easily reused in other parts of your code or even in other projects, saving time and ensuring consistent results. It also means that if you modify how a function works - for instance, replacing a loop with list comprehension in Python - you only need to change it in one place, not every place you're calling it. 

Even if your code is relatively simple, using functions can still provide these benefits, making it easier to maintain and extend your code in the future. If you've ever looked at your code a year (or a week) later and not been able to remember exactly what it did or why, functions are one of several coding practices that can significantly assist with that.

## Structuring a Function

In both Python and R, a function is defined by a name, a set of input parameters, and a return statement to provide the output. The general structure is as follows:

Python:
```python
def function_name(input1, input2, ...):
    # Function logic here
    return output
```

R: 
```r
function_name <- function(input1, input2, ...) {
    # Function logic here
    return(output)
}
```
To write a clear and readable function, follow these guidelines:

1. Keep functions small and focused on a single task.
2. Use descriptive names for functions and variables.
3. Make use of comments to explain the purpose of the function and any complex logic.

## Avoiding Multiple Levels of Indentation and Long Functions

When writing code, it's important to avoid creating functions with multiple levels of indentation, such as nested loops or complex if-else statements. Deeply nested code can be challenging to read and understand, making it more difficult to maintain and debug. The same is true for very long functions. There are no hard-and-fast rules for what is too many levels of indentation or a too-long function, and to some extent these are context-dependent, but these are things to keep in mind. 

### Tips for reducing indentation levels:

1. **Refactor nested loops into separate functions**: If you find yourself using nested loops or deeply nested if-else statements, consider breaking the inner loops or conditional blocks into separate functions. This approach makes the code more modular and easier to understand.

   ```python
   # Instead of this
   def process_data(data):
       for item in data:
           for attribute in item:
               # Perform some operation
   
   # Do this
   def process_attribute(attribute):
       # Perform some operation

   def process_data(data):
       for item in data:
           for attribute in item:
               process_attribute(attribute)
   ```
2. **Use list comprehensions or generator expressions:** In Python, you can often replace nested loops with list comprehensions or generator expressions, which provide a more concise and readable way to iterate over collections.

  ```python
  # Instead of this
  squares = []
  for number in numbers:
    squares.append(number ** 2)

  # Do this
  squares = [number ** 2 for number in numbers]
  ```
  
### Tips for avoiding long functions:

1. **Divide and conquer:** If a function is doing too much, consider splitting it into smaller, more focused functions. Each function should have a single responsibility, making it easier to understand and test.
3. **Leverage dictionaries, lists, or tables for efficient data transformation:** When dealing with complex data transformations, such as mapping one set of values to another, it's more efficient to use an object like a list in R or a dictionary in Python rather than lengthy if/then statements. Create a separate function that returns a mapping object (list or dictionary) representing the relationship between the values. Then, use this function and apply the mapping to the relevant column in your data frame or table. This approach simplifies the code, making it more readable and maintainable.

By following these best practices, you'll create code that's more readable, maintainable, and easier to debug, ultimately leading to higher-quality programs.


## Documenting a Function

Properly documenting your functions makes it easier for others to understand and use your code. Here's how to document a function in Python and R:

Python (docstrings):
```python
def add_numbers(a, b):
    """
    Add two numbers and return the result.

    Parameters:
    a (int): The first number
    b (int): The second number

    Returns:
    int: The sum of a and b
    """
    return a + b
```

R (roxygen2):
```r
#' Add two numbers and return the result
#'
#' @param a The first number
#' @param b The second number
#' @return The sum of a and b
#' @examples
#' add_numbers(1, 2)
add_numbers <- function(a, b) {
    return(a + b)
}
```

## Structuring a Program with a Main Function

Wrapping smaller functions within a main function makes it easier to manage, run, and import into other programs, as well as shows you what the overall inputs and outputs are for your code. Here's an example of how to do this in Python and R:

Python:
```python
def read_data(file_path):
    # Code to read data from a file
    pass

def process_data(data):
    # Code to process the data
    pass

def save_data(data, output_path):
    # Code to save processed data to a file
    pass

def main(input_file, output_file):
    data = read_data(input_file)
    processed_data = process_data(data)
    save_data(processed_data, output_file)

if __name__ == '__main__':
    main('input.txt', 'output.txt')
```

R:
```R
read_data <- function(file_path) {
    # Code to read data from a file
    return(data)
}

process_data <- function(data) {
    # Code to process the data
    return(processed_data)
}

save_data <- function(data, output_path) {
    # Code to save processed data to a file
}

main <- function(input_file, output_file) {
    data <- read_data(input_file)
    processed_data <- process_data(data)
    save_data(processed_data, output_file)
}

main('input.txt', 'output.txt')
```

## Unit Testing with Functions

Writing code using functions also enables you to perform unit tests. Unit testing is a method of testing individual pieces (units) of code, usually functions or methods, to ensure that they work as expected. By using functions, you can isolate specific parts of your code and test their behavior under various conditions.

When you write functions, you can test each one independently, making it easier to identify and fix errors. Additionally, unit tests serve as documentation, demonstrating how your functions are intended to be used and what behavior to expect.

There are several testing frameworks available for Python and R that make unit testing more manageable:

- For Python, the built-in `unittest` module or the popular `pytest` library can be used.
- In R, the `testthat` package is widely used for unit testing.

Here's an example of how you might write a unit test for a simple function in Python using `pytest`:

```python
# your_module.py

def add(a, b):
    return a + b

# test_your_module.py

import pytest
from your_module import add

def test_add():
    assert add(1, 2) == 3
    assert add(-1, 1) == 0
    assert add(0, 0) == 0
```

By incorporating unit tests into your development process, you can create code that's more reliable, maintainable, and easier to understand. While these aren't likely to be part of your coding process for all of the code you write, they're a nice tool to have available, especially if you want to share your code in the form of a package or module for others to use. 

### Effectively Using Large Language Models

Large Language models can be a big help with restructuring your code and following best practices. GPT or the Generative Pre-trained Transformer, is one of these models. Bard, from Google, is another one. 

The available tools and versions are changing rapidly, but here are some of the kinds of tasks you can ask for help with:

1. **General code improvements if you're not sure what you want**. You can ask GPT to help you reorganize your code to be more efficient, more readable, to use best practices, etc. I've tried asking it write R code like it's [Hadley Wickham](https://en.wikipedia.org/wiki/Hadley_Wickham) or Python code like [Brett Slatkin](https://research.google/people/BrettSlatkin/); I don't know that this is more effective than just asking it to write good code, but I've definitely gotten different responses from it.
2. **Specific code improvements if you do know what you want.** You can ask it to help you break up bigger functions into smaller ones. You can ask it for help refactoring loops, or putting all of your functions in a main function.
3. **Writing function-level documentation**: It can read your code and make guesses about what your functions are doing and what format the inputs and outputs are in.
4. **Writing test cases**: It can read your code and generate test cases.

This doesn't obviate the need to review what it's writing for you and understand each line -- and you can also ask it to explain each change it's making if you don't understand something.

It also gets things wrong! I asked it to help with restructuring so that I had fewer levels of indentation and it not did -- but when I give it more explicit, detailed instructions like "help me break these lines into their own function and use 'apply'", or "write a list comprehension for this loop", it's more likely to get it correct. 

But even with these limitations, I've found this to be a huge help, particularly in terms of 'best practices'-type tasks like documentation and test cases that I might otherwise not get to, especially when I'm first coding something.

## Conclusion

User-defined functions form the foundation of Python and R, offering a significant advantage when writing code in these languages. While there is an initial learning curve when adopting this approach, especially if you come from a more procedural programming background, the benefits are really significant. When you look back on code you've written in the past, code that's structured this way is code you're more 
understand and be able to reuse. 

If you'd like to learn more about using functions effectively in Python and R, consider exploring the following resources:

1. Python:
    - [Python documentation on functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
    - [Real Python: Defining Your Own Python Function](https://realpython.com/defining-your-own-python-function/)

2. R:
    - [R documentation on functions](https://cran.r-project.org/doc/manuals/r-release/R-intro.html#Writing-your-own-functions)
    - [R for Data Science: Functions](https://r4ds.had.co.nz/functions.html)
