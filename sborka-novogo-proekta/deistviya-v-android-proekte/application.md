# Application

```csharp
[Application]
public class Application : Android.App.Application
{
    public Application(IntPtr handle, JniHandleOwnership transer)
        : base(handle, transer)
    {
    }
}
```