# 2.4 监控

与伺服工具更换功能相关的状态可以由用户监控。

菜单路径：
`操作面板 - 选择 - 伺服工具更换 (Operation Panel - Select - Servo Tool Change)`

<p align="center">
 <img src="../_assets/fig2_5_eng.png"></img>
 <em><p align="center">图 2.5 伺服工具更换监控屏幕</p></em>
</p>

<br>

- 伺服工具更换功能  
显示附加轴的伺服工具更换功能是否启用。

- 伺服工具连接状态  
指示附加轴上伺服工具的当前连接状态。
如果工具已连接，显示相应的工具标识符。
如果断开连接，则显示"--"。

- 编码器电源输出  
显示用于编码器电源控制的分配输出信号编号及其开/关状态。

- 编码器电源输入  
显示用于监控编码器电源状态的分配输入信号编号及其开/关状态。

<br>

{% hint style="info" %}
- 输入/输出信号的逻辑级别可以在以下位置配置：

`[F2: 系统] - 2: 控制参数 - 2: I/O信号设置 - 1: 输入信号属性 - 2: 输出信号属性 ([F2: System] - 2: Control Parameters - 2: I/O Signal Settings - 1: Input Signal Attributes - 2: Output Signal Attributes)`

- 使用 Hi6 控制器，用户映射的系统 I/O 信号对应 SI[48-51] / SO[48-51]。

{% endhint %}