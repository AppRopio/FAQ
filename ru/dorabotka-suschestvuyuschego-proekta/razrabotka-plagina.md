# Разработка плагина

При выборе этого способа, необходимо создать в проекте создать отдельную `Solution Folder` по имени модуля, в которой создать следующие проекты:

* ModuleName.Models
* ModuleName.API
* ModuleName.Core
* ModuleName.iOS
* ModuleName.Droid

Models \(модели, которые используются для клиент-серверного взаимодействия\), API \(будет отвечать за взаимодействие с сервером\) и CORE \(содержит всю бизнес-логику\) проекты типа Portable Class Library.

Теперь во все проекты, кроме Models, необходимо добавить NuGet пакет MvvmCross \(поддерживаемую версию можно взять [здесь](/sborka-novogo-proekta/spisok-paketov.md), добавлять нужно только MvvmCross пакет, не учитывая пока плагинов и других пакетов\) и добавить ссылки на [базовые библиотеки AppRopio](/perechen-bibliotek-modulei.md).

## Настройка Core

В ядро проекта необходимо добавить два класса: `App.cs` и `PluginLoader`

Чтобы ядро запустилось, необходимо создать в нем собственный `Application` \(`App.cs`\):

```
public class App : MvvmCross.Core.ViewModels.MvxApplication
{
    ...
}
```

В этом классе выполняется регистрация сервисов и `ViewModel` , использующихся в Core.

Сейчас необходимо создать класс `PluginLoader` – это загрузчик плагина, который вызывается MvvmCross в момент инициализации всех плагинов и в котором происходит инициализация `App`:

```
public class PluginLoader : IMvxPluginLoader
{
    public static readonly PluginLoader Instance = new PluginLoader();

    private bool _loaded;

    public void EnsureLoaded()
    {
        if (_loaded)
            return;

        new App().Initialize();

        new API.App().Initialize();

        new App().Initialize();
        
        var manager = Mvx.Resolve<IMvxPluginManager>();
        manager.EnsurePlatformAdaptionLoaded<PluginLoader>();

        MvxTrace.Trace(MvxTraceLevel.Diagnostic, $"{PluginName} plugin is loaded");

        _loaded = true;
    }
}
```

### RouterSubscriber

Теперь нужно создать и зарегистрировать класс `RouterSubscriber`. Подробную инструкцию можно найти [здесь](routersubscriber.md).

## Настройка UI

В UI проектах необходимо создать класс `Plugin` , в котором будут регистрироваться все View, а также сервис для работы с UI-темой модуля:

```
public class Plugin : IMvxPlugin
{
    public void Load()
    {
        ...
    }
}
```

### Bootstrap.cs

Финальный шаг настройки модуля – добавление в запускаемый UI проект bootstrap-файла, который будет связывать классы `PluginLoader` и `Plugin` , а также регистрировать их в MvvmCross

```
public class PluginName_PluginBootstrap 
        : MvxLoaderPluginBootstrapAction<PluginLoader, Plugin>
    {
    }
```

## Дополнительные материалы

* [Создание и разработка экранов](razrabotka-ekranov.md)
* [Навигация между экранами](rabota-s-navigatsiei.md)
* [Работа с темой](rabota-s-temoi-proekta.md)



