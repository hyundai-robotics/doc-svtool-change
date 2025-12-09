# 2.5 Attach/Detach Command (toolchng)


```toolchng``` command is a procedure used to switch the servo tool assigned to an additional axis.


### Description 
    
There are two methods to change the servo tool:

- Manual operation using R-code (358)

- Executing a task program using  ```toolchng``` command  

When using the command-based method, a completion signal input is required.

To use this command, the servo tool change environment must be properly configured beforehand.

<br>

### Syntax
  
  ```python
   toolchng on/off,tg=<Target Tool>,is=<Completion Signal>,wait=<Timeout>
  ```

<br>

### Parameter Description

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Meaning</th>
      <th style="text-align:left">Note</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        Connect or disconnect the servo tool
        <ul>
        <li>on : Connect the assigned servo tool</li>
        <li>off :  Disconnect the assigned servo tool</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Target tool</td>
      <td style="text-align:left">
        Specifies the tool to be connected or disconnected.  
        Available types:
        <ul>
        <li>G1~G16 : Spot welding gun numbers</li>
        <li>P1~P16 : Positioner numbers</li>
        <li>J1~J16 : Jig numbers</li>
        </ul>
        If multiple tools are changed simultaneously, specify them as a string array. <br>
        ex.) toolchng on,tg=["G1","G2"],is=si50,wait=3.0  
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Connection complete signal</td>
      <td style="text-align:left">
        Input signal used to confirm mechanical tool engagement.
      </td>
      <td style="text-align:left"></td>
      <tr>
      <td style="text-align:left">wait</td>
      <td style="text-align:left">
        Timeout duration
        <ul>
        <li><0~5.0> (sec) : Maximum waiting time (in seconds) for the completion signal. If the signal is not received within the specified time, an error will be generated.</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <tr>
    </tr>
  </tbody>
</table>


<br>

### Usage Examples
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