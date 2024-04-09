# Introduction of Control Sequence in Flight Information


## 1. Control Sequence Composition
The control sequence consists of various commands, where each command is terminated by a semicolon `;`, and each command is composed of different strings. (All characters are English symbols.) 

The first character of each command represents a class of functions, and the meanings of the existing classes are listed as follows:
1: Time class (including wait by time and wait for reset functions)
2: Control class (including unlock, lock, position control, velocity control, landing, and fault injection functions)

The second character of each command represents the specific function, and the subsequent characters represent the parameters for the corresponding function. The meanings of the existing functions are interpreted as follows:

- 1.Time class
  - 1.Wait by time: Wait(times)
  - 2.Wait for reset: WaitReset(Pos)
- 2.Control class
  - 1.Unlock and Takeoff: Arm2takeoff(param)
  - 2.Lock: DisArm(void)
  - 3.Position Control: FlyPos(pos)
  - 4.Velocity Control: FlyVel(vel)
  - 5.Land: Land(void)
  - 6.Fault Injection: FaultInject(param)
  - 7.Yaw Control: FlyYaw(yaw_rad)
  - 8.Circular Path: FlyCirlce(param)
  - 9.Waypoint Path: FlyLongTrack(param)
  - 10.Acceleration and Deceleration Motion: AcceAndDece(param)
  - 11.Circular Path (with Center): FlyCircleCenter(param)

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

## 2. Meanings of Existing Functions in Control Sequence
### 1.1 Wait by time
  - Function name: Wait(times)
  - Input Parameters: times (1-dimensional, unit:s)
  - Meaning: Keep last commands for `times` seconds, and wait for next command.
  - Usage form: `"1,1,times;"`

### 1.2 Wait for reset
  - Function name: WaitReset(Pos)
  - Input Parameters: Pos (3-dimensional, units:m)
  - Meaning: Keep last commands until the UAV reaches the designated location `Pos`.
  - Usage form: `"1,2,Pos[0],Pos[1],Pos[2];"`

### 2.1 Unlock and Takeoff
  - Function name: Arm2takeoff(param)
  - Input Parameters: param[0] (time interval between armed and takeoff), param[1] (take off vz), param[2] (take off h)
  - Meaning: Used for arming and set the take off height and take off velocity in z-axis.
  - Usage form: `"2,1,param[0],param[1],param[2];"`

### 2.2 Lock
  - Function name: Disarm()
  - Input Parameters: Null
  - Meaning: Used for disarming the UAV.
  - Usage form: `"2,2;"`

### 2.3 Position Control
  - Function name: FlyPos(pos)
  - Input Parameters: pos (3-dimensional, units:m)
  - Meaning: Used for navigating the UAV to the designated location `pos` (Inertial Frame, ENU).
  - Usage form: `"2,3,pos[0],pos[1],pos[2];"`

### 2.4 Velocity Control
  - Function name: FlyVel(vel)
  - Input Parameters: vel (3-dimensional, units:m/s)
  - Meaning: Used to make the UAV fly at a set speed (Body frame, FLU).
  - Usage form: `"2,4,vel[0],vel[1],vel[2];"`

### 2.5 Land
  - Function name: Land()
  - Input Parameters: Null
  - Meaning: Used to make the UAV land.
  - Usage form: `"2,5;"`

### 2.6 Fault Injection
  - Function name: FaultInjec(param)
  - Input Parameters: param (The detailed information can be seen in [Section 4](#4-meanings-of-fault-injection-commands).)
  - Meaning: Used to inject the faults into the UAV model.
  - Usage form: `"2,6,param;"`

### 2.7 Yaw Control
  - Function name: FlyYaw(yaw_rad)
  - Input Parameters: yaw_rad (1-dimensional, unit: degree)
  - Meaning: Used to change the yaw angle of the UAV, usually used with [1.1 Wait](#11-wait-by-time).
  - Usage form: `"2,7,yaw_rad;"`

### 2.8 Circlar Path
  - Function name: FlyCircle(param)
  - Input Parameters: param[0] (radius of the circle, unit:m), param[1] (linear vel of the UAV, unit:m/s), param[2] (fly clockwise:0 or anti-clockwise:1)
  - Meaning: Used to make the UAV to fly a circle path with designated radius and velocity.
  - Usage form: `"2,8,param[0],param[1],param[2];"`

### 2.9 Waypoint Track
  - Function name: FlyLongTrack(param)
  - Input Parameters: param[0] (vel1), param[1-4] (pos1 & tgt_yaw1), etc...param[0+5i - 4+5i]
  - Meaning: Used to make the UAV to fly a set of waypoints with designated velocity and location..
  - Usage form: `"2,9,param[0],param[1+i],param[2+i],param[3+i],param[4+i];"(i=0,1,2,...)`

### 2.10 Acceleration and Deceleration Motion
  - Function name: AcceAndDece(param)
  - Input Parameters: param[0] (acceleration), param[1] (time), param[2] (direction: 0 for acceleration and 1 for deceleration)
  - Meaning: Used to make the UAV to fly with an acceleration.
  - Usage form: `"2,10,param[0],param[1],param[2];"`

### 2.11 Circular Path (with Center)
  - Function name: FlyCircleCenter(param)
  - Input Parameters: param[0] (radius of the circle, unit:m), param[1] (linear vel of the UAV, unit:m/s), param[2] (fly clockwise:0 or anti-clockwise:1), param[3-5] (target position of circle(x, y, z))
  - Meaning: Used to make the UAV to fly Circlar path with a center in Inertial Frame.
  - Usage form: `"2,11,param[0],param[1],param[2];"`

## 3. Existing Fault Types in RflyMAD
### 1.Motor Fault 
  - ID: 123450
  - Three fault modes (Sudden: 1, Persistent: 2, and Periodic: 11)
  - The detailed information about meanings of three fault modes can be seen at examples in [Section 4](#4-meanings-of-fault-injection-commands).
  - Four fault parameters within the range [0,1], where 0 represents complete damage, and 1 represents normal.
### 2.Propeller Fault 
  - ID: 123451
  - Four fault parameters within the range [0,1], where 0 represents complete damage, and 1 represents normal.
### 3.Accelerometer Fault
  - ID: 123452
  - Two fault modes (Noise: 3, and Scale Factor: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 4.Gyroscope Fault
  - ID: 123453
  - Two fault modes (Noise: 3, and Scale Factor: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 5.Barometer Fault
  - ID: 123454
  - Two fault modes (Noise: 3, and Scale Factor: 4)
  - Scale Factor Fault (1 fault parameter for scale factor coefficient)
  - Noise Fault (2 fault parameters for noise gain level).
### 6.Magnetometer Fault
  - ID: 123455
  - Two fault modes (Noise: 3, and Scale Factor: 4)
  - Scale Factor Fault (3 fault parameters for scale factor coefficient) 
  - Noise Fault (6 fault parameters for noise gain level).
### 7.GPS Fault
  - ID: 123456
  - Two fault modes (Noise: 3, and Scale Factor: 4)
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
### 20.Without Fault
  - ID: 123549
  - No fault parameters, for there is no fault.

## 4. Meanings of Fault Injection Commands
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
- "param[16]" represents specific fault parameters, and their meanings are defined in [Exising Fault Types in RflyMAD](#3-existing-fault-types-in-rflymad).

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



