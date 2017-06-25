# Индивидуальные переключатели для каждого сайта
Перевод на русский язык оригинала [_Per site switches_](https://github.com/gorhill/uBlock/wiki/Per-site-switches) от 12 апреля 2017.

***

Индивидуальные переключатели позволяют менять некоторые настройки на каждом сайте отдельно.

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1g.png)

- [Блокировка всплывающих окон](#Блокировка-всплывающих-окон)
- [Блокировка больших медиа-элементов](#Блокировка-больших-медиа-элементов)
- [Отключение косметических фильтров](#Отключение-косметических-фильтров)
- [Блокировка сторонних шрифтов](#Блокировка-сторонних-шрифтов)

***

## Блокировка всплывающих окон

По умолчанию всплывающие окна разрешены, если для их блокировки не существует фильтра. Но если этот параметр включен, независимо от фильтров **все** всплывающие окна будут безоговорочно заблокированы на конкретном сайте:

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1i.png)<br><sup>Все всплывающие окна будут заблокированы: [Попробуйте сами.](http://jessehakanen.net/adblockpluspopupaddon/test.html)</sup>

Блокировка всплывающих окон зависит от наличия соответствующих фильтров во включённых списках фильтров, поэтому эта функция наиболее полезна, если сайт создает всплывающие окна, для которых нет правил в сторонних списках фильтров.

**Предостережение для браузеров основанных на Chromium:** Из-за ограничений Chromium API, _не всегда_ возможно точно определить является ли новая открытая вкладка всплывающим окном или же результатом обычного нажатия на ссылку пользователем. Поэтому при включённой блокировке всплывающих окон, _возможно_ Вы не сможете открыть ссылку в новый вкладке через контекстное меню.

***

## Блокировка больших медиа-элементов

Второй значок -- это включение/выключение блокировки больших медиа-элементов для текущего сайта. Основная цель этой функции -- уменьшить нагрузку на сеть, но также это может ускорить загрузку страницы.

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1h.png)<br><sup>Значок показывает количество больших медиа-элементов, заблокированных на странице.</sup>

По умолчанию эта настройка отключена. Также глобальная  The global default can be enabled in the _Settings_ pane in the dashboard.

![a](https://cloud.githubusercontent.com/assets/585534/12380164/2575ee24-bd3a-11e5-8743-24da038463f8.png)

The threshold size -- a global setting -- to decide when to block or not is also configurable. The threshold size can be set to zero: this will cause all media elements to be blocked. For the sake of documentation, let's refer to media elements (images, videos, audios) which are larger than the set size as _"large media elements"_.

You can enable/disable on a per-site basis, there is a switch in the popup panel to toggle for the current site.

When large media elements have been blocked on a page, you may force a reload of these elements interactively: if you hover over the placeholder of a blocked image and the cursor changes into a magnifier, this means that clicking on a blocked image will force a reload of that image.

If you use this feature and large media elements were blocked on a web page, the context menu will contain a new entry: _"Temporarily allow large media elements"_. When you click this entry, uBO will disable temporarily the blocking of large media element for the site, and attempt to load the blocked media elements without re-loading the page. In some cases you may need to force a reload of the page, for example if large media elements were fetched programmatically by the page. The temporary disabling will be removed for a tab as soon as you travel to a new site, or close the tab.

Blocked large media elements are reported in the logger with the filter `no-large-media: [scope] true`.

Note that this feature has no privacy value: a connection to the remote server must be performed in order to fetch the size of the resource. This of course applies only to resources which were not otherwise blocked by uBO's filtering engine.

Examples of usefulness (let's say you just stumbled onto these pages not knowing whether the article would really interest you), bandwidth consumed:

- <http://www.wired.com/2016/01/drones-arent-just-toys-anymore>
    - Not blocking large media elements: 5.5 MB.
    - Blocking media elements larger than 1 MB: 2.1 MB.
    - Blocking media elements larger than 50 kB: 1.2 MB.
- <http://www.tomshardware.com/reviews/samsung-gear-vr-headset,4405.html>
    - Not blocking large media elements: 15.1 MB.
    - Blocking media elements larger than 1 MB: 15.1 MB.
    - Blocking media elements larger than 50 kB: 61 kB.
- <https://twitter.com/> (your Twitter stream):
    - Not loading largish images by default can help Twitter page performance: click on a placeholder to load only the images which seems to be of interest to you.
    - This is true for any "infinite scrolling" web pages ([another example](http://www.bloomberg.com/news/articles/2016-01-19/being-illegal-won-t-keep-drones-from-taking-over-india)). Not loading the images by default help a lot in such cases.

***

## Отключение косметических фильтров

"Cosmetic filtering" in uBO is what is known as ["element hiding"](https://adblockplus.org/filters#elemhide) in Adblock Plus.

You can easily toggle on/off cosmetic filtering for a given site:

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1j.png)<br><sup>The badge shows the number of DOM elements that have been hidden on the page.</sup>

When present, the badge number indicates the number of elements hidden on the page by uBO as a result of cosmetic filtering. If you disable cosmetic filtering while there are hidden elements on the page, these elements will become visible/hidden as you toggle off/on cosmetic filtering.

A good example of cosmetic filtering in action are the ads showing up with the results of a Google Search page ([example](https://www.google.com/search?q=buy+car&oq=buy+car)).

Cosmetic filtering is always enabled by default.

> ***
> **Tips**
>
> It is often suggested adding a custom static filter such as `@@||example.com^$elemhide` or `@@||example.com^$generichide` to prevent "adblock" detection by specific sites ([example](https://adblockplus.org/forum/viewtopic.php?f=2&t=30763#p124225), [example](https://adblockplus.org/forum/viewtopic.php?f=2&t=43961)). You can accomplish the same goal more simply by just toggling off cosmetic filtering using this switch while on the problematic site.
> 
> This switch can help uBO to further lower its CPU-cycle footprint, which might be beneficial on devices with limited CPU-cycle resources -- and thus helping extend battery life and speed up page load times. The idea is to disable cosmetic filtering everywhere by default, and to enable it only for those sites which really benefit from it.
> ***

To disable cosmetic filtering everywhere by default, go to the [_Settings_ pane in the dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings), and check the option _"Disable cosmetic filtering"_ under the _"Default behavior"_ header. From then on, cosmetic filtering will be turned off everywhere by default, and to turn it on for a specific site where it is really needed, just enable it using the switch in uBO's popup panel.

***

## Блокировка сторонних шрифтов

You can prevent web fonts from being downloaded for the current site:

![Popup UI](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/img/popup-1k.png)<br><sup>The badge shows the number of font resources that have been blocked on the page.</sup>

Because of security and privacy concerns, many prefer to block all web fonts by default. You can do this by adding the following rule directly in the _"My rules"_ pane in the dashboard:

    no-remote-fonts: * true

This will block all web fonts everywhere by default, and in this case you can toggle off the switch to allow web fonts on a per-site basis.

**Caveat for Chromium-based browsers:** Chromium's webRequest API [does not specifically report requests of type `font`](https://developer.chrome.com/extensions/webRequest#type-ResourceType), fonts are reported as type `other`. Whether a request is for a font resource is inferred by uBlock using the "extension" of the path part of a URL. However a URL can be anything really, regardless of request type, so for Chromium-based browsers, uBlock **may** have to block a font **after** the request is made, when the response headers are received from the remote server -- as the response headers allow to identify for sure the type of a resource.
