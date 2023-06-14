# `template_of_document`

This is a template for developers to write a document for their user-defined function, which is important and useful for beginners to learn how to call the function.
The work might be boring and dull but significant at the same time.

Some basic rules are listed in this file, including the use of words, phrases, syntax, etc.
Hope that it can assist you to write a formal, neat, and easy-to-understand document that is also consistent with ours.

**Please note that there are just some suggestions rather than laws or regulations. To make yourself understood by other users is always the first thing that you need to concern about.**

Please be free to @[CuiiGen](https://github.com/CuiiGen) if you have any questions.
It's quite a pleasure for us to have you.

## Syntax

Different ways to call the function should be listed as follows.

```python
function_name(arg1)
function_name(arg1, arg2)
function_name(arg1, arg2, **kwargs)
```

## Description

Here comes the main part of this file.
Detailed descriptions of the function should be introduced.
Differences between the various ways to call the function should also be explained.

### Verbs

To maintain the consistency of all the documents, the following verbs should be used as much as possible.

|       Verb        | Example                                                                           | Comment                                                                                 |
| :---------------: | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
|      return       | `len()` returns the length of an array or list.                                   |                                                                                         |
| compute/calculate | `inv(X)` computes the inverse of square matrix `X`.                               | "compute" and "calculate" are almost always interchangeable. So either of them is fine. |
|      specify      | `function(____, method='algorithm')` specifies the algorithm to use in computing. | (be) specified by something / specify variable as something / adjective.                |
|      accept       | `det(A)` accepts a square matrix.                                                 |                                                                                         |

### "argument" or "parameter"

Besides, pay attention to these two terms, "argument" and "parameter", which are often used interchangeably.

- A parameter represents a value that the procedure expects you to pass when you call it. The procedure's declaration defines its parameters.

- An argument represents the value that you pass to a procedure parameter when you call the procedure. The calling code supplies the arguments when it calls the procedure.

More information is available on [argument vs. parameter
](https://learn.microsoft.com/en-us/style-guide/a-z-word-list-term-collections/a/argument-vs-parameter) and [Differences Between Parameters and Arguments (Visual Basic)](https://learn.microsoft.com/en-us/dotnet/visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments).

### Tips about using matrix, vector, array, and list

Here are also some commonly-used terms that may be helpful to you.

- An m-by-n matrix `A`, or an m-by-m square matrix `A`. That is, the shape (not dimension) of the matrix `A` is `(m, n)` or `(m, m)`.
- A vector (array) of length `n`.

By the way, "matrix" and "vector" are often seen in the functions that refer to theorems or equations in Matrix Theory, a branch of mathematics that focuses on the study of matrices.
In other cases, "array" is more common, and "list" is a bit rare.

## Examples

Here is the first example of the user-defined function.
Basic ways to call it should be illustrated.

```python
>>> import numpy as np
>>> from somewhere import function

>>> a, b = 1, 2
>>> c = function(a, b)
>>> print('The result of `function`: 'c)

The result of `function`: 2

```

---

Here is the second example of the user-defined function, if needed.

```python
>>> import numpy as np
>>> from somewhere import function

>>> a, b = 1, 2

>>> c = function(a, b, operator='-')
>>> print('The result of `function`: 'c)

The result of `function`: -1

```

## Input Arguments

Detailed introduction of all the input arguments.

`arg1` —— A summary description, specified as an array, list, float, integer, or other datatypes else.

Detailed descriptions.

---

`arg2` —— A summary description, specified as an array, list, float, integer, or other datatypes else.

Detailed descriptions.

## Output Arguments

Detailed introduction of all the output arguments if needed.

## More About

More information that users need to know or they may want to know.
For example, the detailed derivation of an algorithm or theorem.

It will be great if you'd like to convert this file from `Markdown` to `HTML` to make sure it can be rendered properly online.
The procedure is shown as follows.

1. Download Typora from its [official website](https://typora.io/) and then install it.
1. Download the [theme "Vue"](https://theme.typoraio.cn/theme/Vue/) and install it with the help of this [guide](https://support.typora.io/About-Themes/).
1. Download and install the [Pandoc](https://www.pandoc.org/).
1. Open this file in Typora and then export it in the format of `HTML`.
1. Save it to `/2_tutorial/` and modify `README.md` correspondingly. Attention that you also need to convert the modified `README.md` to the `./docs/index.html`.

## References

Last but not least, all the literature, reports, online websites, or other supporting materials that you referred to should be listed at the end of this file.

[BibTeX bibliography style: IEEEtran](https://www.bibtex.com/s/bibliography-style-ieeetran-ieeetran/) is recommended.
