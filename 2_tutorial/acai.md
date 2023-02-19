```python
>>> from OpenHA.assessment.attribute import acai, control_allocation
>>> import numpy as np

>>> bf = control_allocation(4, 0.28, 0.1)
>>> fmax, fmin = 6, 0
>>> G = np.array([15, 0, 0, 0]).reshape((-1, 1))
>>> acai(bf, fmax, fmin, G)

0.7299473938200366

```
