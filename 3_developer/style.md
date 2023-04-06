# Style Guidance

To ensure the consistency and readability of the code throughout this repository, we have established basic guidelines and standards for developers.
This includes recommendations for coding style, naming conventions, and comment. Contributors to this repository are expected to review and adhere to these guidelines.

## Coding Style

The code in this repository is written in Python and follows the [PEP8](https://www.python.org/dev/peps/pep-0008/) coding style guidelines.
We recommend using the `black` formatter, which strictly adheres to the PEP8 rules when formatting code.
More information about `black` is available on its [official website](https://black.readthedocs.io/en/stable/index.html).

To install `black`, run the command `pip install black`.
Integrated development environments such as Visual Studio Code or JetBrains PyCharm generally support formatting code with `black`.
In the case of Visual Studio Code, add the following code to the configuration file `settings.json`, enabling `black` to be used as the default code formatter with hotkey `Shift+Alt+F`.

```json
"python.formatting.provider": "black",
"python.formatting.blackArgs": [
    "-S"
]
```

Note that in this repository, single quotes are used exclusively for strings (`'str'` or `'''str'''`)!!!
Since `black` defaults to using double quotes, the `-S` or `--skip-string-normalization` argument should be used to prevent automatic conversion of single quotes to double quotes.

## Naming Conventions

Common names for variables and functions include:

- `b`: single lowercase letter
- `B`: single uppercase letter
- `lowercase`: lowercase words without underscores
- `lower_case_with_underscores`: lowercase words separated by underscores
- `UPPERCASE`: uppercase words without underscores
- `UPPER_CASE_WITH_UNDERSCORES`: uppercase words separated by underscores
- `CapitalizedWords` (or `CapWords`, or `CamelCase`): capitalized words without underscores, with the first letter of each new word capitalized
- `mixedCase`: similar to `CamelCase`, but with the first letter lowercased

In general, this repository follows the convention of using **underscores** to separate words in variable and function names:

- Lowercase words with underscores (e.g. `load_data()`, `simulation_results`) are used for variable and function names.
- Class names are written using CamelCase (e.g. `AbstractClass`), with a maximum of two words.
- Constants are written in ALL_CAPS separated by underscores (e.g. `MAX_SIZE`).

In summary, names should be short, descriptive, and easy to understand.
In some cases, other naming conventions such as `CamelCase` or abbreviated names might be accepted for compatibility with third-party libraries.

## Comments and DocStrings

Comments are a key element of code readability, helping to reduce the difficulty of reading code for other users and improving the efficiency of code editing, modification, and debugging.
Therefore, it is important to add comments at appropriate locations throughout the code, using both block and inline comments.
Note that never describe the code. Assume the person reading the code knows Python (though not what you're trying to do) better than you do.

```python
# We use a weighted dictionary search to find out where i is in
# the array. We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:  # True if i is 0 or a power of 2.

```

Python has built-in support for DocStrings, which can be used for classes, functions, modules, and packages.
DocStrings can be accessed using the `__doc__` attribute.
The commenting and DocString conventions used in this repository are based on the [Google Style Guide](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings).
Users can refer to this guide for more specific details.

A simple example of a function DocString is shown below:

```python
def plus(a: int, b: int = 0) -> int:
    '''
    Summary description of this function.

    Detailed description of this function.
    Its functionality or purpose should be explained comprehensively and explicitly.
    The content should also be consistent with its corresponding API document.

    Args:
        a: int. Description of the `a` parameter.
        b: int, optional. Description of the `b` parameter.

    Returns:
        Describes the type of the return value and its semantics. This section can be omitted if the function only returns None, or if the docstring starts with "Returns" or "Yields", and the opening sentence is sufficient to describe the return value.

    Raises:
        List of exceptions that may be raised.
    '''

    # The main function code goes here
    return a + b

```

## Copyright Notice

A copyright notice should be placed at the top of each file, as shown in the example below, providing information about the encoding format used in the file and a copyright statement.

```python
# -*- coding: utf-8 -*-
# Copyright (C) rflylab from School of Automation Science and Electrical Engineering, Beihang University.
# All Rights Reserved.

# Insert code below

```
