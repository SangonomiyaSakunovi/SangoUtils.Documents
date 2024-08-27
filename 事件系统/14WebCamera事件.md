# 1. 基本原则

只适用于USB相机， 必须提前连接好相机防止出错。

# 2. Unity端

需要引入com.sangoutils.htcvivetrackerhelper包。

## 2.1 WebCameraUGUI

在Inspector面板可以修改对应参数，注意有两种渲染方式。

### 2.1.1 Canvas+RawImage

推荐使用的方式，需要场景中下述组件：

1) Canvas：     
(1) RenderMode为Screen Space - Camera   
(2) 拖拽为Render Camera赋值     


2) Camera:      
(1) Render Type为Base    
(2) Physical Camera为True  
(3) Environment中Background Type为Solid Color       
