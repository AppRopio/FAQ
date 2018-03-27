# AppDelegate

Пример класса `AppDelegate` для приложения, использующего в качестве основной навигации левое меню.

```
[Register("AppDelegate")]
public class AppDelegate : ARApplicationDelegate
{
    protected override MvxAsyncIosSetup CreateSetup(IMvxApplicationDelegate appDelegate, MvxIosViewPresenter presenter)
    {
        return new Setup(appDelegate, presenter);
    }

    protected override MvxIosViewPresenter CreatePresenter(IMvxApplicationDelegate appDelegate, UIWindow window)
    {
        return new MenuNavigationPresenter(this, Window);
    }

    protected override UIViewController ConstructDefaultViCo()
    {
        var viCo = base.ConstructDefaultViCo();
        viCo.View.BackgroundColor = Theme.ColorPalette.Background.ToUIColor();
        return viCo;
    }	 
}
```

Метод `CreateSetup` используется для создания экземпляра класса `Setup` , в котором осуществляется настройка UI . проекта и создается `Application` . Этот метод может быть использован для создания собственного класса `Setup` , если ты используешь подход [разработки ядра](/ru/dorabotka-suschestvuyuschego-proekta/razrabotka-yadra.md).

Метод `CreatePresenter` используется для получения экзепляра презентера, реализующего в себе логику навигации между экранами. Здесь можно вернуть экземпляр своего презентера, если предоставляемый презентер не устраивает.

Метод `ConstructDefaultViCo` используется для создания экрана, отображаемого после скрытия `SplashScreen` \(или `LaunchScreen` \). Это необходимо, так как время выхода из метода `FinishedLaunching` ограничено и так как инициализация всех модулей и MvvmCross происходит асинхронно \(во время отображения этого экрана\).

