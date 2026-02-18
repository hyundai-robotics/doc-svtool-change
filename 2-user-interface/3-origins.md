# 2.3 轴原点

系统管理每个伺服电机的轴原点位置。

导航路径：
`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 3: 轴原点 ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 3: Axis Home Position)`

<p align="center">
 <img src="../_assets/fig2_4_eng.png"></img>
 <em><p align="center">图 2.4 伺服工具轴原点设置</p></em>
</p>

<br>

当伺服工具连接时，相应的附加轴的原点位置会自动更新为分配给所选伺服工具的原点位置。
换句话说，配置在：
`[F2: 系统] - 4: 应用参数 - 11: 伺服工具更换 - 3: 轴原点 ([F2: System] - 4: Application Parameters - 11: Servo Tool Change - 3: Axis Home Position)`
的值会自动应用于：
`[F2: 系统] - 3: 机器人参数 - 2: 轴原点 ([F2: System] - 3: Robot Parameters - 2: Axis Home Position)`。

除了轴原点，以下参数也会自动更新为分配给连接的伺服工具的值：

- 对应附加轴的软限位  

- 编码器偏移  

- 伺服参数  

- 加速度/减速度参数  