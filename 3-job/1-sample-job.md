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