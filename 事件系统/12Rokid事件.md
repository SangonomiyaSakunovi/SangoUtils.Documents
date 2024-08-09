# 1. 基本原则

需要引入com.sangoutils.enginesunity-rokiduxr包.

# 2. 手势回调事件

多数情况下需要 **先判断追踪到的手势数量**，减少bug.

```cs
internal class GestureBehaviour : MonoBehaviour
{
    private void Update()
    {
        NativeInterface.NativeAPI.GetTrackingHandNum();
        
        GesEventInput.Instance.GetGestureType(HandType.RightHand);
        GesEventInput.Instance.GetHandOrientation(HandType.RightHand);
        GesEventInput.Instance.GetSkeletonPose(SkeletonIndexFlag.WRIST, HandType.RightHand);
    }
}
```
# 3. 相机回调事件

Max Pro上面的灰度广角摄像头，**只能** 通过数据共享的方式拦截广播的事件.

```cs
internal class CameraBehaviour : MonoBehaviour
{
    private bool _isInit = false;

    private void Awake()
    {
#if UNITY_EDITOR
        return;
#endif
        NativeInterface.NativeAPI.StartCameraPreview();
    }

    private void Update()
    {
        NativeInterface.NativeAPI.GetHeadPose();
        
        if (!_isInit && NativeInterface.NativeAPI.IsPreviewing() && BaiduAI_LogoRecognitionsEventBus.IsInitialized)
        {
            Init();
        }
    }

    private void OnApplicationPause(bool pause)
    {
        if (pause)
        {
            Release();
        }
        else
        {
            NativeInterface.NativeAPI.StartCameraPreview();
        }
    }

    private void OnDestroy()
    {
        Release();
    }

    private void Init()
    {
        NativeInterface.NativeAPI.SetCameraPreviewDataType(2);
        NativeInterface.NativeAPI.OnCameraDataUpdate += OnCameraDataUpdate;

        _isInit = true;
    }

    private void OnCameraDataUpdate(int cameraWidth, int cameraHeight, byte[] cameraData, long timestamp)
    {
        Loom.QueueOnMainThread(() =>
        {
            //TODO
        });
    }

    private void Release()
    {
        if (_isInit)
        {
            NativeInterface.NativeAPI.OnCameraDataUpdate -= OnCameraDataUpdate;
            NativeInterface.NativeAPI.StopCameraPreview();
            NativeInterface.NativeAPI.ClearCameraDataUpdate();
            _isInit = false;
        }
    }
}
```

# 4. 交互回调事件

建议在Inspector面板订阅事件.