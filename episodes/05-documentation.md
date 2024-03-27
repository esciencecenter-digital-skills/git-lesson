---
title: Document your research software
teaching: 25
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand the importance of writing code documentation together with the source code
- Know what makes a good documentation
- Learn what tools can be used for writing documentation
- Be able to motivate a balanced decision: sometimes READMEs are absolutely enough

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What can I do to make my code more easily understandable?
- What information should go into comments?
- What are docstrings and what information should go into docstrings?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Why we teach this lesson

Everyone should document their code, even if they're working alone.

These are the main points:
- Code documentation has to be versionnable and branchable
- Code documentation should be tracked together with the source code
- README is often enough

**Please do not skim over the two above points**. Please take few minutes to
explain why documentation (sources) should be tracked together with the source
code.  Please discuss this aspect with workshop participants and connect it to
**reproducibility**. This is for me (Radovan) the most important take-home
message.

Specific motivations:

- Code documentation becomes quickly unmanageable if not part of the source code.
- It helps people to quickly use your code thus reducing the time spent to explain over and again to new users.
- It helps people to collaborate.
- It improves the design of your code.

:::::::::::::::::::::::::::::::::::::::::  callout

## In-code documentation

Above we used

Comments, function docstrings
- Advantages
- Good for programmers
- Version controlled alongside code
- Can be used to auto-generate documentation for functions/classes
- Disadvantage
- Probably not enough for users of the code


::::::::::::::::::::::::::::::::::::::::::::::::::

Other topic

:::::::::::::::::::::::::::::::::::::::::  callout

## README files

If you read the output of `git status` carefully,
you'll see that it includes this hint:

```output
(use "git checkout -- <file>..." to discard changes in working directory)
```

As it says,
`git checkout` without a version identifier restores files to the state saved in `HEAD`.
The double dash `--` is needed to separate the names of the files being recovered
from the command itself:
without it,
Git would try to use the name of the file as the commit identifier.

::::::::::::::::::::::::::::::::::::::::::::::::::

In this episode we will learn how to write good documentation inside your code.

:::::::::::::::::::::::::::::::::::::::  challenge

## Writing good comments - In-code-1: Comments

Let's take a look at two example comments (comments in Python start with `#`):

**Comment A**

```python
  # now we check if temperature is below -50
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Comment B**

```python
  # we regard temperatures below -50 degrees as measurement errors
  if temperature < -50:
      print("ERROR: temperature is too low")
```

**Which of these comments is more useful? Can you explain why?**

:::::::::::::::  solution

## Solution

+ **Comment A** describes **what** happens in this piece of code. This can be
    useful for somebody who has never seen Python or a program, but for somebody
    who has, it can feel like a redundant commentary.
+ **Comment B** is probably more useful as it describes **why** this piece of code
    is there, i.e. its **purpose**.

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::
## Sometimes version control is better than a comment

:::::::::::::::::::::::::::::::::::::::  challenge

## Examples for code comments where Git is a better solution

**Keeping zombie code** "just in case" (rather use version control):

```python
  # do not run this code!
  # if temperature > 0:
  #     print("It is warm")
```
  Instead: Remove the code, you can always find it back in a previous version of your code in Git.

**Emulating version control**:

```python
  # John Doe: threshold changed from 0 to 15 on August 5, 2013
  if temperature > 15:
      print("It is warm")
```
Instead: You can get this information from `git log` or `git show` or `git annotate` or similar.

::::::::::::::::::::::::::::::::::::::::::::::::::

## What are "docstrings" and how can they be useful?

Here is function `fahrenheit_to_celsius` which converts temperature in
Fahrenheit to Celsius, implemented in a couple of different languages.
Your language is missing? Please contribute an example.

The first set of examples uses **regular comments**:

::::::::::::::: spoiler

### Python

```py
# This function converts a temperature in Fahrenheit to Celsius.
def fahrenheit_to_celsius(temp_f: float) -> float:
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### R

```r
# Convert Fahrenheit to Celsius
fahrenheit_to_celsius <- function(temp_f)
{
  temp_c <- (temp_f - 32.0) * (5.0/9.0)
  temp_c
}
```

::::::::::::::::::::::::


:::::::::::::::: spoiler

### Julia

```julia
# This function converts a temperature in Fahrenheit to Celsius.
function fahrenheit_to_celsius(temp_f)
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
end
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### Fortran

```fortran
! Convert Fahrenheit to Celsius
function fahrenheit_to_celsius(temp_f) result(temp_c)
    implicit none
    real temp_f
    real temp_c
    temp_c = (temp_f - 32.0) * (5.0/9.0)
end function
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### Rust

```rust
// Convert Fahrenheit to Celsius
fn fahrenheit_to_celsius(temp_f: f64) -> f64 {
    let temp_c = (temp_f - 32.0) * 5.0 / 9.0
    temp_c
}
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### C++

```c++
// Converts a temperature in Fahrenheit to Celsius
double fahrenheit_to_celsius(double temp_f) {
    auto temp_c = (temp_f - 32.0) * (5.0 / 9.0);
    return temp_c;
}
```

::::::::::::::::::::::::

The second set uses **docstrings or similar concepts**. Please compare the two
(above and below):

::::::::::::::: spoiler

### Python

```py
def fahrenheit_to_celsius(temp_f: float) -> float:
    """
    Converts a temperature in Fahrenheit to Celsius.

    Parameters
    ----------
    temp_f : float
        The temperature in Fahrenheit.

    Returns
    -------
    float
        The temperature in Celsius.
    """

    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### R

```r
#' Convert Fahrenheit to Celsius
#'
#' @param temp_f A numeric vector of temperatures in Fahrenheit.
#' @return A numeric vector of temperatures in Celsius.
fahrenheit_to_celsius <- function(temp_f)
{
  temp_c <- (temp_f - 32.0) * (5.0/9.0)
  temp_c
}
```

::::::::::::::::::::::::


:::::::::::::::: spoiler

### Julia

```julia
"""
    fahrenheit_to_celsius(temp_f::Float)

Converts temperature in Fahrenheit to Celsius.

# Arguments
- `temp_f::Float`: Temperature in Fahrenheit.

# Returns
- `temp_c::Float`: Temperature in Celsius.
"""
function fahrenheit_to_celsius(temp_f)
    temp_c = (temp_f - 32.0) * (5.0/9.0)
    return temp_c
end
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### Fortran

```fortran
!> @brief Convert Fahrenheit to Celsius
!! @param temp_f Temperature in Fahrenheit
!! @return Temperature in Celsius
function fahrenheit_to_celsius(temp_f) result(temp_c)
    implicit none
    real temp_f
    real temp_c
    temp_c = (temp_f - 32.0) * (5.0/9.0)
end function
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### Rust

```rust
/// Convert Fahrenheit to Celsius
/// # Arguments
/// * `temp_f` - Temperature in Fahrenheit
///
/// # Returns
/// * `temp_c` - Temperature in Celsius
fn fahrenheit_to_celsius(temp_f: f64) -> f64 {
    let temp_c = (temp_f - 32.0) * 5.0 / 9.0
    temp_c
}
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### C++

```c++
// @brief: Converts a temperature in Fahrenheit to Celsius
//
// @param: temp_f: Temperature in Fahrenheit
//
// @return: Temperature in Celsius
double fahrenheit_to_celsius(double temp_f) {
    auto temp_c = (temp_f - 32.0) * (5.0 / 9.0);
    return temp_c;
}
```

::::::::::::::::::::::::

Docstrings can do a bit more than just comments:
- Tools can generate help text automatically from the docstrings.
- Tools can generate documentation pages automatically from code.

It is common to write docstrings for functions, classes, and modules.

Good docstrings describe:
- What the function does
- What goes in (including the type of the input variables)
- What goes out (including the return type)

**Naming is documentation**:
Giving explicit, descriptive names to your code segments (functions, classes,
variables) already provides very useful and important documentation. In
practice you will find that for simple functions it is unnecessary to add a
docstring when the function name and variable names already give enough
information.



:::::::::::::::::::::::::::::::::::::::: keypoints

- Comments should describe the why for your code not the what.
- Writing docstrings can be a good way to write documentation while you type
  code since it also makes it possible
  to query that information from outside the code or to auto-generate
  documentation pages.

::::::::::::::::::::::::::::::::::::::::::::::::::


