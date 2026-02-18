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