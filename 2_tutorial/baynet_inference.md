# `baynet_inference`

Use the pre-trained model and test_result to get probability.

## Syntax

```python
baynet_inference(D_matrix, model_path, test_result)
```

## Description

This function uses the original D matrix data file to obtain the name of test indicators and different fault types. So only the headers of the original data file is in need. Together with the pre-trained model, the test result from real experiments is also sent into this function, so the fault probability will be returned by this function after model inference.

## Examples

```python
>>> import panda as pd
>>> from pgmpy.models import BayesianNetwork
>>> from pgmpy.inference import VariableElimination, BeliefPropagation

>>> path = <your folder absolute path> + '/' + 'D_matrix-CMG.xlsx'
>>> model_path = <your folder absolute path> + '/' + 'CMG.xmlbif'
>>> testResult = [0] + [1 for i in range(23)]
>>> result = baynet_inference(path, model_path, testResult)
>>> temp = sorted(result.items(), key=lambda x: x[1])
>>> fault = []
>>> prob = []
>>> for ele in temp:
        fault.append(ele[0])
        prob.append(ele[1])

>>> output = {'fault': fault, 'prob': prob}
>>> print(output)

The result of `function`: 
{'fault': ['控制板:转子控制器:速度环', '控制板:转子控制器:电流环', '控制板:转子控制器:电流采集卡', '控制板:转子控制器:换向器', '控制板:转子控制器:转子加电检测器', '控制板:转子控制器:绕组开关驱动器', '控制板:转子控制器:100v加电开关', '控制板:转子控制器:100v断电开关', '控制板:框架控制器:位置环', '控制板:框架控制器:滑模控制', '控制板:框架控制器:逻辑变换', '控制板:框架控制器:27V加电', '控制板:框架控制器:27V断电', '控制板:框架控制器:27V加电状态', '控制板:框架控制器:角速度计算', '控制板:框架控制器:超速判断', '控制板:旋变SPI:通讯模块', '控制板:旋变SPI:粗精耦合', '控制板:1553通讯:复位状态', '控制板:1553通讯:转子加断电', '控制板:1553通讯:框架加断电', '旋转变压器', '旋变解调机箱:串行通讯', '旋变解调机箱:激磁', '旋变解调机箱:粗机解调', '旋变解调机箱:精机解调', '驱动板:转子驱动电路:100V开关控制', '驱动板:转子驱动电路:电压斩波器', '驱动板:转子驱动电路:半桥驱动电路', '驱动板:转子驱动电路:绕组开通切断开关组', '驱动板:转子驱动电路:100V加电状态', '驱动板:转子驱动电路:固紧端轴温检测', '驱动板:转子驱动电路:电流采样', '驱动板:转子驱动电路:转子电机电压', '驱动板:转子驱动电路:滑动端轴温检测', '驱动板:框架驱动电路:全桥驱动电路', '驱动板:框架驱动电路:27V加断电', '驱动板:框架驱动电路:电流 采样', '驱动板:框架驱动电路:27V加电状态', '框架驱动电机:Hall传感器', '转子驱动电机:电机绕组', '转子轴承:固紧端热敏电阻', '转子轴承:滑动端热敏电阻', '电源板:27V', '驱动板:框架驱动电路:继电器', '控制板:框架控制器:绕组加电', '控制板:1553通讯:框架过流判断', '控制板:框架控制器:绕组断电', '控制板:1553通讯:转子过流判断', '控制板:转子控制器:转速采集', '转子驱动电机:Hall传感器', '导电环'], 
'prob': [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.16764, 0.17412, 0.2467, 0.31494, 0.38221, 0.5, 0.5, 0.5]}

```

---

Here is the second example of this function.

```python
>>> import panda as pd
>>> from pgmpy.models import BayesianNetwork
>>> from pgmpy.inference import VariableElimination, BeliefPropagation

>>> path = <your folder absolute path> + '/' + 'D_matrix-IMU.xlsx'
>>> model_path = <your folder absolute path> + '/' + 'IMU.xmlbif'

>>> # Remainder the user to enter an array as test result
>>> input_array = input("Please enter an array of length 30 consisting of 0 and 1, with elements separated by commas:")
>>> # Convert the input string into an array
>>> test_result = [int(x) for x in input_array.split(',')]
>>> # Check if the array length is 30
>>> if len(test_result) == 30:
        print("The test item result is entered correctly.")
    else:
        print(f"Array length is invalid. Current length is {len(test_result)}")

>>> result = baynet_inference(path, model_path, test_result)
>>> temp = sorted(result.items(), key=lambda x: x[1])
>>> fault = []
>>> prob = []
>>> for ele in temp:
        fault.append(ele[0])
        prob.append(ele[1])
>>> output = {'fault': fault, 'prob': prob}
>>> print(output)


The result of `function`: 
{'fault': ['导航板导航数据通讯单元', '导航板控制单元', '导航板模拟数据采集单元', '导航板储存单元', '滤波板滤波电路', '滤波板尖峰和浪涌抑制电路', '滤波板储能电路', '滤波板直流28V监测电路', '滤波板备用28V监测电路', '电源板±15V直流转换电路', '电源板5.1V直流转换电路', '电源板-5.1V直流转换电路', '电源板5V直流转换电路', '电源板二次电源检测电路', '电源板信号联接单元', '惯性部件箱体单元', '滤波板28V反接保护电路', '惯性部件IMU单元', '滤波板信号联接单元', '导航板供电单元', '滤波板后端滤波电路', '惯性部件信号联接单元'], 
'prob': [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.20478395061728394, 0.2619957030317498, 0.2737662650965728, 0.32082021041345576, 0.5, 0.5, 0.5020339255567168]}
```

Attention:

The example files in the above code are the source D matrix data files and pre-trained models, which are also uploaded at [Bayesian Net Download](https://rfly-openha.github.io/documents/5_download_support/BayesianNetDownload.html) website. 

## Input Arguments

`D_matrix` —— A string. It is the path where the source D matrix data file is located. It is recommended to use the absolute path of this file, for the function doesn't handle the input path exactly.

---

`model_path` —— A string. It is the path where the pre-trained bayesian network is located. It is recommended to use the absolute path of this file, for the function doesn't handle the input path exactly.

---

`test_result` —— An array. It contains the test results from each test indicator. When the test result from an indicator is 0 means there is no fault, and 1 represents that there is a fault detected by the indicator.

## Properties of Arguments
| Name of the parameters  | is optional?    | Source, dialog or input port?|
| -------------------- | ------------------------- |---------------------- |
|       `D_martix`      |          No           |        Input port      |
|     `model_path`      |          No           |        Input port        |
|     `test_result`     |          No           |        Input port        |


## Output Arguments

`result` —— An array. It contains the fault probability of each items in the prediction of the Bayesian Network with the input `test_result`.