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
SI[48–51] / SO[48–51]
{% endhint %}

<br>

## 2.1.1 Encoder Reset
For the first installation of a servo tool, an encoder reset must be performed before the tool can be attached.
The encoder reset procedure is as follows:

  1. Make Servo Tool Change enabled ('enable' radio button)
  2. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/8-r-code/14-r359) + '1' → Encoder power ON 
  3. [Encoder reset](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-system/6-initialization/4-serial-encoder-reset) 
  4. [R359](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/8-r-code/14-r359) + '0' → Encoder power OFF


{% hint style="warning" %}
If the servo tool is attached without performing an encoder reset, an encoder-related error will occur.
{% endhint %}