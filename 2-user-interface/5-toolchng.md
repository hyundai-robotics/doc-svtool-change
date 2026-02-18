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