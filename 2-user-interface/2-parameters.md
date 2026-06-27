# 2.2 Servo Tool Parameter Settings

For each servo motor, the system manages the axis specification, assigned servo tool number, and additional axis number used during tool change operations.  
Navigation path:  
`[F2: 系统] - 4: Application Parameters - 11: Servo Tool Change - 2: Servo Tool Parameter Settings ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 2: Servo Tool Parameter Settings)`

<p align="center">  
 <img src="../_assets/fig2_2_eng.png"></img>  
 <em><p align="center">图 2.2 Servo Tool 参数设置</p></em>  
</p>

- Axis Type  
选择工具更换轴的规格。  
Options: Servo Gun, Positioner, Jig

- Axis Motion Type  
选择轴是否以线性或旋转运动方式运行。

- Servo Gun / Positioner / Jig Number  
根据所选择的轴类型分配相应的编号。  
伺服工具参数必须与此编号以1:1的方式匹配。  
因此，相同的编号不能用于不同的伺服工具参数集。  
如果不需要配置额外的伺服工具，设置此值为0。

- additional Axis Number  
指定用于连接和断开的附加轴编号。  
如果轴类型为 Servo Gun，则附加轴编号会基于在 Gun Number Assignment 中设置的值自动分配。  
对于 Positioner 或 Jig 轴，用户必须手动分配此编号。  
如果需要，可以在单个附加轴上配置多个定位器或夹具。

<br>

* 示例用法  
以下配置显示了每个伺服工具的轴类型、分配的伺服枪/定位器/夹具编号以及相应的附加轴编号。

  - P1, P2, P3: 分配给附加轴 1 的伺服工具

  - G1, G3, G5: 分配给附加轴 2 的伺服工具

  - G2, G4: 分配给附加轴 3 的伺服工具

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
 <em><p align="center">图 2.3 附加轴和工具更换目标</p></em>  
</p>