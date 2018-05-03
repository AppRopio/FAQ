# payments

Как и при подключении любого модуля к проекту необходимо проверить наличие bootstrap-файла \(и добавить при необходимости\), который отвечает за инициализацию модуля \(то есть "запускает" его работу\).

Помимо этого, необходимо добавить ссылки на все библиотеки `AppRopio.Payments.*.dll` \(подробнее [здесь](https://github.com/appropio/faq/tree/01a74964a039dfb9acb17ee3a5d97021d54f864c/perechen-bibliotek-modulei.md)\) и выбрать провайдера эквайринга \(с подключением соответствующих библиотек\)

**ВНИМАНИЕ**

При наличии подключенного модуля "Корзина" **обязательным** условием работы модуля оплаты является регистрация этого модуля в конфигурационном файле модуля "Корзина".

Пример:

```javascript
{
    ...
    "inAppPayments": {
        "all": {
            "typeName": "AppRopio.Payments.{ProviderName}.{ProjectName}.{EntryPointName}",
            "assemblyName": "AppRopio.Payments.{ProviderName}.{ProjectName}"
        }
    },
    ...
}
```

## CloudPayments

* Добавить ссылки на библиотеки \(подробнее [здесь](https://github.com/appropio/faq/tree/01a74964a039dfb9acb17ee3a5d97021d54f864c/perechen-bibliotek-modulei.md)\)
* Добавить bootstrap
* Добавить Configs/CloudPayment.json \(подробнее [здесь](payments-cloudpayments-config.md)\)
* _\[опционально\] Зарегистрировать в Configs/Basket.json \(подробнее _[_здесь_](payments-cloudpayments-basketconfig.md)_\)_

## ApplePay

* Добавить ссылки на библиотеки \(подробнее [здесь](https://github.com/appropio/faq/tree/01a74964a039dfb9acb17ee3a5d97021d54f864c/perechen-bibliotek-modulei.md)\)
* Добавить bootstrap
* Добавить Configs/ApplePay.json \(подробнее [здесь](payments-applepay-config.md)\)
* Зарегистрировать merchantId на [developer.apple.com](https://developer.apple.com)
* Добавить в AppID возможность оплаты ApplePay
* Перевыпустить Provision Profiles для приложения
* Добавить merchantId в `Entitlements.plist`

