# Подготовка Android проекта

* Проверить `AndroidManifest.xml` \(взять необходимые свойства из списка [здесь](/sborka-novogo-proekta/deistviya-v-android-proekte/androidmanifest.md)\)

* Удалить из проекта лишние файлы \(`MainActivity.cs`\) и папки (`Resources`)

* Подключить папку с ресурсами (скачать можно [отсюда](https://1drv.ms/u/s!Aqo42ClDiE2fibJ46aMbyqhFktXj8w))

  * Поменять название темы на заданную в `AndroidManifest.xml` ранее
  
  * Проверить в `strings.xml` название приложения 
  
  * Изменить `AppAttributesValues.xml`:
  
    * изменить цветовую палитру
    
    * изменить палитру шрифтов, не забыв изменить `fonts.xml` [опционально] 
    
    * изменить палитру контролов [опционально] 
    
* Добавить в проект

* Подключить dll'ки в соответствии со списком модулей и настроек \(таблицу соответствия между библиотеками и модулями можно найти [здесь](/perechen-bibliotek-modulei.md)\)

  * Добавить Bootstrap-файлы для каждого модуля

  * Добавить папку `Settings` с конфигурационными файлами для ядра и для темы каждого модуля

  * Подключить требуемые пакеты \(список основных пакетов можно найти [здесь](/sborka-novogo-proekta/spisok-paketov.md)\)

  * Подключить пакет иконок \(полный пакет иконок можно скачать [отсюда](/Images.zip)\)

* Добавить в проект [LinkerPleaseInclude.cs](/sborka-novogo-proekta/deistviya-v-ios-proekte/linkerpleaseinclude.md)

* Добавить `--linkskip=MvvmCross --linkskip=MvvmCross.Core --linkskip=MvvmCross.Binding --linkskip=MvvmCross.Platform` в аргументы mtouch запускаемого проекта![](/sborka-novogo-proekta/deistviya-v-ios-proekte/add mtouch arguments.png)

* Изменить `AppDelegate` \(наследовать от `ARApplicationDelegate` и переопределить методы `CreateSetup` и `CreatePresenter` , [пример](/sborka-novogo-proekta/deistviya-v-ios-proekte/appdelegate.md)\)

* Добавить в проект постзагрузочный индикатор \([loader.html](/sborka-novogo-proekta/deistviya-v-ios-proekte/loader.html) со свойством `BuildAction` установленным в `BundleResource` \)

* Подключить в `Assets.xcassets` иконки приложения для отображения на рабочем столе и в системе и загрузочный экран \(`LaunchScreen.xib` с картинкой, добавленной в Assets через Image Set\)![](/sborka-novogo-proekta/deistviya-v-ios-proekte/add image set.png)

* Проверить сборку и запуск проекта на симуляторе

* Настроить цветовую схему \([работа с темой проекта](/dorabotka-suschestvuyuschego-proekta/rabota-s-temoi-proekta.md)\), проверить и перекрасить пакет иконок \(иконки берутся из дизайна\)

* Запросить ApiKey и иденификатор компании \(подробная [инструкция](/sborka-novogo-proekta/zapros-litsenzii.md)\)



