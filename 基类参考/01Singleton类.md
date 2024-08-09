# 1. C#项目

```cs
public abstract class Singleton<T> where T : class
{
    private static T? _instance;
    private static readonly object _lock = new object();

    public static T Instance
    {
        get
        {
            if (_instance == null)
            {
                lock (_lock)
                {
                    _instance = Activator.CreateInstance<T>();
                }
            }
            return _instance;
        }
    }
}
```

# 2. Unity项目

该基类存在继承深度问题，建议优先考虑Source Generator，见 **语法事件** 章节.

```cs
public abstract class UnitySingleton<T> : MonoBehaviour where T : MonoBehaviour
{
    private static T? _instance;

    public static T Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = FindObjectOfType(typeof(T)) as T;
                if (_instance == null)
                {
                    GameObject gameObject = new GameObject("[" + typeof(T).FullName + "]");
                    _instance = gameObject.AddComponent<T>();
                    gameObject.hideFlags = HideFlags.HideInHierarchy;
                    DontDestroyOnLoad(gameObject);
                }
            }
            return _instance;
        }
    }

    private void Awake()
    {
        if (_instance != null && _instance != this)
        {
            Destroy(gameObject);
        }
    }
}
```