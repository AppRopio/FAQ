# deistviya-v-android-proekte

* Удалить из проекта лишние файлы \(`MainActivity.cs`\) и папки \(`Resources`\)
* Подключить папку с ресурсами \(скачать можно [отсюда](https://1drv.ms/u/s!Aqo42ClDiE2fibJ46aMbyqhFktXj8w)
  * Проверить в `strings.xml` название приложения
  * Изменить в `Resource.designer.cs` namespace и значение `fullName` в атрибуте `ResourceDesignerAttribute` на корректные
  * Изменить `AppAttributesValues.xml`:
    * изменить цветовую палитру
    * изменить палитру шрифтов, не забыв изменить `fonts.xml` \[опционально\]
    * изменить палитру контролов \[опционально\]
* Подключить папку с локализацией
* Проверить `AndroidManifest.xml` \(взять необходимые свойства из списка [здесь](androidmanifest.md)\)
* Поменять название темы в ресурсах на заданную в `AndroidManifest.xml` ранее
* Подключить dll'ки в соответствии со списком модулей и настроек \(таблицу соответствия между библиотеками и модулями можно найти [здесь](https://github.com/appropio/faq/tree/01a74964a039dfb9acb17ee3a5d97021d54f864c/perechen-bibliotek-modulei.md)\)
  * Добавить Bootstrap-файлы для каждого модуля
  * В папку `Assets` добавить папку `Settings/Configs` с конфигурационными файлами для **ядра** каждого модуля
  * Подключить требуемые пакеты \(список основных пакетов можно найти [здесь](../spisok-paketov.md)\)
* Добавить в корень проекта файлы:
  * [LinkerPleaseInclude.cs](linkerpleaseinclude.md)
  * [Application.cs](application.md)
  * [SplashActivity.cs](splashactivity.md)
  * [Setup.cs](setup.md)
* Проверить сборку и запуск проекта на симуляторе
* Заменить иконки на корректные, если требуется
* Запросить ApiKey и иденификатор компании \(подробная [инструкция](../zapros-litsenzii.md)\)
* Запросить подключение к билд-серверу или корректировку его параметров

