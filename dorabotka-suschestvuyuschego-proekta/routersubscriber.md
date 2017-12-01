# RouterSubscriber

Сейчас необходимо создать обработчик, который будет являться точкой входа для модуля навигации. Этот обработчик называется `RouterSubscriber`

```
using System;
using AppRopio.Base.Core.Models.Bundle;
using AppRopio.Base.Core.Models.Navigation;
using AppRopio.Base.Core.Services.Router;

namespace ProjectName.Core.Services.Implementations
{
    public class RouterSubscriber : AppRopio.Base.Core.RouterSubsriber
    {
        public override bool CanNavigatedTo(string type, BaseBundle bundle = null)
        {
            var vm = LookupService.Resolve(type);
            ShowViewModel(vm, new BaseBundle(NavigationType.ClearAndPush));

            return true;
        }

        public override void FailedNavigatedTo(string type, BaseBundle bundle = null)
        {
            //nothing
        }
    }
}
```

В самом простом случае `RouterSubscriber` всего лишь получает тип класса `ViewModel`, зарегистрированной для текущего `type` и выполняет навигацию на него, используя стандартные механизмы MvvmCross. Однако возможности `RouterSubscriber` на этом не ограничиваются, потому что принимаемый им `type` не обязательно должен быть типом какой-либо `ViewModel`, это может быть тип любого класса \(или любая строка\), который поможет определить порядок действий при навигации в модуль. Помимо этого, в `RouterSubscriber` также могут придти параметры для первичной инициализации \(параметр `bundle`\). Это может потребоваться в случаях, когда модуль зависит от текущих настроек запущенного приложения \(например, модуль оплаты будет принимать через этот параметр информацию о заказе\).

После создания `RouterSubscriber` его необходимо зарегистрировать в соответствующем сервисе. В зависимости от выбранного подхода к разработке классы для регистрации будут немного отличаться. Но в обоих случаях нужно переопределить в `App.cs` метод `Initialize`

#### Разработка ядра

```
public class App : AppRopio.***.Navigation.Core.App
{
    public override Initialize()
    {
        base.Initialize();
        
        Mvx.CallbackWhenRegistered<IRouterService>((service) => router.Register<Type>(new RouterSubscriber()));
    }
}
```

#### Разработка плагина

```
public class App : MvvmCross.Core.ViewModels.MvxApplication
{
    public override Initialize()
    {
        base.Initialize();
        
        Mvx.CallbackWhenRegistered<IRouterService>((service) => router.Register<Type>(new RouterSubscriber()));
    }
}
```

Регистрацию **обязательно** надо выполнять через callback по регистрации сервиса `IRouterService`, так как все плагины и сам MvvmCross стартуют асинхронно и нет гарантии что к моменту старта твоего ядра все сервисы будут зарегистрированы.

