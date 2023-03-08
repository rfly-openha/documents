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
