
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Servo Tool Change

[__SOURCE](1-intro/README.md)
# 1. Overview
[__SOURCE](1-intro/1-definition.md)
# 1.1 What is Multi (Servo) Tool Change?

Servo tool change refers to the process in which the robot automatically replaces tools—such as jigs, positioners, or servo guns equipped with servo motors—using an Automatic Tool Changer (ATC).

<p align="center">
 <img src="../_assets/fig1_1.png"></img>
 <em><p align="center">Figure 1.1 Servo Tool and Robot</p></em>
</p>


This manual is written based on a system equipped with three additional axes: the first axis is used for three positioners, the second axis is used for three servo guns, and the third axis is used for two servo guns, all of which are exchanged and operated via an ATC. The actual system installed on site may differ, so operators must refer to this manual and apply the procedures according to the specifications of the on-site equipment.

<!--
## System Specifications Covered in This Manual
<p align="center">
 <img src="../_assets/fig1_2_eng.png"></img>
 <em><p align="center">Figure 1.2 Types of Servo Tools Covered in This Manual</p></em>
</p>
-->

<br>

{% hint style="info" %}   
 - Required reference document  
    -	[${cont_model} Robot Controller Operation Manual](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-Hi6-tp630/README?cont_model=${cont_model})  
    -	[${cont_model} Robot Controller Operation Manual - Additional axes](https://hrbook-hrc.web.app/#/view/doc-add-axes/en/README?cont_model=${cont_model})
    -   [${cont_model} Functional Manual - Positioner Sync.](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/README?cont_model=${cont_model})
    -	[${cont_model} Robot Controller Function Manual - Spot Welding](https://hrbook-hrc.web.app/#/view/doc-spot-weld/en/README?cont_model=${cont_model})

{% endhint %}
[__SOURCE](1-intro/2-specs.md)
#  1.2 Specifications

The specifications of the Servo Tool Change function in the ${cont_model} robot controller are as follows:


| Item | Specification | 
| :---: | :---: | 
| Maximum number of supported tool motors | 16 ea | 
| Supported tool types | servo gun, positioner, jig | 
| Maximum number of tools that can be changed simultaneously | 4 ea | 
[__SOURCE](1-intro/3-operations.md)
# 1.3 Operation Workflow

To use the Servo Tool Change function, the system must be initialized and configured to a level that supports additional axes.
Based on the system specifications covered in this manual, the workflow—from system initialization to user program creation—is summarized in the table below.



| Step | Configuration | Description | Detailed Setting Path |Notes|
| :---: | :---: | :---: |:---:  |:---:|
| 1 | [System Initialization](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/1-system-format?cont_model=${cont_model}) | Perform system initialization |`system**/5:Intialization/1:System format] ||
| 2 | [Robot Type Selection](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/2-robot-type-sel?cont_model=${cont_model})| Register robot type and number of additional axes |`system**/5:Intialization/2:Robot type selection] |Number of additional axes: 3|
| 3 | Rebooting |  | ||
| 4 | [Additional Axis Parameter Setup](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/5-add-axis-param?cont_model=${cont_model}) | Register additional axis information |`system**/5:Intialization/5:Additional axis parameter setting] |Default setup: T1 = G1, T2 = G2, T3 = J1|
| 5 | Rebooting |  | ||
| 6 | [Application Settings](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/3-usage-set/README?cont_model=${cont_model}) | Configure application settings, I/O signals, and user key assignments |`system**/5:Intialization/3:Usage setting] |Spot welding usage, user key assignment|
| 7 | [Encoder Offset Setup](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/4-robot-parameter/4-encoder-offset/README?cont_model=${cont_model}) | Register encoder origin |`system**/3: Robot Parameters → 4: Encoder Offset] ||
| 8 | [Axis Origin Setup](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/4-robot-parameter/2-axis-origin?cont_model=${cont_model}) | Set the axis origin and run automatic calibration |`system**/3: Robot Parameters → 2: Axis Origin] ||
| 9 | [*Spot Gun Setup](https://hrbook-hrc.web.app/#/view/doc-spot-weld/en/5-spot-weld-parameter/5-2-welding-gun-parameter/README?cont_model=${cont_model}) | Configure gun parameters (only for spot welding). |`system**/4: Application Parameters → 1: Spot Welding → 2: Welding Gun Parameters] ||
| 10 | [Servo Tool Change Setup](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/README?cont_model=${cont_model}) | Configure environment settings for servo tool change |`system**/4: Application Parameters → 11: Servo Tool Change] ||
| 11 | [Tool Data Setup](https://hrbook-hrc.web.app/#/view/doc-load-estimation/en/README?cont_model=${cont_model}) | Perform load estimation for tool attach/detach (T0) | `system**/6: Auto calibration → 4: Load Estimation] ||
| 12 | [Positioner Calibration](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/2-system_settings/2-3-positioner-calibration/README?cont_model=${cont_model}) | When using a positioner for servo tool change, create calibration programs for each positioner | ||
| 13 | [Program Development](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/3-programming/README?cont_model=${cont_model}) |  | |toolchng (attach/detach) <br> posi_calib (Positioner Calibration)|
| 14 | [Auto Operation](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/2-operation/2-automatic-operation/README?cont_model=${cont_model}) |  | ||


<br>


{% hint style="info" %}
- *Spot Gun Configuration (Required only when using spot welding)
    - Assign the tool number, additional axis number, and welding controller number corresponding to each gun number. 
    - Servo tool parameters can be configured only for gun numbers defined in this setting.
{% endhint %}

<br>

<p align="center">
 <img src="../_assets/fig1_3_eng.png"></img>
 <em><p align="center">Figure 1.3 Spot Gun Configuration</p></em>
</p>


<br>

The configuration described above is summarized in the table below.

|Welder	|Gun number|Tool number|Gun type|Additional axis|
| :---: | :---: | :---: |:---:  |:---:|
|W1|**G1**|	T1|	servo gun	|a2|
|W2|**G2**|	T2|	servo gun	|a3|
|W1|**G3**| T3|	servo gun	|a2|
|W2|**G4**| T4|	servo gun	|a3|
|W1|**G5**|	T5|	servo gun	|a2|


[__SOURCE](2-user-interface/README.md)
# 2. User Interface


[__SOURCE](2-user-interface/1-environment.md)
# 2.1 Environment Settings

Servo tool change environment settings must be configured before use.

『system』 → 『4: Application parameter』 → 『11: Servo tool change』 → 『1: Environment setting』

<p align="center">
 <img src="../_assets/fig2_1_eng.png"></img>
 <em><p align="center">Figure 2.1 Servo Tool Change Environment Settings</p></em>
</p>

- function use  
Enables or disables the tool change feature for additional axes.

- connection  
Monitors the current status of the servo tool (attached or detached).
If the tool is currently attached, it can be forcibly detached.
To do so, switch the status to Off while the motor is powered Off, then cycle the controller power.
Forced attachment is not supported when the tool is detached.

- encoder poswer output signal   
Assigns the output signal used to control encoder power during tool attachment or detachment.
When this signal is On, the relay controlling the 5V encoder power is activated.
	
- encoder poswer input signal  
Assigns the input signal used to verify the encoder power control state during tool attachment or detachment.
This input monitors whether the relay controlling the 5V encoder power is operating correctly. 

<br>

{% hint style="info" %}
- The I/O signal logic can be configured under:
『System』 → 『2: Control Parameters』 → 『2: I/O Signal Settings』 → 『1: Input Signal Attributes』 / 『2: Output Signal Attributes』

- Among the system I/O signals, user-defined signals are assigned as follows:
SI[48-51] / SO[48-51]
{% endhint %}

<br>

**Encoder Reset**

For the first installation of a servo tool, an encoder reset must be performed before the tool can be attached.
The encoder reset procedure is as follows:

  1. Make Servo Tool Change enabled ('enable' radio button)
  2. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '1' → Encoder power ON 
  3. [Encoder reset](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/4-serial-encoder-reset?cont_model=${cont_model}) 
  4. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '0' → Encoder power OFF


{% hint style="warning" %}
If the servo tool is attached without performing an encoder reset, an encoder-related error will occur.
{% endhint %}
[__SOURCE](2-user-interface/2-parameters.md)
# 2.2 Servo Tool Parameter Settings


For each servo motor, the system manages the axis specification, assigned servo tool number, and additional axis number used during tool change operations.
Navigation path:
『[F2]: System』 → 『4: Application Parameters』 → 『11: Servo Tool Change』 → 『2: Servo Tool Parameter Settings』

<p align="center">
 <img src="../_assets/fig2_2_eng.png"></img>
 <em><p align="center">Figure 2.2 Servo Tool Parameter Settings</p></em>
</p>


- Axis Type  
Select the specification of the tool change axis.
Options: Servo Gun, Positioner, Jig

- Axis Motion Type  
Select whether the axis operates in Linear or Rotary motion.

- Servo Gun / Positioner / Jig Number  
Assign the corresponding number based on the selected axis type.
The servo tool parameters must match this number in a 1:1 mapping.
Therefore, the same number cannot be used for different servo tool parameter sets.
If no additional servo tools need to be configured, set this value to 0.

- additional Axis Number  
Specify the additional axis number used for attachment and detachment.
If the axis type is Servo Gun, the additional axis number is automatically assigned based on the value set in Gun Number Assignment.
For Positioner or Jig axes, the user must manually assign this number.
Multiple positioners or jigs may be configured on a single additional axis if required.

<br>

*	Example Usage  
The following configuration shows the axis type, assigned servo gun/positioner/jig number, and corresponding additional axis number for each servo tool.

  - P1, P2, P3: Servo tools assigned to additional axis 1

  - G1, G3, G5: Servo tools assigned to additional axis 2

  - G2, G4: Servo tools assigned to additional axis 3


<br>


|Tool Change Target|Axis Type|Motion Type|Servo Gun / Jig Number|Additionary axis number|
| :---: | :---: | :---: |:---: |:---:|
|Servo Tool #1|Servo Gun|Linear|G1|2|
|Servo Tool #2|Servo Gun|Linear|G2|3|
|Servo Tool #3|Positioner|Rotary|P1|1|
|Servo Tool #4|Servo Gun|Linear|G3|2|
|Servo Tool #5|Servo Gun|Linear|G4|3|
|Servo Tool #6|Positioner|Rotary|P2|1|
|Servo Tool #7|Positioner|Rotary|P3|1|
|Servo Tool #8|Servo Gun|Linear|G5|2|

<br>

In an actual Servo Tool Change system, the relationship between additional axes and servo tool parameters is applied as shown in the diagram below.


<p align="center">
 <img src="../_assets/fig2_3_eng.png"></img>
 <em><p align="center">Figure 2.3 Additional Axis and Tool Change Targets</p></em>
</p>

[__SOURCE](2-user-interface/3-origins.md)
# 2.3 Axis Origin

The system manages the axis home position for each servo motor. 

Navigation path:
『System』 → 『4: Application Parameters』 → 『11: Servo Tool Change』 → 『3: Axis Home Position』

<p align="center">
 <img src="../_assets/fig2_4_eng.png"></img>
 <em><p align="center">Figure 2.4 Servo Tool Axis Home Position Settings</p></em>
</p>

<br>

When a servo tool is connected, the home position of the corresponding additional axis is automatically updated to the home position assigned to the selected servo tool.
In other words, the values configured under:
『System』 → 『4: Application Parameters』 → 『11: Servo Tool Change』 → 『3: Axis Home Position』
are automatically applied to:
『System』 → 『3: Robot Parameters』 → 『2: Axis Home Position』.

In addition to the axis home position, the following parameters are also automatically updated to the values assigned to the connected servo tool:

- Soft limit of the corresponding additional axis  

- Encoder offset  

- Servo parameters  

- Acceleration/deceleration parameters
[__SOURCE](2-user-interface/4-monitoring.md)
# 2.4 Monitoring

The status related to the Servo Tool Change function can be monitored by the user.

Menu Path:
『Operation Panel』 → 『Select』 → 『Servo Tool Change』

<p align="center">
 <img src="../_assets/fig2_5_eng.png"></img>
 <em><p align="center">Figure 2.5 Servo Tool Change Monitoring Screen</p></em>
</p>

<br>


- Servo Tool Change Function  
Displays whether the servo tool change function is enabled for the additional axis.

- Servo Tool Connection Status  
Indicates the current connection state of the servo tool on the additional axis.
If the tool is connected, the corresponding tool identifier is displayed.
If disconnected, "--" is shown.

- Encoder Power Output  
Displays the assigned output signal number used for encoder power control as well as its ON/OFF status.

- Encoder Power Input  
Displays the assigned input signal number used to monitor the encoder power state along with its ON/OFF status.

<br>

{% hint style="info" %}
- The logic level of input/output signals can be configured in:

『System』 → 『2: Control Parameters』 → 『2: I/O Signal Settings』 →
『1: Input Signal Attributes』 / 『2: Output Signal Attributes』

- System I/O signals for user mapping correspond to SI[48-51] / SO[48-51].

{% endhint %}

[__SOURCE](2-user-interface/5-toolchng.md)
# 2.5 Attach/Detach Command (toolchng)


```toolchng``` command is a procedure used to switch the servo tool assigned to an additional axis.


### Description 
    
There are two methods to change the servo tool:

- Manual operation using R-code (358)

- Executing a task program using  ```toolchng``` command  

When using the command-based method, a completion signal input is required.

To use this command, the servo tool change environment must be properly configured beforehand.

<br>

### Syntax
  
  ```python
   toolchng on/off,tg=<Target Tool>,is=<Completion Signal>,wait=<Timeout>
  ```

<br>

### Parameter Description

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        Connect or disconnect the servo tool
        <ul>
        <li>on : Connect the assigned servo tool</li>
        <li>off :  Disconnect the assigned servo tool</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Target tool</td>
      <td style="text-align:left">
        Specifies the tool to be connected or disconnected.  
        Available types:
        <ul>
        <li>G1~G16 : Spot welding gun numbers</li>
        <li>P1~P16 : Positioner numbers</li>
        <li>J1~J16 : Jig numbers</li>
        </ul>
        If multiple tools are changed simultaneously, specify them as a string array. <br>
        ex.) toolchng on,tg=["G1","G2"],is=si50,wait=3.0  
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Connection complete signal</td>
      <td style="text-align:left">
        Input signal used to confirm mechanical tool engagement.
      </td>
      <td style="text-align:left"></td>
      <tr>
      <td style="text-align:left">wait</td>
      <td style="text-align:left">
        Timeout duration
        <ul>
        <li><0~5.0> (sec) : Maximum waiting time (in seconds) for the completion signal. If the signal is not received within the specified time, an error will be generated.</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <tr>
    </tr>
  </tbody>
</table>


<br>

### Usage Examples
```python
S10	  move L, ...
      toolchng off,tg=G1		

S11	  move L, ...	
  	  toolchng on,tg=G4,is=di20	

S22	  move L, ...
      toolchng off,tg=G4		

S31	  move L, ...	
  	  toolchng on,tg=[G1,G2],is=di20	

S42	  move L, ...
      toolchng off,tg=[G1,G2]		


```
[__SOURCE](2-user-interface/6-manual.md)
# 2.6 Manual Attach/Detach Function

Servo tools can be manually connected or disconnected while the system is in Manual Mode.
Manual servo tool change is executed by entering '[R..] + 358'.
This procedure applies to all servo tool types including jigs and positioners.

This section explains how to use the R358 manual tool change function for servo guns and positioners based on the configuration shown in [2.2 Servo Tool Parameter Settings](../2-user-interface/2-parameters.md) (Figure 2.3).


### (1) Manual Positioner Connection/Disconnection

- Switch the mode selector to Manual Mode, and enable Servo Tool Change for additional axis 1.
(A reboot is required if system settings have been modified.)

- Press the [R..] key, then enter 358.

- The tool change command window will appear.
  Enter "1" to initiate tool connection.

- Since the tool type is a positioner, enter "2".

- Enter the target positioner number, for example "1".

<p align="center">
 <img src="../_assets/fig2_6_eng.png"></img>
 <em><p align="center">Figure 2.6 Positioner P1 Connection</p></em>
</p>

<br>

{% hint style="info" %}  
If the motor is not ON, the following message will appear and the connection/disconnection process will not be executed.

<p align="center">
 <img src="../_assets/fig2_7_eng.png"></img>
 
</p>
{% endhint %}

<br>

### (2)	Manual Servo Gun Connection/Disconnection

- Switch the mode selector to Manual Mode, and enable Servo Tool Change for additional axis 1.
(A reboot is required if the setting has been modified.)

- Press the [R..] key, then enter 358.

- When the tool change command window appears, enter "1" to execute the connection.

- Since the tool type is a servo gun, enter "1".

- Enter the servo gun number to be connected, for example "1".

<p align="center">
 <img src="../_assets/fig2_8_eng.png"></img>
 <em><p align="center">Figure 2.8 Servo Gun G1 Connection</p></em>
</p>

<br>

<p align="center">
 <img src="../_assets/fig2_9_eng.png"></img>
 <em><p align="center">Figure 2.9 Servo Gun G2 Connection</p></em>
</p>


<br>

{% hint style="info" %}

-  When selecting "Fix" during the tool change input, the tool will not be physically changed.
 This function is used only to update the servo tool's axis origin, soft limit, and encoder offset.
- If the additional axis type is a jig, enter "3" for the axis type selection.
{% endhint %}
- If all additional axes are configured with the same tool type, the system will not request input for "Tool Type" during the R358 manual operation.
[__SOURCE](2-user-interface/7-timing.md)
# 2.7 Attach/Detach Timing

###	Connection  

When the connection command (toolchng on) is executed and the robot and servo tool are mechanically coupled, the controller receives the connection-complete signal and performs the internal connection process.
During this sequence, the encoder power for the servo tool axis is enabled and the motor is turned ON.

###	Disconnection

The disconnection command (toolchng off) executes the reverse sequence of the connection process to remove the tool.

<br>


<p align="center">
 <img src="../_assets/fig2_10_eng.png"></img>
 <em><p align="center">Figure 2.10 Servo Tool Change Connection/Disconnection Timing</p></em>
</p>

[__SOURCE](2-user-interface/8-posical.md)
# 2.8 Positioner Calibration Command (posi_calib)


This command performs positioner calibration, which is required for synchronized motion between the robot and the positioner.
Normally, positioner calibration is executed through the setup dialog.
However, when the positioner changes during operation due to a servo tool change, calibration must be updated while the robot is running.
The posi_calib command allows this process to be executed within a robot program.

<br>

For detailed usage instructions, refer to "[2.3.4 posi_calib](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/2-system_settings/2-3-positioner-calibration/4_posi_calib?cont_model=${cont_model})" in the documentation.
[__SOURCE](3-job/README.md)
# 3. Job Examples

[__SOURCE](3-job/1-sample-job.md)
# 3.1 Tool Change Attach/Detach Example




```python
S10   move L, ...                         # Move to servo tool release position
      toolchng off,tg=G1                  # Execute servo tool disconnection
                                          # Servo tool disconnection output (dedicated output)
      do11 = 1                            # Output ATC cam open signal
      wait di11                           # Wait for ATC cam open confirmation signal

S11   move L, ...                         # Robot motion
S12   move L, ...                         # Robot motion
S13   move L, ...                         # Robot motion

S14   move L, ...                         # Move to servo tool connection position
      wait di12                           # Wait for tool connection-ready signal
      do11 = 0                            # Output ATC cam close signal
      toolchng on,tg=G1,di=1              # Execute mechanical connection of the servo tool
                                          # Servo tool connection process

S15   move L, ...                         # Robot motion

```
[__SOURCE](3-job/2-positioner-example.md)
# 3.2 Positioner Attach/Detach Example


<p align="center">
 <img src="../_assets/fig3_1.png"></img>
 <em><p align="center">Figure 3.1 Example System Configuration: Two Robots and Three Positioners (Italian Manufacturer C)</p></em>
</p>

<br>

(1)	System Configuration of the Positioner Change System

- System layout: 2 robots + 3 positioners

- Required equipment:

    - ATC (Auto Tool Changer) capable of connecting each positioner to each robot

    - Servo gun changer compatible with our robots

(2)	Operation Workflow

- Robot 1 connects to Positioner A and performs welding.
 Robot 2 connects to Positioner C and performs welding.
Meanwhile, the operator mounts a workpiece on Positioner B.

- When work on each positioner is completed, the connection between the robot and positioner is released.

- After all three independent operations are completed, the entire positioner system rotates 120° counterclockwise.

- Robot 1 then connects to Positioner B and starts processing.
 Robot 2 connects to Positioner A.
The operator mounts a new workpiece onto Positioner C.

- This cycle continues repeatedly.

(3)	Precautions

Perform the disconnection and connection operations of each positioner at the same defined location whenever possible, to ensure stable operation and prevent mechanical tolerance misalignment.
[__SOURCE](4-faq/README.md)
# 4. FAQ

1. Is pneumatic gun tool change supported?

   If the target tool is a gun and its type is defined as a pneumatic gun, the system supports attach/detach operations for the pneumatic gun.
<br>

2. An encoder-related error appears during the first servo tool attachment. What should I do?

   Before using the tool for the first time, an encoder reset must be performed.
In an environment where servo tool change is enabled, supply encoder power using R359, then perform the encoder reset first. ([2.1.1 Encoder Reset](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/2-user-interface/1-environment?cont_model=${cont_model}))

<br>