# 1. System类

多数情况下，都需要下述内容，建议直接全部载入.   

+ Microsoft.Bcl.AsyncInterfaces.dll
+ Microsoft.Win32.Registry.dll
+ System.Buffers.dll
+ System.Collections.Immutable.dll
+ System.Memory.dll
+ System.Numerics.Vectors.dll
+ System.Runtime.CompilerServices.Unsafe.dll
+ System.Security.AccessControl.dll
+ System.Security.Principal.Windows.dll
+ System.Text.Encodings.Web.dll
+ System.Text.Json.dll
+ System.Threading.Tasks.Extensions.dll

序列化工具也可选，但注意框架中使用System.Text.Json，两者可同时存在：

+ Newtonsoft.Json.dll

# 2. SangoUtils拓展

多数情况下，都需要下述内容，建议直接全部载入.   
默认后续章节提到的拓展，均为已经导入下述dll的结果.  

+ SangoUtils.CustomEditors_Unity.dll
+ SangoUtils.UnitySourceGenerators.dll

下述内容可能会与部分sdk产生冲突问题，不建议直接导入，可以使用导入.cs的方式使用.

+ SangoUtils.Behaviours_Unity.dll

# 3. sdk拓展
## 3.1 Rokid拓展

Rokid需要4个文件，可直接导入响应的.unitypackage包