# 2.1 环境设置

伺服工具更换环境设置必须在使用前配置。

`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 1: 使用环境设置 ([F2: system] - 4: Application parameter - 11: Servo tool change - 1: Environment setting)`

<p align="center">
 <img src="../_assets/fig2_1_eng.png"></img>
 <em><p align="center">图 2.1 伺服工具更换环境设置</p></em>
</p>

- 功能使用  
启用或禁用附加轴的工具更换功能。

- 连接  
监控伺服工具的当前状态（已连接或已断开）。
如果当前工具已附着，可以强制断开。
为此，在电机电源关闭时将状态切换为关闭，然后循环控制器电源。
当工具已断开时，不支持强制附着。

- 编码器电源输出信号  
分配用于控制工具附加或断开时编码器电源的输出信号。
当该信号为开启时，控制5V编码器电源的继电器被激活。

- 编码器电源输入信号  
分配用于验证工具附加或断开时编码器电源控制状态的输入信号。
该输入监控控制5V编码器电源的继电器是否正常工作。 

<br>

{% hint style="info" %}
- I/O信号逻辑可以在以下位置配置：
`[F2: 系统] - 2: 控制参数 - 2: I/O信号设置 - 1: 输入信号属性 - 2: 输出信号属性 ([F2: System] - 2: Control Parameters - 2: I/O Signal Settings - 1: Input Signal Attributes - 2: Output Signal Attributes)`

- 在 Hi6 控制器中，系统 I/O 信号中，用户定义信号分配如下：
SI[48-51] / SO[48-51]
{% endhint %}

<br>

**编码器复位**

对于首次安装伺服工具，必须在附加工具之前执行编码器复位。
编码器复位程序如下：

  1. 使能伺服工具更换（'enable' 单选按钮）
  2. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '1' → 编码器电源开启 
  3. [编码器复位](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/6-initialization/4-serial-encoder-reset?cont_model=${cont_model}) 
  4. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '0' → 编码器电源关闭


{% hint style="warning" %}
如果在未执行编码器复位的情况下附加伺服工具，将会发生编码器相关错误。
{% endhint %}