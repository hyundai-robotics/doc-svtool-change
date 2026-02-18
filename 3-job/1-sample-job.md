# 3.1 工具更换附加/分离示例




```python
S10   move L, ...                         # 移动到伺服工具释放位置
      toolchng off,tg=G1                  # 执行伺服工具断开
                                          # 伺服工具断开输出（专用输出）
      do11 = 1                            # 输出ATC凸轮打开信号
      wait di11                           # 等待ATC凸轮打开确认信号

S11   move L, ...                         # 机器人运动
S12   move L, ...                         # 机器人运动
S13   move L, ...                         # 机器人运动

S14   move L, ...                         # 移动到伺服工具连接位置
      wait di12                           # 等待工具连接准备信号
      do11 = 0                            # 输出ATC凸轮关闭信号
      toolchng on,tg=G1,di=1              # 执行伺服工具的机械连接
                                          # 伺服工具连接过程

S15   move L, ...                         # 机器人运动

```