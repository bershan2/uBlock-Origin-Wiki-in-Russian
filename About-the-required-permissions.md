# О необходимых разрешениях в Chromium
Перевод на русский язык оригинала [_About the required permissions_](https://github.com/gorhill/uBlock/wiki/About-the-required-permissions) от 8 июня 2015.

### Необходимые разрешения (в Chromium) для работы uBlock

uBlock требует такие-же разрешения что и [Privacy Badger](https://www.eff.org/privacybadger), разве что Privacy Badger также запрашивает ещё одно разрешение -- куки (`cookies`). Вот перечень разрешений необходимых для работы uBlock:

    "permissions": [
        "contextMenus",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "http://*/*",
        "https://*/*"
    ],

[`"privacy"`](https://developer.chrome.com/extensions/privacy) -- это единственное разрешение добавленное начиная с [ версии 0.9.8.2](https://github.com/gorhill/uBlock/releases/tag/0.9.8.2). Все прочие разрешения требовались с первого релиза uBlock (кроме `"contextMenus"`, который был добавлен для поддержки возможности блокировать элементы через контекстное меню).

Разрешение `privacy` необходимо чтобы uBlock отключил функцию "Использовать подсказки для ускорения загрузки страниц" (англ. "Prefetch resources to load pages more quickly"). Это полностью предотвращает установление соединения для всех заблокированных запросов, защищая Вашу приватность.

Вот перечень разрешений необходимых для работы Privacy Badger:

    "permissions": [
        "contextMenus",
        "cookies",
        "privacy",
        "storage",
        "tabs",
        "unlimitedStorage",
        "webNavigation",
        "webRequest",
        "webRequestBlocking",
        "http://*/*",
        "https://*/*"
    ],

### "Просмотр и изменение ваших данных на посещаемых сайтах" (англ. "Access your data on all web sites")

Это разрешение требовалось ещё в [начальной версии](https://github.com/gorhill/uBlock/blob/b5fdac90539b19a0db8f36ea537bd150edb4d9c8/manifest.json).

- Необходимо для проверки всех сетевых запросов чтобы прерывать их в случае необходимости.
    - Только для http и https- сетевых адресов.

Смотрите код:

- [chrome.webRequest](https://github.com/gorhill/uBlock/search?q=%22chrome.webRequest%22&type=Code)

###  (англ. "Access your tabs and browsing activity")

Требуется начиная с [первой версии](https://github.com/gorhill/uBlock/blob/b5fdac90539b19a0db8f36ea537bd150edb4d9c8/manifest.json).

Это разрешение необходимо чтобы:

- Открывать новые вкладки (при нажатии на название списка фильтров чтобы показывать их содержимое)
- Обнаруживать добавление и закрытие вкладок
- Обновлять значок
- Очищать память от устаревших внутренних структур данных
- Знать, какая вкладка активна в настоящий момент (чтобы вставлять во всплывающее меню соответствующие статистику и/или настройки)
- Вставлять скрипт инструмента выбора элементов
- Блокировать всплывающие окна

См. исходный код:

- [chrome.tabs](https://github.com/gorhill/uBlock/search?q=%22chrome.tabs%22&type=Code)
- [chrome.webNavigation](https://github.com/gorhill/uBlock/search?q=%22chrome.webNavigation%22&type=Code)

### (англ. "Change your privacy-related settings")

Требуется начиная с [версии 0.9.8.2](https://github.com/gorhill/uBlock/commit/e65c2939757f09db646d277b82da8690aaf3adbc) ([лог измнений](https://github.com/gorhill/uBlock/releases/tag/0.9.8.2)).

Это разрешение необходимо чтобы:

- Отключить (англ. _"Prefetch resources to load pages more quickly"_)
    - Это **полностью** предотвращает установление TCP соединения  для заблокированных запросов: **Эта настройка засчищает Вашу конфиденциальность.**<sup>[1]</sup>
    - На страницах с большим количеством заблокированных запросов эта настройка даже уменьшает нагрузку при загрузке страницы (если у вас еще не установлен этот параметр).
    - When uBlock blocks a network request, the expectation is that it blocks **completely** the connection, hence the new permission is necessary for uBlock to do **truthfully** what it says it does.
- Отключить [hyperlink auditing/beacon](http://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/) (0.9.8.5)

Основная задача uBlock -- это блокировать **сетевые соединения**, а не только передачу данных. В противном случае, не предотвращая соединение, а только передачу данных, uBlock вводил бы в заблухдение пользователей. Поэтому это разрешение будет необходимо и в будущем, хотя мне (автору, Raymond Hill -- прим. переводчика) и жаль тех кто не понимает что оно позволяет uBlock лучше выполняться свою функцию<sup>[2]</sup>. Блокировщик, не способный полностью предотвратить установление соединения, не выполняет свою основную функцию.

**Privacy Badger также запрашиевает эти же разрешения.** Я (Raymond Hill -- прим. переводчика) хочу чтобы uBlock помогал пользователям заботящимся о приватности в первую очередь.

Если (англ. _prefetching_)  had been disabled by default, this new permission would not be needed, but _prefetching_ is unfortunately enabled by default, and under _Privacy_ heading, which is itself hidden by default under _"advanced settings"_, and even at this point, you would still have to dig to find out the [negative side effects of prefetching](https://wikipedia.org/wiki/Link_prefetching#Issues_and_criticisms) (related: [dark patterns](https://darkpatterns.org/)).

![c](https://cloud.githubusercontent.com/assets/585534/7914528/924b9314-0845-11e5-8012-f67e4b1814cd.png)

Also, the benefits of _prefetching_ are probably marginal, and in the context of a blocker, the benefits could be negative, since a lot of useless connections would be made, just to be discarded after the browser find out the requests won't be made anyway. So do not fall for the _"lost of major performance boost"_ claim I read elsewhere, this is just a silly and baseless claim.

**Edit:** actually, prefetching is worst than I first thought, I had tested that it was just a connection issue, but [as per Google](https://support.google.com/chrome/answer/1385029):

> If you turn this setting on in Chrome, websites (and any of their embedded resources) that are prerendered or prefetched may set and read their own cookies as if you had visited them before -- even if you don’t visit the prerendered or prefetched pages after all.

See code:

- [chrome.privacy.network](https://github.com/gorhill/uBlock/commit/e65c2939757f09db646d277b82da8690aaf3adbc)

<sub>[1] Само по себе установление TCP соединения риводит к утечке Вашего IP аддресса на удаленный сервер -- это неприемлемо this is incompatible with an extension which primary purpose is to **completely** prevent connections to remove server, not just merely prevent the transfer of data. For instance, [see what can be found](https://www.browserleaks.com/whois) with a just that connection being established (IP, OS Fingerprinting, IP Address Location).</sub>

<sub>[2] In version 0.9.8.3, there will be [a setting to allow re-enabling prefetching](https://github.com/gorhill/uBlock/issues/274), default will still be  to disable it though.
</sub>
