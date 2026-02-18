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