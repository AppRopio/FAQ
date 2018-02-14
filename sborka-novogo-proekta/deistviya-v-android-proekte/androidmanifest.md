# AndroidManifest.xml

## Проверить название пакета

`Package name` должен быть представлен в соответствии с маской `com.notissimus.{имя_приложения}.{название_платформы}`

## Указать иконку приложения

В поле `Application icon` прописать следующее: `@drawable/icon_name`, где `icon_name` – название твоей иконки приложения

## Указать тему приложения

В поле `Application theme` прописать: `@style/Theme.Name`, где `Name` – названии темы приложения, обычно совпадающее с названием приложения. Подробнее про создание темы приложения смотри [здесь](/sborka-novogo-proekta/deistviya-v-android-proekte/sozdanie-temi-prilozheniya.md)

## Версия Android

Minimum Android version: 5.0 (API level 21)
Target Android version: Automatic
Target framework: use latest installed platform

## Разрешения

Добавить в код `AndroidManifest.xml` между тегами `<manifest>` следующий код:

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
```

## Добавить ключ карт Google

Добавить в код `AndroidManifest.xml` между тегами `<application>` следующий код:

```xml
<meta-data android:name="com.google.android.geo.API_KEY" android:value="api_key" />
```

Подробнее про получения ключа [здесь](https://developers.google.com/maps/documentation/android-api/signup?hl=ru)

## Итоге

В итоге манифест должен выглядеть примерно так:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" android:versionCode="1" android:versionName="1.0" package="com.notissimus.app_name.platform_name">
	<uses-sdk android:minSdkVersion="21" android:targetSdkVersion="26" />
	<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
	<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.INTERNET" />
	<application android:allowBackup="true" android:label="@string/app_name" android:theme="@style/Theme.Name" android:icon="@drawable/icon_name">
		<meta-data android:name="com.google.android.geo.API_KEY" android:value="api_key" />
	</application>
</manifest>
```