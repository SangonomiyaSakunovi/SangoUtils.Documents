# 1. 基本原则

上位机与下位机均需运行，顺序任意.   
发送数据使用udp，上位机可修改interval，下位机循环监听即可.

# 2. Unity下位机端

需要引入com.sangoutils.htcvivetrackerhelper包.

## 2.1 TrackerDataReceiver

在Inspector面板订阅事件，注意必须调整Position与Rotation映射.    
已知的映射有：  
+ Tracking Reference Channel B: front, Tracking Reference Channel C: Left.    
Position: -x, y, z.     
Rotation: -z, -y, x, w.

# 3. Python上位机端
## 3.1 运行前检查

检查Tracking Reference与Tracker的连接情况，需要确保均被发现.

## 3.2 运行

直接运行run.bat