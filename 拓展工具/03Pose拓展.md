# 1. 基本原则

AR应用中，sdk一般均提供Pose参数， 故应尽可能利用Pose，后对刚体进行控制.   
由于部分sdk中含有Pose拓展，故需先行检查防止冲突，**建议** 直接导入PoseUtils.cs文件.

# 2 获取/设置Pose

+ Transform.GetPose()
+ Transform.SetPose()

## 3 Pose计算

+ PoseUtils.Lerp()