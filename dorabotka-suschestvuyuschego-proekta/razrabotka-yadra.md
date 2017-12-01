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

Теперь необходимо создать и зарегистрировать класс `RouterSubscriber` . Подробную инструкцию можно найти [здесь](/dorabotka-suschestvuyuschego-proekta/routersubscriber.md).

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



