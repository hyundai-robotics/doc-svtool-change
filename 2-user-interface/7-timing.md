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