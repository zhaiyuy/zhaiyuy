基于DDPG的无人机的飞行决策
====
##### 翟玉媛 21S053088 ；刘锡诚 21S153125

仿真环境
-----
 * Airsim
 * Pycharm
 * UE4
 
环境依赖
-----
 * cv
 * numpy
 * time
 * os
 * matplotlib
 * python3.6
 * pytorch1.6
 
代码介绍
-----
### 重要变量介绍
 DDPG_for_obstacle_avoidance.py包含了算法的所有功能，其中
  * class ReplayMemory定义了经验回放池的大小、样本采样方式等；
  * class ENV 定义了奖励函数的计算、RGB图像到灰度图像的转换；
  * class Actor(nn.Module)定义了Actor网络结构以及输入输出；
  * class Critic(nn.Module)定义了Critic网络结构以及输入输出；   
  * class DDPG(object)定义了DDPG算法输入输出的格式和训练方式；
  * load_model是用于区分训练和测试的布尔值；
### 代码逻辑
  * (1) 初始化状态空间、动作空间，训练环境，获取一帧图像处理后复制堆叠为四帧图像信息，作为图像初状态
  * (2) 进入循环，循环次数为设定的最大回合数
  * (3) 通过当前状态获取动作量，并与环境交互。无人机接收动作后，以该动作运动0.5秒获取新的状态量，并根据新状态量计算奖励值大小。
  * (4) 将新状态量、执行动作后的奖励值，是否坠毁或完成任务等信息整合为训练环境返回数组
  * (5) 将当前状态与环境返回的数组数据组成四元组添加到经验池，即save_data_task.csv中
  * (6) 当经验池数据大于设定值时，开始从经验池中抽取数据训练，更新网络参数
  * (7) 更新状态信息（每次取当前时刻的前四帧图像信息），并返回第(2)步
  * (8) 当循环数超过最大回合数后，将episode reward存储到ereward.csv中，返回第(1)步
  * (9) 训练结束后，模型存储在episode0.pth中
  * (10)调用训练好的模型进行仿真
 ### 代码运行
 安装好Airsim和UE4后，在Pycharm中打开DDPG_for_obstacle_avoidance.py，点击运行即可。
 
仿真结果
-----
 详细的仿真结果可以在课程报告中查看。

