# Manual Control GD20 invt Inverter
**Control *invt* Inverter GD20 Series manually by programming groups**  
<img src="https://i.imgur.com/3k4Hsev.jpg" width="210" height="350">
<img src="https://i.imgur.com/robAkFR.png" width="280" height="350">  
***invt** inverter  model **GD20-0R7G-S2** and **SPG 60W 3-phase motor** are used for examples in this reference.*

## Product Overview
### Name plate
<img src="https://i.imgur.com/VqdgyqS.png" width="400" height="215">

### Specifications
<img src="https://i.imgur.com/Sxol4Uo.png" width="200" height="45">  
<img src="https://i.imgur.com/ZLw7K5P.png" width="600" height="185">

## Keypad Operation
<img src="https://i.imgur.com/7zYExoP.png" width="550" height="550">

## Start/Stop and Rotation Control
### Parameter adjustment
For example, set parameter `P00.01 = 1`  
<img src="https://i.imgur.com/O6DTtqs.png" width="690" height="285">  
**Note:** *Normally, SHIFT key is used to change the display of setting frequency, motor speed, output
ampere, ... (pay attention to the status lights corresponding to the data displayed)*.

### Getting started
To start manually programming inverter with keypad mode, you have to make sure that all settings are set to default. To do this, these following steps are applied:
- Step 1: Make connection for inverter and motor by wiring 3 lines U-V-W from motor to inverter
- Step 2: Connect L-N terminals to power supply (220Vac) and start the inverter
- Step 3: Set parameter `P00.18 = 1` to restore default settings
- Step 4: Set Maximum output frequency `P00.03` and Upper limit of the running frequency `P00.04` must greater than rated frequency of the motor
	- `P00.03 >= 50`
	- `P00.04 = 50 ~ P00.03`
- Step 5: Set motor parameter (60W 3Ph SPG motor)
	- Motor power (kW) → `P02.01 = 0.06`
	- Frequency (Hz) → `P02.01 = 50`
	- Speed (RPM) → `P02. 03 = 1350`
	- Voltage (V) → `P02.04 = 220`
	- Current (A) → `P02.05 = 0.8`
- Step 6: Set `P00.01 = 0` to run command from keypad
- Step 7: Set `P00.06 = 1` to adjust motor speed by potentiometer on keypad

Now we can control some simple tasks of motor using keypad: *start/stop motor*, *control speed manually*, *jogging to test*.

### Control rotation direction
The procedure of switching FWD/REV rotation is described in the *figure* below.  
<img src="https://i.imgur.com/yiNVZDn.png" width="475" height="240">  
Before controlling the switching rotation process, first we have to resive some important control parameters of group `P01`.  
<img src="https://i.imgur.com/lDhEglS.png" width="685" height="350">  
For example, to have the motor switched its rotation direction at frequency 40Hz immediately, we can adjust the above parameters to control the process.  
- `P01.13 = 0` (can be ignored)
- `P01.14 = 2`
- `P01.15 = 40`
- `P01.24 = 0` (can be ignored)

## Start with Profile and DC Braking
### Acceleration and deceleration
To adjust the acceleration and deceleration time manually by kedpad, we can access and manipulate two parameters `P00.11` and `P00.12`, where:
- `P00.11` is acceleration time (ACC time 1) as the inverter speeds up from 0Hz to maximum frequency (value of `P00.03`)
- `P00.12` is deceleration time (DEC time 1) as the inverter speeds down from maximum frequency (value of `P00.03`) to 0Hz
> *Both `P00.11` and `P00.12` have the range of 0.0 to 3600.0s*

### DC braking
#### DC injection braking overview
> **DC injection bracking (or DC braking) is a non-contact electromagnetic interaction method to decelerate the moving of rotor by injecting DC current into two of three windings of the rotor.**

<img src="https://i.imgur.com/EsBY9Cy.jpg" width="410" height="250">  
*DC injection braking begins when AC voltage is removed (S1 opens) and DC voltage is injected into the windings (S2 closes)*

**Advantages and disadvantages of DC braking**  

Advantages | Disadvantages
---------- | -------------
The higher the DC current, the stronger the braking force | Heat generated by braking distributing to the rotor and the inverter's circuit
Alternative to a friction brake system | Require a constant power supply for DC bus
high applicability with DC bus | Avoid braking at high speed, short braking time or braking frequently

There are some methods to control braking process of the motor and DC braking is one of them, other two common methods are *dynamic braking* and *regenerative braking*. In this reference, we use DC braking since 60W motor only needed a small DC braking current to stop rotating.

#### DC braking control


## Register
## Modbus Overview

## References
[1]   
[2]   
[3]   
[4] https://www.motioncontroltips.com/what-is-dc-injection-braking-and-how-does-it-compare-with-other-methods/  
[5] 