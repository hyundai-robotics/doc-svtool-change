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

※	Example Usage  
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
