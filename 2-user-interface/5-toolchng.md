# 2.5 접속/분리 명령(toolchng)


```toolchng``` 명령문은 부가축에 할당된 서보툴을 변경하기 위한 프로시져입니다.


### 설명 
    
서보툴을 변경하는 방법은 Rcode를(358) 이용한 수동조작과 ```toolchng```문을 이용한 작업 프로그램 실행 방식이 있습니다.
- 명령문을 이용한 방법에서는 완료신호 입력이 필요합니다.
- 본 명령어를 사용하기 위해서는 서보툴 체인지 환경이 적절하게 설정되어야 합니다.



<br>

### 문법
  
  ```python
   toolchng on/off,tg=<체인지 대상>,di=<접속완료 신호>,wait=<대기시간>
  ```

<br>

### 파라미터

<table>
  <thead>
    <tr>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">의미</th>
      <th style="text-align:left">기타</th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td style="text-align:left">on/off</td>
      <td style="text-align:left">
        접속/분리
        <ul>
        <li>on : 서보툴 접속</li>
        <li>off :  서보툴 분리</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">체인지 대상</td>
      <td style="text-align:left">
        접속/분리 대상이 되는 서보툴 번호
        <ul>
        <li>G1~G16 : 접속/분리할 용접건 번호</li>
        <li>P1~P16 : 접속/분리할 포지셔너 번호</li>
        <li>J1~J16 : 접속/분리할 지그 번호</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">접속완료 신호</td>
      <td style="text-align:left">
        기계적 접속완료 확인신호
        <ul>
        <li>1~4096 : 기계적인 접속완료 확인을 위한 입력신호 번호</li>
        <li>내용(vol_offset) : Arc용접 시 시너직 전압의 옵셋 전압 값</li>
        <li>범위(vol) : 20 ~ 40 V</li>
        <li>범위(vol_offset) : 200 ~ 200 V(%)</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <tr>
      <td style="text-align:left">대기시간</td>
      <td style="text-align:left">
        접속완료 대기시간
        <ul>
        <li><0~5.0> (sec) : 접속완료 대기시간 (파라미터가 없거나 0이면 무한대기)</li>
        </ul>
      </td>
      <td style="text-align:left"></td>
      <tr>
    </tr>
  </tbody>
</table>


<br>

### 사용예
```python
S10	  move L, ...
      toolchng off,tg=G1		

S11	  move L, ...	
  	  toolchng on,tg=G4,di=1	

S12	  move L, ...
```