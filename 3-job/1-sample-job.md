# 3.1 Tool Change Attach/Detach Example




```python
S10   move L, ...                         # Move to servo tool release position
      toolchng off,tg=G1                  # Execute servo tool disconnection
                                          # Servo tool disconnection output (dedicated output)
      do11 = 1                            # Output ATC cam open signal
      wait di11                           # Wait for ATC cam open confirmation signal

S11   move L, ...                         # Robot motion
S12   move L, ...                         # Robot motion
S13   move L, ...                         # Robot motion

S14   move L, ...                         # Move to servo tool connection position
      wait di12                           # Wait for tool connection-ready signal
      do11 = 0                            # Output ATC cam close signal
      toolchng on,tg=G1,di=1              # Execute mechanical connection of the servo tool
                                          # Servo tool connection process

S15   move L, ...                         # Robot motion

```