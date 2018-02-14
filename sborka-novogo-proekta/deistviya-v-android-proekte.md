# Подготовка Android проекта

* Проверить `AndroidManifest.xml` \(взять необходимые свойства из списка [здесь](/sborka-novogo-proekta/deistviya-v-android-proekte/androidmanifest.md)\)

* Удалить из проекта лишние файлы \(`MainActivity.cs`\) и папки (`Resources`)

* Подключить папку с ресурсами (скачать можно [отсюда](https://1drv.ms/u/s!Aqo42ClDiE2fibJ46aMbyqhFktXj8w))

  * Поменять название темы на заданную в `AndroidManifest.xml` ранее
  
  * Проверить в `strings.xml` название приложения 
  
  * Изменить в `Resource.designer.cs` namespace и значение `fullName` в атрибуте `ResourceDesignerAttribute` на корректные
  
  * Изменить `AppAttributesValues.xml`:
  
    * изменить цветовую палитру
    
    * изменить палитру шрифтов, не забыв изменить `fonts.xml` [опционально] 
    
    * изменить палитру контролов [опционально] 
    
* Добавить в проект файлы:

  * [LinkerPleaseInclude.cs](/sborka-novogo-proekta/deistviya-v-android-proekte/linkerpleaseinclude.md)
  
  * [Application.cs](/sborka-novogo-proekta/deistviya-v-android-proekte/application.md)
  
  * [SplashActivity.cs](/sborka-novogo-proekta/deistviya-v-android-proekte/splashactivity.md)
  
  * [Setup.cs](/sborka-novogo-proekta/deistviya-v-android-proekte/setup.md)

* Подключить dll'ки в соответствии со списком модулей и настроек \(таблицу соответствия между библиотеками и модулями можно найти [здесь](/perechen-bibliotek-modulei.md)\)

  * Добавить Bootstrap-файлы для каждого модуля

  * В папку `Assets` добавить папку `Settings/Configs` с конфигурационными файлами для **ядра** каждого модуля

  * Подключить требуемые пакеты \(список основных пакетов можно найти [здесь](/sborka-novogo-proekta/spisok-paketov.md)\)

* Проверить сборку и запуск проекта на симуляторе

* Заменить иконки на корректные, если требуется

* Запросить ApiKey и иденификатор компании \(подробная [инструкция](/sborka-novogo-proekta/zapros-litsenzii.md)\)



