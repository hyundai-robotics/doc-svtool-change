
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 伺服工具更换
[__SOURCE](0-about-this-manual/README.md)
# 关于手册

[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}

[__SOURCE](1-intro/README.md)
# 1. 概述
[__SOURCE](1-intro/1-definition.md)
# 1.1 什么是多（伺服）工具更换？

伺服工具更换是指机器人通过自动工具更换器（ATC）自动更换工具的过程，例如夹具、定位器或配备伺服电机的伺服枪。

<p align="center">
 <img src="../_assets/fig1_1.png"></img>
 <em><p align="center">图 1.1 伺服工具和机器人</p></em>
</p>

本手册基于一个装备有三个附加轴的系统编写：第一个轴用于三个定位器，第二个轴用于三个伺服枪，第三个轴用于两个伺服枪，所有这些工具通过ATC进行更换和操作。现场安装的实际系统可能有所不同，因此操作员必须参考本手册，并根据现场设备的规格应用相应的程序。

<!--
## 本手册涉及的系统规格
<p align="center">
 <img src="../_assets/fig1_2_eng.png"></img>
 <em><p align="center">图 1.2 本手册涉及的伺服工具类型</p></em>
</p>
-->

<br>

{% hint style="info" %}   
 - 所需参考文件  
    -	[${cont_model} 机器人控制器操作手册](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/README?cont_model=${cont_model})  
    -	[${cont_model} 机器人控制器操作手册 - 附加轴](https://hrbook-hrc.web.app/#/view/doc-add-axes/en/README?cont_model=${cont_model})
    -   [${cont_model} 功能手册 - 定位器同步](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/README?cont_model=${cont_model})
    -	[${cont_model} 机器人控制器功能手册 - 点焊](https://hrbook-hrc.web.app/#/view/doc-spot-weld/en/README?cont_model=${cont_model})

{% endhint %}
[__SOURCE](1-intro/2-specs.md)
#  1.2 规格

${cont_model}机器人控制器中伺服工具更换功能的规格如下：

| 项目 | 规格 | 
| :---: | :---: | 
| 支持的工具电机最大数量 | 16 个 | 
| 支持的工具类型 | 伺服枪、定位器、夹具 | 
| 可以同时更换的工具最大数量 | 4 个 |
[__SOURCE](1-intro/3-operations.md)
# 1.3 操作工作流程

要使用伺服工具更换功能，系统必须初始化并配置到支持附加轴的级别。
基于本手册中涵盖的系统规格，从系统初始化到用户程序创建的工作流程总结如下表所示。

| 步骤 | 配置 | 描述 | 详细设置路径 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| 1 | [系统初始化](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/1-system-format?cont_model=${cont_model}) | 执行系统初始化 | `system**/5:Intialization/1:System format] | |
| 2 | [机器人类型选择](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/2-robot-type-sel?cont_model=${cont_model}) | 注册机器人类型和附加轴数量 | `system**/5:Intialization/2:Robot type selection] | 附加轴数量：3 |
| 3 | 重启 |  |  |  |
| 4 | [附加轴参数设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/5-add-axis-param?cont_model=${cont_model}) | 注册附加轴信息 | `system**/5:Intialization/5:Additional axis parameter setting] | 默认设置：T1 = G1, T2 = G2, T3 = J1 |
| 5 | 重启 |  |  |  |
| 6 | [应用设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/3-usage-set/README?cont_model=${cont_model}) | 配置应用设置、I/O信号和用户按键分配 | `system**/5:Intialization/3:Usage setting] | 点焊用途，用户按键分配 |
| 7 | [编码器偏移设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/4-robot-parameter/4-encoder-offset/README?cont_model=${cont_model}) | 注册编码器原点 | `system**/3: Robot Parameters → 4: Encoder Offset] |  |
| 8 | [轴原点设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/4-robot-parameter/2-axis-origin?cont_model=${cont_model}) | 设置轴原点并运行自动校准 | `system**/3: Robot Parameters → 2: Axis Origin] |  |
| 9 | [*点焊枪设置](https://hrbook-hrc.web.app/#/view/doc-spot-weld/en/5-spot-weld-parameter/5-2-welding-gun-parameter/README?cont_model=${cont_model}) | 配置枪参数（仅适用于点焊）。 | `system**/4: Application Parameters → 1: Spot Welding → 2: Welding Gun Parameters] |  |
| 10 | [伺服工具更换设置](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/README?cont_model=${cont_model}) | 配置伺服工具更换的环境设置 | `system**/4: Application Parameters → 11: Servo Tool Change] |  |
| 11 | [工具数据设置](https://hrbook-hrc.web.app/#/view/doc-load-estimation/en/README?cont_model=${cont_model}) | 执行工具附加/分离（T0）的负载估计 | `system**/6: Auto calibration → 4: Load Estimation] |  |
| 12 | [定位器校准](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/2-system_settings/2-3-positioner-calibration/README?cont_model=${cont_model}) | 使用定位器进行伺服工具更换时，为每个定位器创建校准程序 |  |  |
| 13 | [程序开发](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/3-programming/README?cont_model=${cont_model}) |  |  | toolchng（附加/分离）<br> posi_calib（定位器校准） |
| 14 | [自动操作](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/2-operation/2-automatic-operation/README?cont_model=${cont_model}) |  |  |  |

<br>

{% hint style="info" %}
- *点焊枪配置（仅在使用点焊时需要）
    - 指定与每个枪编号对应的工具编号、附加轴编号和焊接控制器编号。
    - 伺服工具参数仅能为在此设置中定义的枪编号进行配置。
{% endhint %}

<br>

<p align="center">
 <img src="../_assets/fig1_3_eng.png"></img>
 <em><p align="center">图1.3 点焊枪配置</p></em>
</p>

<br>

上述配置总结如下表所示。

| 焊接机 | 枪编号 | 工具编号 | 枪类型 | 附加轴 |
| :---: | :---: | :---: | :---: | :---: |
| W1 | **G1** | T1 | 伺服枪 | a2 |
| W2 | **G2** | T2 | 伺服枪 | a3 |
|W1|**G3**| T3|	伺服枪	|a2|
|W2|**G4**| T4|	伺服枪	|a3|
|W1|**G5**|	T5|	伺服枪	|a2|
[__SOURCE](2-user-interface/README.md)
# 2. 用户界面
[__SOURCE](2-user-interface/1-environment.md)
# 2.1 环境设置

伺服工具更换环境设置必须在使用前进行配置。

`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 1: 环境设置 ([F2: system] - 4: Application parameter - 11: Servo tool change - 1: Environment setting)`

<p align="center">
 <img src="../_assets/fig2_1_eng.png"></img>
 <em><p align="center">图 2.1 伺服工具更换环境设置</p></em>
</p>

- 功能使用  
启用或禁用额外轴的工具更换功能。

- 连接  
监测伺服工具的当前状态（连接或分离）。  
如果工具当前已连接，可以强制分离。  
为此，在电机关闭的情况下，将状态切换为“关”，然后循环控制器电源。  
当工具被分离时，不支持强制连接。

- 编码器电源输出信号  
分配用于在工具连接或分离期间控制编码器电源的输出信号。  
当该信号为“开”时，控制5V编码器电源的继电器被激活。

- 编码器电源输入信号  
分配用于验证工具连接或分离期间编码器电源控制状态的输入信号。  
该输入监测控制5V编码器电源的继电器是否正常工作。

<br>

{% hint style="info" %}
- I/O信号逻辑可以在以下位置配置：  
`[F2: 系统] - 2: 控制参数 - 2: I/O信号设置 - 1: 输入信号属性 - 2: 输出信号属性 ([F2: System] - 2: Control Parameters - 2: I/O Signal Settings - 1: Input Signal Attributes - 2: Output Signal Attributes)`

- 在系统I/O信号中，用户定义信号分配如下：  
SI[48-51] / SO[48-51]
{% endhint %}

<br>

**编码器重置**

在首次安装伺服工具前，必须执行编码器重置才能连接工具。  
编码器重置程序如下：

  1. 启用伺服工具更换（选中“启用”单选按钮）  
  2. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '1' → 编码器电源开启  
  3. [编码器重置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/6-initialization/4-serial-encoder-reset?cont_model=${cont_model})  
  4. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '0' → 编码器电源关闭  
{% hint style="warning" %}
如果在未执行编码器重置的情况下连接伺服工具，将会发生与编码器相关的错误。
{% endhint %}
[__SOURCE](2-user-interface/2-parameters.md)
# 2.2 伺服工具参数设置

对于每个伺服电机，系统管理轴规格、分配的伺服工具编号和在工具更换操作中使用的附加轴编号。
导航路径：
`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 2: 伺服工具参数设置 ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 2: Servo Tool Parameter Settings)`

<p align="center">
 <img src="../_assets/fig2_2_eng.png"></img>
 <em><p align="center">图 2.2 伺服工具参数设置</p></em>
</p>

- 轴类型  
选择工具更换轴的规格。  
选项：伺服枪、定位器、夹具

- 轴运动类型  
选择轴是否以线性或旋转运动操作。

- 伺服枪 / 定位器 / 夹具编号  
根据选择的轴类型分配相应的编号。  
伺服工具参数必须与此编号进行1:1映射。  
因此，相同的编号不能用于不同的伺服工具参数集。  
如果不需要配置额外的伺服工具，请将此值设置为0。

- 附加轴编号  
指定用于连接和断开的附加轴编号。  
如果轴类型为伺服枪，附加轴编号将根据在枪编号分配中设置的值自动分配。  
对于定位器或夹具轴，用户必须手动分配此编号。  
如果需要，可以在单个附加轴上配置多个定位器或夹具。

<br>

* 示例用法  
以下配置显示每个伺服工具的轴类型、分配的伺服枪/定位器/夹具编号以及相应的附加轴编号。

  - P1, P2, P3：分配给附加轴1的伺服工具

  - G1, G3, G5：分配给附加轴2的伺服工具

  - G2, G4：分配给附加轴3的伺服工具

<br>

|工具更换目标|轴类型|运动类型|伺服枪 / 夹具编号|附加轴编号|
| :---: | :---: | :---: |:---: |:---:|
|伺服工具 #1|伺服枪|线性|G1|2|
|伺服工具 #2|伺服枪|线性|G2|3|
|伺服工具 #3|定位器|旋转|P1|1|
|伺服工具 #4|伺服枪|线性|G3|2|
|伺服工具 #5|伺服枪|线性|G4|3|
|伺服工具 #6|定位器|旋转|P2|1|
|伺服工具 #7|定位器|旋转|P3|1|
|伺服工具 #8|伺服枪|线性|G5|2|

<br>

在实际的伺服工具更换系统中，附加轴和伺服工具参数之间的关系如下图所示。

<p align="center">
 <img src="../_assets/fig2_3_eng.png"></img>
 <em><p align="center">图 2.3 附加轴和工具更换目标</p></em>
</p>
[__SOURCE](2-user-interface/3-origins.md)
# 2.3 轴原点

系统管理每个伺服电机的轴原点位置。

导航路径：
`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 3: 轴原点 ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 3: Axis Home Position)`

<p align="center">
 <img src="../_assets/fig2_4_eng.png"></img>
 <em><p align="center">图 2.4 伺服工具轴原点设置</p></em>
</p>

<br>

当伺服工具连接时，相应的附加轴的原点位置会自动更新为分配给所选伺服工具的原点位置。
换句话说，配置在：
`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 3: 轴原点 ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 3: Axis Home Position)`
的值会自动应用于：
`[F2: 系统] - 3: 机器人参数 - 2: 轴原点 ([F2: System] - 3: Robot Parameters - 2: Axis Home Position)`。

除了轴原点，以下参数也会自动更新为分配给连接的伺服工具的值：

- 对应附加轴的软限位  

- 编码器偏移  

- 伺服参数  

- 加速度/减速度参数  
[__SOURCE](2-user-interface/4-monitoring.md)
# 2.4 监控

与伺服工具更换功能相关的状态可以由用户监控。

菜单路径：
`操作面板 - 选择 - 伺服工具更换`

<p align="center">
 <img src="../_assets/fig2_5_eng.png"></img>
 <em><p align="center">图 2.5 伺服工具更换监控屏幕</p></em>
</p>

<br>

- 伺服工具更换功能  
显示附加轴的伺服工具更换功能是否启用。

- 伺服工具连接状态  
指示附加轴上伺服工具的当前连接状态。
如果工具已连接，相应的工具标识符会显示。
如果未连接，则显示 "--"。

- 编码器电源输出  
显示用于编码器电源控制的分配输出信号号码及其开/关状态。

- 编码器电源输入  
显示用于监控编码器电源状态的分配输入信号号码及其开/关状态。

<br>

{% hint style="info" %}
- 输入/输出信号的逻辑电平可以在以下位置配置：

`[F2: 系统] - 2: 控制参数 - 2: I/O 信号设置 - 1: 输入信号属性 - 2: 输出信号属性 ([F2: System] - 2: Control Parameters - 2: I/O Signal Settings - 1: Input Signal Attributes - 2: Output Signal Attributes)`

- 用户映射的系统 I/O 信号对应于 SI[48-51] / SO[48-51]。

{% endhint %}
[__SOURCE](2-user-interface/5-toolchng.md)
# 2.5 附加/解除命令 (toolchng)

```toolchng``` 命令是用于切换分配给附加轴的伺服工具的程序。

### 描述

更改伺服工具有两种方法：

- 使用 R-code (358) 的手动操作

- 使用 ```toolchng``` 命令执行任务程序  

使用基于命令的方法时，需要输入完成信号。

要使用此命令，伺服工具更换环境必须事先正确配置。

<br>

### 语法

```python
toolchng on/off,tg=<目标工具>,is=<完成信号>,wait=<超时>
```

<br>

### 参数描述

<table>
  <thead>
    <tr>
      <th style="text-align:left">参数</th>
      <th style="text-align:left">含义</th>
      <th style="text-align:left">备注</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        连接或断开伺服工具
        <ul>
        <li>on : 连接指定的伺服工具</li>
        <li>off : 断开指定的伺服工具</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
<tr>
      <td style="text-align:left">目标工具</td>
      <td style="text-align:left">
        指定要连接或断开的工具。  
        可用类型：
        <ul>
        <li>G1~G16 : 点焊枪编号</li>
        <li>P1~P16 : 定位器编号</li>
        <li>J1~J16 : 夹具编号</li>
        </ul>
        如果同时更换多个工具，请将其指定为字符串数组。 <br>
        ex.) toolchng on,tg=["G1","G2"],is=si50,wait=3.0  
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">连接完成信号</td>
      <td style="text-align:left">
        用于确认机械工具接合的输入信号。
      </td>
      <td style="text-align:left"></td>
      <tr>
      <td style="text-align:left">等待</td>
      <td style="text-align:left">
        超时时间
        <ul>
        <li><0~5.0> (秒) : 等待完成信号的最长时间（以秒为单位）。如果在指定时间内未收到信号，将会生成错误。</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <tr>
    </tr>
  </tbody>
</table>


<br>

### 使用示例
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
# 2.6 手动连接/断开功能

伺服工具可以在系统处于手动模式时手动连接或断开。
手动伺服工具更换通过输入 '[R..] + 358' 执行。
此过程适用于所有伺服工具类型，包括夹具和定位器。

本节解释如何使用 R358 手动工具更换功能，针对根据 [2.2 伺服工具参数设置](../2-user-interface/2-parameters.md) 显示的配置进行伺服枪和定位器的操作。

### (1) 手动定位器连接/断开

- 将模式选择器切换到手动模式，并启用附加轴 1 的伺服工具更换。
（如果修改了系统设置，需要重启。）

- 按下 [R..] 键，然后输入 358。

- 工具更换命令窗口将出现。
  输入 "1" 以启动工具连接。

- 由于工具类型是定位器，输入 "2"。

- 输入目标定位器编号，例如 "1"。

<p align="center">
 <img src="../_assets/fig2_6_eng.png"></img>
 <em><p align="center">图 2.6 定位器 P1 连接</p></em>
</p>

<br>

{% hint style="info" %}  
如果电机未开启，将出现以下消息，连接/断开过程将无法执行。

<p align="center">
 <img src="../_assets/fig2_7_eng.png"></img>
 
</p>
{% endhint %}

<br>

### (2) 手动伺服枪连接/断开

- 将模式选择器切换到手动模式，并启用附加轴 1 的伺服工具更换。
（如果设置已被修改，需要重启。）

- 按下 [R..] 键，然后输入 358。

- 当工具更换命令窗口出现时，输入 "1" 以执行连接。
- 由于工具类型是伺服枪，请输入“1”。

- 输入要连接的伺服枪编号，例如“1”。

<p align="center">
 <img src="../_assets/fig2_8_eng.png"></img>
 <em><p align="center">图 2.8 伺服枪 G1 连接</p></em>
</p>

<br>

<p align="center">
 <img src="../_assets/fig2_9_eng.png"></img>
 <em><p align="center">图 2.9 伺服枪 G2 连接</p></em>
</p>

<br>

{% hint style="info" %}

-  在工具更换输入时选择“固定”，工具将不会被物理更换。
 此功能仅用于更新伺服工具的轴原点、软限制和编码器偏移。
- 如果附加轴类型是夹具，请在轴类型选择中输入“3”。
{% endhint %}
- 如果所有附加轴都配置为相同的工具类型，在 R358 手动操作期间系统将不请求输入“工具类型”。
[__SOURCE](2-user-interface/7-timing.md)
# 2.7 附加/拆卸时机

### 连接  

当执行连接命令（toolchng on）并且机器人与伺服工具机械耦合时，控制器接收到连接完成信号并执行内部连接过程。 在此过程中，伺服工具轴的编码器电源被启用，电机被打开。

### 断开

断开命令（toolchng off）执行连接过程的反向序列以移除工具。

<br>

<p align="center">
 <img src="../_assets/fig2_10_eng.png"></img>
 <em><p align="center">图 2.10 伺服工具更换连接/断开时机</p></em>
</p>
[__SOURCE](2-user-interface/8-posical.md)
# 2.8 位置器校准命令 (posi_calib)

此命令执行位置器校准，这是机器人与位置器之间同步运动所必需的。  
通常，位置器校准通过设置对话框执行。  
然而，当在操作过程中由于伺服工具更换而导致位置器发生变化时，必须在机器人运行时更新校准。  
posi_calib 命令允许在机器人程序中执行此过程。

<br>

有关详细使用说明，请参阅文档中的 "[2.3.4 posi_calib](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/en/2-system_settings/2-3-positioner-calibration/4_posi_calib?cont_model=${cont_model})"。
[__SOURCE](3-job/README.md)
# 3. 工作示例
[__SOURCE](3-job/1-sample-job.md)
# 3.1 工具更换附加/分离示例




```python
S10   move L, ...                         # 移动到伺服工具释放位置
      toolchng off,tg=G1                  # 执行伺服工具断开
                                          # 伺服工具断开输出（专用输出）
      do11 = 1                            # 输出ATC凸轮打开信号
      wait di11                           # 等待ATC凸轮打开确认信号

S11   move L, ...                         # 机器人运动
S12   move L, ...                         # 机器人运动
S13   move L, ...                         # 机器人运动

S14   move L, ...                         # 移动到伺服工具连接位置
      wait di12                           # 等待工具连接准备信号
      do11 = 0                            # 输出ATC凸轮关闭信号
      toolchng on,tg=G1,di=1              # 执行伺服工具的机械连接
                                          # 伺服工具连接过程

S15   move L, ...                         # 机器人运动

```
[__SOURCE](3-job/2-positioner-example.md)
# 3.2 定位器连接/断开示例


<p align="center">
 <img src="../_assets/fig3_1.png"></img>
 <em><p align="center">图3.1 示例系统配置：两个机器人和三个定位器（意大利制造商C）</p></em>
</p>

<br>

(1)	定位器变更系统的系统配置

- 系统布局：2个机器人 + 3个定位器

- 所需设备：

    - ATC（自动换刀装置），能够将每个定位器连接到每个机器人

    - 与我们的机器人兼容的伺服枪换装装置

(2)	操作工作流程

- 机器人1连接到定位器A并进行焊接。机器人2连接到定位器C并进行焊接。与此同时，操作员在定位器B上安装工件。

- 当每个定位器上的工作完成后，机器人与定位器之间的连接会释放。

- 在所有三个独立操作完成后，整个定位器系统逆时针旋转120°。

- 然后，机器人1连接到定位器B并开始加工。机器人2连接到定位器A。操作员在定位器C上安装一个新工件。

- 这个循环不断重复。

(3)	注意事项

尽可能在相同的定义位置执行每个定位器的断开和连接操作，以确保稳定的操作并防止机械公差错位。
[__SOURCE](4-faq/README.md)
# 4. 常见问题

1. 是否支持气动枪工具更换？

   如果目标工具是枪，其类型定义为气动枪，则系统支持气动枪的连接/断开操作。
<br>

2. 在第一次伺服工具附件过程中出现编码器相关错误。我该怎么办？

   在首次使用工具之前，必须执行编码器重置。
在启用伺服工具更换的环境中，使用 R359 供电编码器电源，然后首先执行编码器重置。 ([2.1.1 编码器重置](https://hrbook-hrc.web.app/#/view/doc-svtool-change/en/2-user-interface/1-environment?cont_model=${cont_model}))

<br>