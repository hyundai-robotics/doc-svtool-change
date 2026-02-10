
[__SOURCE](README.md)
# ${cont_model} 제어기 기능설명서 - 서보툴 체인지

[__SOURCE](1-intro/README.md)
# 1. 개요
[__SOURCE](1-intro/1-definition.md)
# 1.1 멀티 (서보)툴 체인지란?

서보 모터가 부착된 두 개 이상의 툴(지그, 포지셔너, 서보건 등)에 대하여 툴 체인저(ATC)를 이용하여 로봇이 자동으로 툴을 교체하는 행위를 말합니다.

<p align="center">
 <img src="../_assets/fig1_1.png"></img>
 <em><p align="center">그림 1.1 서보툴과 로봇</p></em>
</p>


본 설명서에서는 
 - 6축 로봇
 - 부가축 1 (a1) : 포지셔너 (포지셔너 3개 툴체인지)
 - 부가축 2 (a2) : 서보건 (서보건 3개 툴체인지)
 - 부가축 3 (a3) : 서보건 (서보건 2개 툴체인지)  

 총 9축으로 구성된 가상의 시스템을 기반으로 설명을 진행합니다. 현장에서 사용하는 시스템이 이와 동일할 수는 없으므로 본 설명서의 내용을 참고하여 현장 시스템에 맞게 사용하십시오.

<!--
## 설명서에서 다루는 시스템 사양
<p align="center">
 <img src="../_assets/fig1_2.png"></img>
 <em><p align="center">그림 1.2 설명서에서 다루는 서보툴의 종류</p></em>
</p>
-->

<br>

{% hint style="info" %}   
 - 필수설명서  
    -	[${cont_model} 로봇제어기 조작설명서](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/README?cont_model=${cont_model})  
    -	[${cont_model} 로봇제어기 기능설명서 - 부가축](https://hrbook-hrc.web.app/#/view/doc-add-axes/ko/README?cont_model=${cont_model})   
    -   [${cont_model} 로봇제어기 기능설명서 - 포지셔너동기](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/ko/README?cont_model=${cont_model})  
    -	[${cont_model} 로봇제어기 기능설명서 - 스폿 용접](https://hrbook-hrc.web.app/#/view/doc-spot-weld/ko/README?cont_model=${cont_model})

{% endhint %}
[__SOURCE](1-intro/2-specs.md)
#  1.2 주요사양

${cont_model} 로봇제어기의 서보툴 체인지 기능 사양은 다음 표와 같습니다.


| 항목 | 사양 | 
| :---: | :---: | 
| 체인지 가능한 모터의 최대 수 | 16개 | 
| 체인지 축 사양 | 서보건, 포지셔너, 지그 | 
| 동시 체인지 최대 수 | 4개 | 
[__SOURCE](1-intro/3-operations.md)
# 1.3 조작 순서

서보툴 체인지 기능을 사용하기 위해서는 부가축을 사용할 수 있는 정도의 시스템 초기화와 설정이 완료되어 있어야 합니다. 본 설명서에서 다루는 시스템 사양과 관련하여, 시스템 초기화부터 사용자 프로그램 작성까지의 작업 순서를 아래표로 설명합니다.



| 순서 | 설정 | 내용 | 상세설정 |참고|
| :---: | :---: | :---: |:---:  |:---:|
| 1 | [시스템 초기화](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/6-initialization/1-system-format?cont_model=${cont_model}) | 시스템 초기화 실시 |`[F2: 시스템] - 5:초기화 - 1:시스템 초기화` ||
| 2 | [로봇타입 선택](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/6-initialization/2-robot-type-sel?cont_model=${cont_model})| 로봇타입 및 부가축 개수 등록 |`[F2: 시스템] - 5:초기화 - 2:로봇타입 선택` |부가축 개수 : 3|
| 3 | 재부팅 | 전원을 끈 후 15초 후 재부팅 | ||
| 4 | 부가축 파라미터 설정 | 부가축 정보 등록 |`[F2: 시스템] - 5:초기화 - 5:시스템 초기화` |T1=G1, T2=G2, T3=J1으로 초기설정|
| 5 | 재부팅 | 전원을 끈 후 15초 후 재부팅 | ||
| 6 | [용도설정](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/6-initialization/3-usage-set/README?cont_model=${cont_model}) | 작업용도설정, 입출력신호, 사용자키 할당 등 |`[F2: 시스템] - 5:초기화 - 3:용도설정` |스폿용도, 스폿 사용자키 할당|
| 7 | [엔코더 옵셋 설정](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/4-robot-parameter/4-encoder-offset/README?cont_model=${cont_model}) | 엔코더 원점 등록 |`[F2: 시스템] - 3:로봇 파라미터 - 4:엔코더 옵셋` ||
| 8 | [축 원점 설정](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/4-robot-parameter/2-axis-origin?cont_model=${cont_model}) | 축 원점 설정, 자동 캘리브레이션 실행 |`[F2: 시스템] - 3:로봇 파라미터 - 2:축 원점` ||
| 9 | [*스폿건 설정](https://hrbook-hrc.web.app/#/view/doc-spot-weld/ko/5-spot-weld-parameter/5-2-welding-gun-parameter/README?cont_model=${cont_model}) | 스폿용접의 경우 건 파라미터 설정 |`[F2: 시스템] - 4:응용 파라미터 - 1:스폿용접 - 2:용접건 파라미터` ||
| 10 | [서보툴 체인지 설정](https://hrbook-hrc.web.app/#/view/doc-svtool-change/ko/README?cont_model=${cont_model}) | 서보툴 체인지를 위한 환경 설정 |`[F2: 시스템] - 4:응용 파라미터 - 11:서보툴 체인지` ||
| 11 | [툴 데이터 설정](https://hrbook-hrc.web.app/#/view/doc-load-estimation/ko/README?cont_model=${cont_model}) | 툴의 분리(T0)와 접속에 따른 부하추정 수행 | `[F2: 시스템] - 6:자동 캘리브레이션 - 4:부하추정 기능` ||
| 12 | [포지셔너 캘리브레이션 수행](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/ko/README?cont_model=${cont_model}) | 포지셔너를 이용한 서보툴 체인지인 경우 각각의 포지셔너 별로 캘리브레이션 프로그램 작성 | ||
| 13 | [프로그램 작성](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/3-programming/README?cont_model=${cont_model}) |  | |toolchng (접속/분리) <br> posi_calib (포지셔너 캘리브레이션)|
| 14 | [자동 운전](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/2-operation/2-automatic-operation/README?cont_model=${cont_model}) |  | ||


<br>


{% hint style="info" %}
- *스폿건 설정 (스폿 용접의 경우에만 설정)  
    - 각 건번호에 대응하는 툴 번호, 부가축 번호, 용접기 번호를 모두 지정합니다.  
    - 본 항목에서 설정된 건 번호에 대해서만 서보툴 체인지에서 서보툴 파라미터 지정이 가능합니다.
{% endhint %}

<br>

<p align="center">
 <img src="../_assets/fig1_3.png"></img>
 <em><p align="center">그림 1.3 스폿 건별 설정</p></em>
</p>


<br>

위 설정을 요약하면 아래 표와 같습니다.

|용접기	|건번호|툴번호|	건타입	|부가축|
| :---: | :---: | :---: |:---:  |:---:|
|W1|**G1**|	T1|	서보건	|a2|
|W2|**G2**|	T2|	서보건	|a3|
|W1|**G3**|	T3|	서보건	|a2|
|W2|**G4**|	T4|	서보건	|a3|
|W1|**G5**|	T5|	서보건	|a2|


[__SOURCE](2-user-interface/README.md)
# 2. 사용자 인터페이스


[__SOURCE](2-user-interface/1-environment.md)
# 2.1 사용환경 설정



서보툴에 대한 체인지 환경을 설정합니다.

`[F2: 시스템] - 4: 응용 파라미터 - 11: 서보툴 체인지 - 1: 사용환경 설정`

<p align="center">
 <img src="../_assets/fig2_1.png"></img>
 <em><p align="center">그림 2.1 서보툴 체인지 사용환경 설정</p></em>
</p>

- 서보툴 체인지 기능   
부가축에 대한 체인지 기능의 사용여부를 설정합니다.  

- 서보툴 접속 상태  
현재 서보툴의 접속 또는 분리 상태를 모니터링합니다. 또한, 현재 서보툴이 접속된 경우에는 강제로 분리할 수 있으며 이를 위해서는 모터 Off 상태에서 **Off**로 변경한 후, 제어기 전원을 재투입하면 됩니다. 이와 반대로 서보툴이 분리된 경우에 강제 접속은 불가합니다.  

- 엔코더 전원투입 출력신호  
접속 또는 분리 시 엔코더 전원 제어를 위한 출력 신호를 할당합니다. 이 신호가 On인 경우 엔코더 5V전원선을 제어하는 릴레이가 동작합니다.  
	
- 엔코더 전원투입 입력신호  
접속 또는 분리 시 엔코더 전원 제어 상태를 확인하기 위한 입력 신호를 할당합니다. 엔코더 5V 전원선을 제어하는 릴레이의 동작 여부를 확인합니다.  

{% hint style="info" %}
-	입출력 신호의 논리는 `[F2: 시스템] - 2: 제어 파라미터 - 2: 입출력 신호 설정 - 1: 입력 신호 속성 - 2: 출력 신호 속성`에서 설정할 수 있습니다.
-	시스템 입출력 신호중 사용자 신호는 각각 SI[48~51]/SO[48~51]로 대응됩니다.
{% endhint %}

<br>

**엔코더 리셋**

최초 서보툴 장착 시 서보툴의 엔코더 리셋을 수행해야 접속이 가능합니다. 엔코더 리셋 절차는 아래와 같습니다.

  1. 서보툴 체인지 사용 설정
  2. [R359](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '1' 입력으로 엔코더 전원 인가 
  3. [엔코더 리셋](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/7-system/6-initialization/4-serial-encoder-reset?cont_model=${cont_model}) 수행
  4. [R359](https://hrbook-hrc.web.app/#/view/doc-${cont_model}-operation/ko-tp630/8-r-code/14-r359?cont_model=${cont_model}) + '0' 입력으로 엔코더 전원 해제


{% hint style="warning" %}
엔코더 리셋 미수행 상태에서 서보툴 체인지 접속시 엔코더 관련 에러 발생합니다.
{% endhint %}
[__SOURCE](2-user-interface/2-parameters.md)
# 2.2 서보툴 파라미터 설정


각 서보모터에 대해 축 사양과 서보툴의 번호, 그리고 체인지시 부가축 번호를 관리합니다. 
`[F2: 시스템] - 4: 응용 파라미터 - 11: 서보툴 체인지 - 2: 서보툴 파라미터 설정`

<p align="center">
 <img src="../_assets/fig2_2.png"></img>
 <em><p align="center">그림 2.2 서보툴 파라미터 설정</p></em>
</p>


-	축 사양
체인지 축의 사양을 선택합니다. <서보건, 포지셔너, 지그> 중 하나로 선택 가능합니다.

-	축 구성 
체인지 축의 축구성이 직동인지 회전인지 선택합니다.

-	서보건/포지셔너/지그 번호 
축사양에 대한 번호를 설정합니다.
서보툴 파라미터와 서보건/포지셔너/지그 번호는 1:1 대응해야 합니다. 따라서 서로 다른 서보툴 파라미터에 동일한 서보건/포지셔너/지그 번호를 중복하여 설정할 수 없습니다.
더 이상 설정할 서보툴이 없는 경우 0번을 설정하면 됩니다.

-	부가축 번호 
접속/분리 시 제어할 부가축의 번호를 지정합니다. 축사양이 서보건이면 '건번호 대응 툴번호 지정'에서 설정된 부가축 번호가 자동으로 지정됩니다. 포지셔너/지그 축인 경우에는 사용자가 설정합니다. 하나의 부가축에 여러 개의 포지셔너/지그를 체인지하는 경우 체인지 할 포지셔너의 수만큼 서보툴 파라미터를 등록합니다.

*	사용 예시  
다음의 설정은 각 서보툴 별 사용하는 축 사양과 서보건/포지셔너/지그번호, 부가축 번호를 나타냅니다.
-	P1, P2, P3: 부가축 1번에 체인지하는 서보툴
-	G1, G3, G5: 부가축 2번으로 체인지하는 서보툴
-	G2, G4: 부가축 3번으로 체인지하는 서보툴


<br>


|체인지 대상|축 사양|축 구성|서보건/지그 번호|부가축 번호|
| :---: | :---: | :---: |:---: |:---:|
|1번 서보툴|서보건|직동|G1|2|
|2번 서보툴|서보건|직동|G2|3|
|3번 서보툴|포지셔너|회전|P1|1|
|4번 서보툴|서보건|직동|G3|2|
|5번 서보툴|서보건|직동|G4|3|
|6번 서보툴|포지셔너|회전|P2|1|
|7번 서보툴|포지셔너|회전|P3|1|
|8번 서보툴|서보건|직동|G5|2|

<br>

실제 서보툴 체인지 시스템 상에서 부가축 및 서보툴의 파라미터 적용 관계는 다음 그림과 같습니다.


<p align="center">
 <img src="../_assets/fig2_3.png"></img>
 <em><p align="center">그림 2.3 부가축과 툴체인지 대상</p></em>
</p>

[__SOURCE](2-user-interface/3-origins.md)
# 2.3 축 원점
각각의 서보모터에 대한 축 원점을 관리합니다. 

`[F2: 시스템] - 4: 응용 파라미터 - 11: 서보툴 체인지 - 3: 축 원점`


<p align="center">
 <img src="../_assets/fig2_4.png"></img>
 <em><p align="center">그림 2.4 서보툴 축 원점 설정</p></em>
</p>


서보툴을 접속하면 해당 부가축의 축 원점이 체인지할 서보툴의 축 원점으로 자동 갱신됩니다. 즉 `[F2: 시스템] - 4: 응용 파라미터 - 11: 서보툴 체인지 - 3: 축 원점`의 설정값으로 `[F2: 시스템] - 3: 로봇 파라미터 - 2: 축 원점`의 값을 갱신합니다.

이 밖에도 해당 부가축의 소프트 리밋, 엔코더 옵셋, 서보 파라미터, 가감속 파라미터도 위에서 언급한 축 원점과 같이 서보툴 접속 시 체인지할 서보툴의 값으로 자동 갱신됩니다.

[__SOURCE](2-user-interface/4-monitoring.md)
# 2.4 모니터링

서보툴 체인지 관련 상태를 사용자에게 모니터링 합니다.

`창조정 - 선택 - 서보툴 체인지`


<p align="center">
 <img src="../_assets/fig2_5.png"></img>
 <em><p align="center">그림 2.5 서보툴 체인지 모니터링</p></em>
</p>

<br>

-	서보툴 체인지 기능  
부가축에 대한 서보툴 체인지 기능의 사용여부를 표시합니다.
 
-	서보툴 접속 상태  
부가축에 대한 서보툴 접속/분리 상태를 표시합니다. 접속인 경우 체인지 대상이 표시되며, 분리인 경우 "--"이 표시됩니다.

-	엔코더 전원투입 출력  
엔코더 전원투입을 위한 출력신호 번호와 함께 출력 상태를 표시합니다.

-	엔코더 전원투입 입력  
엔코더 전원투입을 위한 입력신호 번호와 함께 입력 상태를 표시합니다.

<br>

{% hint style="info" %}
-	입출력 신호의 논리는 `[F2: 시스템] - 2: 제어 파라미터 - 2: 입출력 신호 설정 - 1: 입력 신호 속성 - 2: 출력 신호 속성`에서 설정할 수 있습니다.
-	시스템 입출력 신호중 사용자 신호는 각각 SI[48~51]/SO[48~51]로 대응됩니다.
{% endhint %}

[__SOURCE](2-user-interface/5-toolchng.md)
# 2.5 접속/분리 명령(toolchng)


```toolchng``` 명령문은 부가축에 할당된 서보툴을 변경하기 위한 프로시져입니다.


### 설명 
    
서보툴을 변경하는 방법은 Rcode를(358) 이용한 수동조작과 ```toolchng```문을 이용한 작업 프로그램 실행 방식이 있습니다.
- 명령문을 이용한 방법에서는 완료신호 입력이 필요합니다.
- 본 명령어를 사용하기 위해서는 서보툴 체인지 환경이 적절하게 설정되어야 합니다.



<br>

### 문법
  
  ```python
   toolchng on/off,tg=<체인지 대상>,is=<접속완료 신호>,wait=<대기시간>
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
        멀티건을 동시에 접속/분리하는 경우에는 문자열 배열로 지정합니다. <br>
        ex.) toolchng on,tg=["G1","G2"],is=si50,wait=3.0  
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">접속완료 신호</td>
      <td style="text-align:left">
        기계적 접속완료 확인신호
        <ul>
        <li>di20 : 기계적인 접속완료 확인을 위한 입력신호 번호</li>
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
  	  toolchng on,tg=G4,is=di20	

S22	  move L, ...
      toolchng off,tg=G4		

S31	  move L, ...	
  	  toolchng on,tg=["G1","G2"],is=di20	

S42	  move L, ...
      toolchng off,tg=["G1","G2"]		


```
[__SOURCE](2-user-interface/6-manual.md)
# 2.6 수동 접속/분리 기능



서보툴을 수동상태에서 접속/분리하는 기능입니다. 서보툴 수동 접속/분리는 '[R..]+358'을 입력하여 수행합니다. 지그/포지셔너까지 포함한 서보툴 수동 접속 분리도 '[R..]+358'을 입력하여 수행합니다. 본 장에서는 [2.2 서보툴 파라미터 설정](../2-user-interface/2-parameters.md) 그림2.3의 서보툴 체인지 환경의 포지셔너와 서보건 접속을 위한 R358 사용법에 대해서 설명합니다.

### (1)	포지셔너 수동 접속/분리

- 모드 스위치를 수동모드 전환하고 부가1축의 서보툴 체인지 환경을 '유효'로 합니다. (변경시 재부팅 필요)
- [R..]키 + 358을 입력합니다.
- 체인지 동작 입력창이 나타납니다. 접속을 위해 '1'을 입력합니다.
- 서보툴의 축사양이 포지셔너이므로 '2'를 입력합니다.
- 체인지할 포지셔너 번호 '1'을 입력합니다.
 

<p align="center">
 <img src="../_assets/fig2_6.png"></img>
 <em><p align="center">그림 2.6 포지셔너 P1 접속</p></em>
</p>

<br>

{% hint style="info" %}
모터 ON이 아니면 하기와 같은 메시지가 출력되고 접속/분리가 실행되지 않습니다.

<p align="center">
 <img src="../_assets/fig2_7.png"></img>
 
</p>
 

{% endhint %}




<br>



### (2)	서보건 수동 접속/분리

- 모드 스위치를 수동모드 전환하고 1번 부가축의 서보툴 체인지 환경을 '유효'로 합니다. (변경시 재부팅 필요)
- [R..]키 + 358을 입력합니다.
- 체인지 동작 입력창이 나타납니다. 접속을 위해 '1'을 입력합니다.
- 서보툴의 축사양이 서보건이므로 '1'를 입력합니다.
- 체인지할 서보건 번호 '1'을 입력합니다.
 

<p align="center">
 <img src="../_assets/fig2_8.png"></img>
 <em><p align="center">그림 2.8 서보건 G1 접속</p></em>
</p>

<br>

<p align="center">
 <img src="../_assets/fig2_9.png"></img>
 <em><p align="center">그림 2.9 서보건 G2 접속</p></em>
</p>


<br>

{% hint style="info" %}
- 체인지 동작 입력시 '고정(fix)'는 실제로 툴이 교체되지 않고 서보툴의 축원점과 소프트리밋, 엔코더 옵셋을 변경하기 위한 기능입니다.
- 부가축이 지그인 경우에는 축사양 입력시 '3'을 입력합니다.
- 부가축이 모든 같은 타입인 경우에는 R358 사용시 '서보툴의 축사양'에 대한 입력을 요청하지 않습니다.
{% endhint %}

[__SOURCE](2-user-interface/7-timing.md)
# 2.7 접속/분리 타이밍

###	접속   
접속명령(toolchng on)을 실행중 로봇과 서보툴이 기계적으로 접속이 되면 접속완료 신호를 입력받고 제어기 내부적으로 접속 처리를 수행합니다. 또한, 서보툴축 구동을 위한 엔코더 전원 투입과 모터 ON 동작이 추가됩니다.

###	분리  
분리명령(toolchng off)은 접속과 상반되는 시퀀스를 가지고 분리 처리를 수행합니다.

<br>


<p align="center">
 <img src="../_assets/fig2_10.png"></img>
 <em><p align="center">그림 2.10 서보툴 체인지 접속/분리 타이밍</p></em>
</p>

[__SOURCE](2-user-interface/8-posical.md)
# 2.8 포지셔너 캘리브레이션 명령(posi_calib)


포지셔너가 로봇과 동기동작을 하기 위해 필요한 포지셔너 캘리브레이션을 수행하는 명령입니다. 일반적으로 포지셔너 캘리브레이션은 설정 대화상자를 통해 수행합니다. 그러나, 서보툴 체인지로 포지셔너가 변경되는 경우에는 로봇 운전 중 캘리브레이션이 변경되어야 합니다. 이를 로봇 프로그램 상에서 수행하기 위한 명령어가 포지셔너 캘리브레이션입니다. 

<br>

자세한 명령어 사용법은 "[posi_calib 명령어](https://hrbook-hrc.web.app/#/view/doc-positioner-sync/ko/2-system_settings/2-3-positioner-calibration/4_posi_calib?cont_model=${cont_model})"를 참고하시기 바랍니다.

[__SOURCE](3-job/README.md)
# 3. 작업 예시

[__SOURCE](3-job/1-sample-job.md)
# 3.1 툴체인지의 접속/분리 예시




```python
S10	  move L, ...				#서보툴 분리위치 이동
	  toolchng off,tg=G1		#서보툴 분리 실행
	    			#서보툴 분리 출력(전용출력)
	  do11=1			#ATC cam 개방 출력
	  wait di11				#ATC cam 개방완료 신호확인
S11	  move L, ...				#로봇이동
S12	  move L, ...				#로봇이동
S13	  move L, ...				#로봇이동
S14	  move L, ...				#서보툴 접속위치 이동
	  wait di12			    #접속 가능 신호확인
	  do11=0			#ATC cam 닫기 출력
	  toolchng on,tg=G1,di=1			#기계적 접속 실행
					#서보툴 접속 처리
S15	  move L, ...				#로봇이동
```
[__SOURCE](3-job/2-positioner-example.md)
# 3.2 포지셔너의 접속/분리 예시


<p align="center">
 <img src="../_assets/fig3_1.png"></img>
 <em><p align="center">그림 3.1 로봇 2대, 포지셔너 3대 예시 (이태리 C사 시스템)</p></em>
</p>

<br>

(1)	포지셔너 체인지 시스템의 구성
-	시스템 구성: 로봇 2대 + 포지셔너 3대
-	필요 장비: 각 포지셔너와 각각의 로봇을 연결할 수 있는 ATC(Auto Tool Changer), 당사 로봇의 서보건 체인저

(2)	작업 내용
-	로봇 1이 포지셔너 A와 접속 후 작업 수행. 로봇 2는 포지셔너 C와 작업 수행. 작업자는 포지셔너 B에 작업물 장착
-	각 포지셔너 별 작업이 종료되면 로봇과 포지셔너 간 접속을 끊음.
-	3 부분의 작업이 완료된 후 전체 포지셔너 시스템이 반시계방향으로 120도 회전.
-	로봇 1이 포지셔너 B와 접속 후 작업 수행. 로봇 2는 포지셔너 A와 작업 수행. 작업자는 포지셔너 C에 작업물 장착
-	이후 작업 반복 수행

(3)	주의 사항
-	각 포지셔너의 분리/접속 기능 동작은 가능한 한 동일한 위치에서 수행하십시오.

[__SOURCE](4-faq/README.md)
# 4. 자주하는 질문

1. 공압건의 체인지도 가능한가요?  
체인지 대상이 건이고, 건타입이 공압건인 경우는 공압건에 대한 접속/분리를 수행합니다. 

<br>

2. 처음 서보툴 접속시에 엔코더 관련 에러가 발생하는데 어떻게 해야 하나요?  
툴의 최초 사용을 위해서는 엔코더 리셋을 수행해야 합니다. 서보툴체인지가 가능한 환경에서 R359를 이용해서 엔코더 전원을 입력하고, 엔코더 리셋을 먼저 수행해 주시기 바랍니다. ([2.1.1 엔코더 리셋](https://hrbook-hrc.web.app/#/view/doc-svtool-change/ko/2-user-interface/1-environment?cont_model=${cont_model}) 참고)

<br>