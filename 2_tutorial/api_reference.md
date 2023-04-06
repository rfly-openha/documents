# API Reference

## Guidelines for importing functions from OpenHA

The OpenHA namespace is almost empty.

Everything in the namespaces of OpenHA submodules is public. In general, it is recommended to import functions from submodule namespaces. For example, the function `acai()` (defined in `OpenHA\assessment\attribute\degree_of_controllablity.py`) should be imported like this:

```python
from OpenHA.assessment.attribute import acai
result = acai(...)
```

This form of importing submodules is preferred for all submodules.

In some cases, the public API is one level deeper. For example, the `OpenHA.assessment.attribute` module is public, and the functions it contains are not available in the `OpenHA.assessment` namespace. Sometimes it may result in more easily understandable code if functions are imported from one level deeper.

## Dependencies

The OpenHA is aimed to be an open source framework to help users from various fields to build their own PHM applications.
However, objectively, the focus of our research is mainly concentrated on multicopters.
Most of the functions included in this package are based on our research achievements, which are appliable for multicopters.
The proposed algorithms or theories have been published and the papers are available on the [official homepage](http://rfly.buaa.edu.cn/index.html#/publications).
That is the best we can do so far.
So you are welcome to join us to develop your new health assessment algorithms for other platforms including multicopters, such as planes, ships, vehicles, etc.

On the other hand, some other excellent packages and open-source projects are depended on by OpenHA to avoid reinventing the wheel.
These packages provide have been optimized by experienced engineers or programmers.
We don't have the reason or motivation to reinvent the wheel since they have provided us with powerful tools to process data.
Some of the most commonly used packages are introduced as follows.

- [NumPy](https://numpy.org/). NumPy is the fundamental package for scientific computing in Python. It contains lots of classes and functions that you may need in scientific computing and it's also the foundation of many other packages. If you don't know it, go to learn it first.
By the way, importing this package in the following way is recommended.

```python
import numpy as np
```

- [SciPy](https://scipy.org/). SciPy is a collection of mathematical algorithms and convenience functions built on the [Numpy](https://numpy.org/) extension of Python. It adds significant power to the interactive Python session by providing the user with high-level commands and classes for manipulating and visualizing data. With SciPy, an interactive Python session becomes a data-processing and system-prototyping environment rivaling systems, such as MATLAB, IDL, Octave, R-Lab, and SciLab.

- [matplotlib](https://matplotlib.org/). Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python. We may develop more top-level functions to make it more convenient to visualize your assessment results in the future.
Anyway, matplotlib is always the first choice if you want to plot a variable in Python.
By the way, it is recommended to use the following magic command to make it interactive in Jupyter Notebook.

```python
%matplotlib widget # or `%matplotlib ipympl` alternatively
import matplotlib.pyplot as plt
```

- [scikit-learn](https://scikit-learn.org/stable/index.html). Scikit-learn is an open source machine learning library that supports supervised and unsupervised learning. It also provides various tools for model fitting, data preprocessing, model selection, model evaluation, and many other utilities.

- [ProgPy](https://nasa.github.io/progpy/index.html). The NASA Prognostics Python Packages (ProgPy) are a set of open-sourced python packages supporting research and development of prognostics and health management tools. They implement architectures and common functionality of prognostics, supporting researchers and practitioners.
ProgPy consists of a set of packages. See the documentation specific to each package for more information.

Once again, if some algorithms are unavailable in the above packages or projects, you are welcome to report an issue in GitHub to let us know, or you can implement it and create a Pull Request.
We will check it as soon as possible.

## API definition

There is a table of all the submodules and functions defined in OpenHA.

All the documentations are available via the links.

1. [OpenHA.core](#openhacore)
1. OpenHA.assessment
   1. [OpenHA.assessment.attribute](#openhaassessmentattribute)
   1. [OpenHA.assessment.system](#openhaassessmentsystem)
1. OpenHA.processing
   1. [OpenHA.processing.feature](#openhaprocessingfeature)
   1. [OpenHA.processing.preprocessing](#openhaprocessingpreprocessing)
1. [OpenHA.prognostics](#openhaprognostics)

### `OpenHA.core`

| functions                             | description                                                                  |
| ------------------------------------- | ---------------------------------------------------------------------------- |
| [get_interval](./get_interval.html)   |                                                                              |
| [load_ANN](./load_ANN.html)           | Loads an object saved with `torch.save()` or `tf.train.Saver()` from a file. |
| [split_dataset](./split_dataset.html) | Split the dataset into train and test subsets randomly.                      |

### `OpenHA.assessment.attribute`

| functions                                                               | description                                                                                                                                    |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [acai](./acai.html)                                                     | Computes the degree of controllability (DOC) based on the Availability Control Authority Index, namely ACAI, which is proposed by Guang-Xu Du. |
| [control_allocation](./control_allocation.html)                         | Returns the control allocation matrix of a multicopter.                                                                                        |
| [doc_disturbance_rejection_kang](./doc_disturbance_rejection_kang.html) | Compute the new measure representing degree of controllability for disturbance rejection.                                                      |
| [doc_gramian](./doc_gramian.html)                                       | Compute the Gramian-matrix-based DOC.                                                                                                          |
| [doc_recovery_region](./doc_recovery_region.html)                       | Computes the DOC based on the recovery region.                                                                                                 |
| [profust_reliability](./profust_reliability.html)                       | Compute the profust reliability according to the research by Zhiyao Zhao.                                                                      |
| [trapezoidal_membership_func](./trapezoidal_membership_func.html)       | Returns the degree of membership of the state `x` to a set, whose membership function is trapezoidal                                           |

### `OpenHA.assessment.system`

| functions                                                           | description                                                                      |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [analytical_hierarchy_process](./analytical_hierarchy_process.html) | Computes the weight of each element according to pairwise comparison matrix `A`. |
| [gate_and](./gate_and.html)                                         | Calculates probability of an "AND" gate.                                         |
| [gate_not](./gate_not.html)                                         | Calculates probability of a "NOT" gate.                                          |
| [gate_or](./gate_or.html)                                           | Calculates probability of an "OR" gate.                                          |
| [gate_xor](./gate_xor.html)                                         | Calculates probability of a "XOR" gate.                                          |
| [sum_by_weight](./sum_by_weight.html)                               | Calculates the weighted sum.                                                     |

### `OpenHA.processing.feature`

| functions                                                 | description                             |
| --------------------------------------------------------- | --------------------------------------- |
| [average_rectified_value](./average_rectified_value.html) | Calculates the average rectified value. |
| [central_moment](./central_moment.html)                   | Calculates the k-th central moment.     |
| [kurtosis](./kurtosis.html)                               | Compute the kurtosis.                   |
| [raw_moment](./raw_moment.html)                           | Calculates the k-th raw moment.         |
| [skewness](./skewness.html)                               | Compute the skewness.                   |
| [variance](./variance.html)                               | Calculates the variance.                |

### `OpenHA.processing.preprocessing`

| functions                                           | description                                                     |
| --------------------------------------------------- | --------------------------------------------------------------- |
| [interpolation](./interpolation.html)               | Interpolation.                                                  |
| [local_outlier_factor](./local_outlier_factor.html) | The Local Outlier Factors (LOF) of all the points are computed. |

### `OpenHA.prognostics`

Under developing...
