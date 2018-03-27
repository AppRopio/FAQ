# SplashActivity

```csharp
[Activity(MainLauncher = true,
    NoHistory = true,
    ScreenOrientation = ScreenOrientation.Portrait)]
public class SplashActivity : CommonSplashScreenActivity
{
    public SplashActivity()
        : base (Resource.Layout.Splash)
    {
        
    }
}
```