# Разработка ядра

При выборе этого способа, необходимо создать в проекте трехзвенную архитектуру:

* API
* CORE
* UI

Так как UI проекты уже созданы, требуется лишь создать API \(будет отвечать за взаимодействие с сервером\) и CORE \(содержит всю бизнес-логику\) проекты типа Portable Class Library.

Теперь необходимо подключить в эти проекты пакеты MvvmCross \(соответствующие версии можно взять [здесь](/sborka-novogo-proekta/spisok-paketov.md)\) и добавить ссылки на [базовые библиотеки AppRopio](/perechen-bibliotek-modulei.md).

Чтобы ядро запустилось, необходимо создать в нем собственный `Application` \(`App.cs`\) и наследовать его от `App.cs` из пакета подключенной сейчас навигации:

```
public class App : AppRopio.***.Navigation.Core.App
{
    ...
}
```

## RouterSubscriber

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

После создания `RouterSubscriber` его необходимо зарегистрировать в соответствующем сервисе. Для этого нужно переопределить в `App.cs` метод `Initialize`

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

Регистрацию **обязательно** надо выполнять через callback по регистрации сервиса `IRouterService`, так как все плагины и сам MvvmCross стартуют асинхронно и нет гарантии что к моменту старта твоего ядра все сервисы будут зарегистрированы.

## Setup

Следующим шагом необходимо создать в UI проекте файл `Setup.cs` , в котором будет осуществляться настройка UI проекта, а также будет создаваться инстанс приложения из твоего ядра. Этот класс должен быть наследован от соответствующего класса в выбранном модуле навигации:

```
public class Setup : AppRopio.***.Navigation.***.App
{
    public Setup(IMvxApplicationDelegate navDelegate, MvxIosViewPresenter presenter) 
    : base(navDelegate, presenter)
    {
    }

    ...
}
```

Теперь необходимо в `Setup` переопределить метод `CreateApp` и вернуть в нем созданный инстанс класса приложения, который мы добавили в CORE в самом начале.

```
public class Setup : AppRopio.***.Navigation.***.App
{
    public Setup(IMvxApplicationDelegate navDelegate, MvxIosViewPresenter presenter) 
    : base(navDelegate, presenter)
    {
    }

    protected override MvvmCross.Core.ViewModels.IMvxApplication CreateApp()
    {
        return new Core.App();
    }
}
```

Таким образом мы даем MvvmCross'у инстанс приложения, который он будет использовать в дальнейшем.

Осталось только прописать в классе `AppDelegate` в методе `CreateSetup` создание экземпляра класса `Setup` , заменив текущую реализацию. Подробнее узнать о методах класса `AppDelegate` и их назначении можно [здесь](/sborka-novogo-proekta/deistviya-v-ios-proekte/appdelegate.md).

На этом заканчивается подготовительная работа, можно начинать описывать бизнес-логику приложения.

## Дополнительные материалы

* [Создание и разработка экранов](/dorabotka-suschestvuyuschego-proekta/razrabotka-ekranov.md)
* [Навигация между экранами](/dorabotka-suschestvuyuschego-proekta/rabota-s-navigatsiei.md)
* [Работа с темой](/dorabotka-suschestvuyuschego-proekta/rabota-s-temoi-proekta.md)



