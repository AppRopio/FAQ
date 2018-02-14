# Сборка нового проекта на базе AppRopio

## Developer Console

### iOS

* Создать AppID в соответствии с маской `com.notissimus.{имя_приложения}.{название_платформы}`
* Создать Dev и Distr сертификаты, создать push-сертификаты

### Android

* Создать package name в соответствии с маской `com.notissimus.{имя_приложения}.{название_платформы}`
* Создать .keystore и получить Push Sender ID

## Репозиторий

* Склонировать AppRopio.Clients
* Создать новую ветку в соответствии с маской `{имя_проекта}/master`
* Создать решение с запускаемым проектом по пути `AppRopio.Clients/src/{имя_проекта}`
  * Маска имени запускаемого проекта `{имя_проекта}.{название_платформы}`
  * Маска имени решения `{имя_проекта}`

## Решение

* [Описание действий в iOS-проекте](/sborka-novogo-proekta/deistviya-v-ios-proekte.md)
* [Описание действий в Android проекте](/sborka-novogo-proekta/deistviya-v-android-proekte.md)



