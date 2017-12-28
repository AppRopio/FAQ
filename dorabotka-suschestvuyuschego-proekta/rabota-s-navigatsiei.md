# Как работать с навигацией между экранами

Платформа AppRopio использует последние версии пакетов MvvmCross, поэтому принципы работы с навигацией всегда совпадают с принципами, указанными в актуальной документации MvvmCross. Здесь мы рассмотрим некоторые особенности работы с `NavigationVmService`.

## ViewModel

В текущей версии MvvmCross (5.5+) рекомендуется использовать `MvxNavigationService` для осуществления навигации между VM. Этот сервис изменяет последовательность и сами методы, вызывающиеся при создании ViewModel, зато позволяет передать в ViewModel параметр напрямую, не используя сериализацию/десериализацию.
Для реализации универсального параметра навигации, в AppRopio используется `IMvxBundle` в качестве параметра для навигации между `ViewModel`. Это значит, что тебе не нужно использовать наследование от `MvxViewModel<TParameter>`, достаточно создать объект, реализующий интерфейс `IMvxBundle` и использовать его в качестве необходимого параметра в соответствующем `NavigationVmService`.
Принимать параметр, переданный при навигации необходимо в методе `Prepare(IMvxBundle parameter)`, например, как показано в коде ниже:

```
public override void Prepare(IMvxBundle parameters)
{
    base.Prepare(parameters);

    var navigationBundle = parameters.ReadAs<NavigationBundle>();
    this.InitFromBundle(navigationBundle);
}

protected virtual void InitFromBundle(NavigationBundle parameters)
{
    VmNavigationType = parameters.NavigationType == NavigationType.None ?
                                                    NavigationType.ClearAndPush :
                                                    parameters.NavigationType;

    _id = parameters.Id;
}
```


