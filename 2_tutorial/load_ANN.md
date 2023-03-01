# `load_ANN`

<!-- 持续完善中 -->

Loads an object saved with `torch.save()` or `tf.train.Saver()` from a file.

## Syntax

```python
load_ANN(net, path)
load_ANN(net, path, **kwargs)
```

## Description

```python
load_ANN(net, path)
```

Loads the parameters of a well-trained network from a file on the disk.
`net` is an instance of the network model that users build.
`path` specifies the dictionary where the file is located, relatively or absolutely.

---

```python
load_ANN(net, path, **kwargs)
```

More parameters about how to load the network are specified by `kwargs`.
For example, `source` indicate the framework in which the network is build, PyTorch or TensorFlow.
And `map_location` is needed to specify how to remap storage locations in PyTorch.

## Examples

```python
>>> import torch
# the class `CNN` is user-defined
>>> from ANN import CNN
>>> from OpenHA.core.utils import load_ANN

>>> path = 'path_of_the_target_file.pth'
# instance of this class
>>> net = CNN()
# key word argument
>>> map_location = torch.device('cpu')
# load
>>> load_ANN(net, path, source='pytorch', map_location=map_location)

```

## Input Arguments

`net` —— An instance of the network model that users build.

---

`path` —— The dictionary where the file is located, relatively or absolutely.

---

`source` —— The framework in which the network is build, PyTorch or TensorFlow, specified as `pytorch` (default) or `tensorflow`.

---

`map_location` —— Specify how to remap storage locations in [PyTorch](https://pytorch.org/).

## References

[1] https://pytorch.org/docs/stable/generated/torch.load.html
