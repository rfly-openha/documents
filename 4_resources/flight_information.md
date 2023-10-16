# Introduction of Control Sequence in Flight Information


## 1. Control Sequence Composition
The control sequence consists of various commands, where each command is terminated by a semicolon `;`, and each command is composed of different strings. (All characters are English symbols.) 

The first character of each command represents a control class, and the meanings of the existing control classes are interpreted as follows:
1: Time class (including wait by time and wait for reset functions)
2: Control class (including unlock, lock, position control, velocity control, landing, and fault injection functions)

The second character of each command represents the specific function, and the subsequent characters represent the parameters for the corresponding function. The meanings of the existing functions are interpreted as follows:

- 1.Time class
  - 1.Wait by time: Wait(times)
  - 2.Wait for reset: WaitReset(Pos)
- 2.Control class
  - 1.Unlock and Takeoff - Arm2takeoff(param)
  - 2.Lock - DisArm(void)
  - 3.Position Control - FlyPos(pos)
  - 4.Velocity Control - FlyVel(vel)
  - 5.Land - Land(void)
  - 6.Fault Injection - FaultInject(param)
  - 7.Yaw Control - FlyYaw(yaw_rad)
  - 8.Circular Path - FlyCirlce(param)
  - 9.Waypoint Path - FlyLongTrack(param)
  - 10.Acceleration and Deceleration Motion - AcceAndDece(param)
  - 11.Circular Path (with Center) - FlyCircleCenter(param)

Here is a provided example,
```text
2,1,0.5,1,-10;1,1,5;2,3,0,0,-20;1,2,0,0,-20;2,6,123450,123450,0.6,0.8,1,1;1,1,10;2,5
```
which could be explained as follows:
- Unlock and wait for 0.5 seconds, then fly at a speed of 1 m/s to an altitude of 10 meters (2,1,0.5,1,-10)
- Wait for 5 seconds (1,1,5)
- Send a position control command to fly to the location [0, 0, -20] (2,3,0,0,-20)
- Wait for reset and reset the position to [0, 0, -20] (1,2,0,0,-20)
- Inject a fault, simulating a motor fault with fault injection parameters [0.6, 0.8, 1, 1] (2,6,123450,123450,0.6,0.8,1,1) 
- Wait for 10 seconds (1,1,10) 
- Land (2,5)

Users can freely combine commands according to their needs.

## 2. Exising Fault Types in RflyMAD
### 1.Motor Fault 
  - ID: 123450
  - Three fault modes (Sudden: 1, Persistent: 2, and Periodic: 11)
  - Four fault parameters within the range [0,1], where 0 represents complete damage, and 1 represents normal.
### 2.Propeller Fault 
  - ID: 123451
  - Four fault parameters within the range [0,1], where 0 represents complete damage, and 1 represents normal.
### 3.Accelerometer Fault
  - ID: 123452
  - Two fault modes (Scale Factor: 3, and Noise: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 4.Gyroscope Fault
  - ID: 123453
  - Two fault modes (Scale Factor: 3, and Noise: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 5.Barometer Fault
  - ID: 123454
  - Two fault modes (Scale Factor: 3, and Noise: 4)
  - Scale Factor Fault (1 fault parameter for scale factor coefficient)
  - Noise Fault (2 fault parameters for noise gain level).
### 6.Magnetometer Fault
  - ID: 123455
  - Two fault modes (Scale Factor: 3, and Noise: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 7.GPS Fault
  - ID: 123456
  - Two fault modes (Scale Factor: 3, and Noise: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient)
  - Noise Fault (6 fault parameters for noise gain level).
### 8.Payload Drop Fault
  - ID: 123457
  - One fault parameter: Weight leak ratio within the range [0,1].
### 9.Payload Drift Fault
  - ID: 123458
  - Four fault parameters: Weight leak ratio, drift factors for x, y, and z axes within the range [0,1].
### 10.Payload Leak Fault
  - ID: 123459
  - Two fault parameters: Weight leak ratio and leak factor within the range [0,1].
### 11.User-Defined Hover Time
  - ID: 123540
  - One fault parameter: User-defined hover time.
### 12.Battery Failure
  - ID: 123541
  - No fault parameters, directly triggered.
### 13.Low Voltage Fault 
  - ID: 123542
  - One fault parameter: Remaining voltage ratio within the range [0,1].
### 14.Low Battery Fault
  - ID: 123543
  - One fault parameter: Remaining battery level ratio within the range [0,1].
### 15.Steady Wind Fault 
  - ID: 123544
  - Three fault parameters: Wind speed for x, y, and z axes.
### 16.Gust Wind Fault 
  - ID: 123545
  - Two fault parameters: Gust strength (wind speed) and gust direction.
### 17.Turbulent Wind Fault 
  - ID: 123546
  - One fault parameter: Wind strength (wind speed).
### 18.Crosswind Fault
  - ID: 123547
  - One fault parameter: Wind strength (wind speed).
### 19.Wind Noise
  - ID: 123548
  - Two fault parameters: Wind amplitude disturbance factor (within the range [0,1]) and wind gain level.

## 3.Meaning of Fault Injection Commands
The "FaultInject" function is defined as "FaultInject(param)" in the above section, and the input command format is as follows:
```text
2, 6, ID, mode, param[16]
```
In this format, "2,6" is recognized by the program during command processing, and the program directs execution to the "FaultInject" function. The parameters recognized by the "FaultInject" function are as follows:
```text
ID, mode, param[16]
```
where:
- "ID" represents the code for the type of fault.
- "mode" represents different fault injection modes within a specific fault type.
- "param[16]" represents specific fault parameters, and their meanings are defined in [Exising Fault Types in RflyMAD](#2-exising-fault-types-in-rflymad).

If there is no `mode` in one fault type, the input command format of "FaultInject" function is as follows:
```text
2, 6, ID, param[16]
```
The parameters recognized by the "FaultInject" function are as follows:
```text
ID, param[16]
```

Here are some examples with different modes in the same fault type:
(1) Motor Sudden Fault:
```text
2,1,0.5,0.3,1.5;1,1,1;2,4,0.8,0,0;1,1,10;2,6,123450,3,0.9,0.9,0.8,1.0;1,1,10
```
- "2,1,0.5,0.3,1.5" is the takeoff command.
- "1,1,1" is a wait command (1 second).
- "2,4,0.8,0,0" is a forward flight command.
- "1,1,10" is a wait command (10 seconds).
- "2,6,123450,1,0.9,0.9,0.8,1.0" is a fault parameter injection command.
  - '2,6' is the instruction to call the fault injection program.
  - '123450' is the fault ID, indicating a motor fault.
  - '1' is the fault mode, representing a sudden fault.
  - '0.9,0.9,0.8,1.0' are the four failure parameters corresponding to the sudden fault.

(2) Motor Persistent Fault:
```text
2,1,0.5,0.3,1.2;1,1,1;2,4,1.0,0,0;1,1,5;2,6,123450,2,1,0.9,20,1,0.9,20,1,1,1,1,1,1;1,1,25
```
- "2,1,0.5,0.3,1.2" is the takeoff command.
- "1,1,1" is a wait command (1 second).
- "2,4,1.0,0,0" is a forward flight command.
- "1,1,5" is a wait command (5 seconds).
- "2,6,123450,2,1,0.9,20,1,0.9,20,1,1,1,1,1,1" is a fault parameter injection command.
  - '2,6' is the instruction to call the fault injection program.
  - '123450' is the fault ID, indicating a motor fault.
  - '2' is the fault mode, representing a gradual fault.
  - '1,0.9,20,1,0.9,20,1,1,1,1,1,1' are the gradual fault injection parameters. Each group of three parameters represents the reduction of thrust from 100% to 90% over 20 seconds.

(3) Motor Periodic Fault:
```text
2,1,0.5,0.3,1.5;1,1,1;2,4,1.0,0,0;1,1,5;2,6,123450,11,6,0.5,0.85,1,1,1;1,1,40
```
- "2,1,0.5,0.3,1.5" is the takeoff command.
- "1,1,1" is a wait command (1 second).
- "2,4,1.0,0,0" is a forward flight command.
- "1,1,5" is a wait command (5 seconds).
- "2,6,123450,11,6,0.5,0.85,1,1,1" is a fault parameter injection command.
  - '2,6' is the instruction to call the fault injection program.
  - '123450' is the fault ID, indicating a motor fault.
  - '11' is the fault mode, representing periodic sudden fault, and the program will automatically correct the mode to 1 and periodically send the fault.
  - '6' is the fault appearance cycle.
  - '0.5' is the time during the cycle when the fault is active.
  - '0.85,1,1,1' are the four failure parameters corresponding to the periodic sudden fault.



