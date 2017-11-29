# Описание ключей для Info.plist

## Основные значение

```
<key>UIViewControllerBasedStatusBarAppearance</key>
<false/>
<key>UIBackgroundModes</key>
<array>
   <string>remote-notification</string>
</array>
<key>NSLocationUsageDescription</key>
<string>Мы не передаем данные о вашей локации третьим лицам и используем их для вашего удобства</string>
<key>NSLocationAlwaysUsageDescription</key>
<string>Мы не передаем данные о вашей локации третьим лицам и используем их для вашего удобства</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>Мы не передаем данные о вашей локации третьим лицам и используем их для вашего удобства</string>
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>Мы не передаем данные о вашей локации третьим лицам и используем их для вашего удобства</string>
<key>NSCalendarsUsageDescription</key>
<string>Необходим для корректной работы приложения</string>
<key>NSAppTransportSecurity</key>
<dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
</dict>
<key>ITSAppUsesNonExemptEncryption</key>
<string>No</string>
<key>CFBundleDevelopmentRegion</key>
<string>ru</string>
```

## Подключение шрифтов

```
<key>UIAppFonts</key>
<array>
   <string>OPENSANS-BOLD.TTF</string>
   <string>OPENSANS-LIGHT.TTF</string>
   <string>OPENSANS-REGULAR.TTF</string>
   <string>OPENSANS-SEMIBOLD.TTF</string>
</array>
```

## Подключение OAuth через Вконтакте и Facebook

```
<key>CFBundleURLTypes</key>
<array>
   <dict>
      <key>CFBundleURLSchemes</key>
      <array>
         <string>vk{VK_ID}</string>
      </array>
   </dict>
   <dict>
      <key>CFBundleURLSchemes</key>
      <array>
         <string>fb{FB_ID}</string>
      </array>
   </dict>
</array>
<key>FacebookAppID</key>
<string>{FB_ID}</string>
<key>{FB_NAME}</key>
<string>AppropioTest</string>
<key>LSApplicationQueriesSchemes</key>
<array>
   <string>fbapi</string>
   <string>fb-messenger-api</string>
   <string>fbauth2</string>
   <string>fbshareextension</string>
   <string>vk</string>
   <string>vk-share</string>
   <string>vkauthorize</string>
</array>
<key>VkAppID</key>
<string>{VK_ID}</string>
```



