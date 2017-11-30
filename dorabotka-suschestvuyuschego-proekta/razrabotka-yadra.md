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

Сейчас необходимо создать обработчик, который будет являться точкой входа для модуля навигации. Этот обработчик называется `RouterSubscriber`

```
namespace ProjectName.Core.Services.Implementations
{
    public class RouterSubscriber : AppRopio.Base.Core.RouterSubsriber
    {
        public override bool CanNavigatedTo(string type, BaseBundle bundle = null)
        {
            var vm = LookupService.Resolve<IViewModel>();
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



