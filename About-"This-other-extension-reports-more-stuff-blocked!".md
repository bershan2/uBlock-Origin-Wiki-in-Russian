# Об "А другое расширение говорит что заблокировало больше!"
Перевод на русский язык оригинала [_About "This other extension reports more stuff blocked!"_](https://github.com/gorhill/uBlock/wiki/About-"This-other-extension-reports-more-stuff-blocked%21") от 9 мар. 2016.

Кратко: **Не** стоит полагаться на счётчик на значке расширения при оценке эффективности фильтра, т.е. насколько хороша защита Вашей конфиденциальности, Вы можете сильно ошибиться.

***

Оба Adblock Plus и uBlock (а также многие подобные расширения) показывают на своей иконке количество заблокированных ими сетевых запросов.

Иногда на одной и той же странице одно расширение может показывать большее число чем другое, при этом блокируя меньше.

Чем меньше блокировщик блокирует, тем больше будет совершено сетевых запросов. Чем больше сетевых запросов, тем вероятнее что некоторые из них нужно будет заблокировать. Поэтому иногда счетчик на иконке расширения может показывать больше заблокированных сетевых запросов, на самом деле пропустив больше запросов.

Поетому я пологаюсь на [тесты](/gorhill/uBlock/wiki/%C2%B5Block-vs.-others:-Blocking-ads,-trackers,-malwares) при оценке надежности блокировки. Счетчик на значке раширения менее точен в подобной ситуации, доверившисъ ему Вы вполне можете прийти к заключениям не соответствующим действительности.

Если Вы не желаете проводить тесты, то у меня есть [маленькое онлайн-приложение](http://raymondhill.net/httpsb/har-parser.html) позволяющее отследить запросы которые **не** были предотвращены. Чтобы им воспользоваться, откройте _Инструменты Разработчка_ (_Developer Console_) для страницы Вы исследуете и перейдите на вкладку _Сеть_ (_Network_).

Очистите кэш нажатием правой кнопки мыши где-нибудь во вкладке консоли _Сеть_ (_Network_). Перезагрузите исследуемую страницу, затем нажмите правую кнопку мыши во вкладке консоли _Сеть_ (_Network_), и выберите _"Копировать всё как HAR"_ (_"Copy all as HAR"_). Затем вставьте содержимое в текстовое поле этого [онлайн-приложения](http://raymondhill.net/httpsb/har-parser.html), и нажмите _Parse_. Вы увидите доменные имена к которым подключилась исседуемая страница.

Например, на главной странице <http://www.cnet.com/>, **uBlock показывает 10 заблокированных запросов**, а **ABP показывает 16** (оба использовали большое количество фильтров). Давайте посмотрим что происходит "под капотом":

Подключение сервера:

Adblock Plus:
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com
- 1ab45d4854fe036a37ff-6643978b1699ef52a80b7f45a7bcfe3d.r85.cf2.rackcdn.com
- www.googletagservices.com
- zor.livefyre.com
- platform.twitter.com
- s.yimg.com
- dw.cbsimg.net
- geo.query.yahoo.com

uBlock:
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com

Таким образом, uBlock позволил подключение к меньшему количеству внешних серверов, то есть заблокировал больше, но всё равно счетчик на его значке показал меньшее число заблокированных запросов.

Поэтому не стоит полагаться на счётчик на значке расширения при оценке эффективности фильтра, т.е. насколько хороша защита Вашей конфиденциальности, Вы можете сильно ошибиться.

С другой стороны, чрезмерное блокирование может "поломать" отдельные компоненты сайта. В конце концов, попытайтесь разобраться что на самом деле происходит за кадром, и Вы всегда сможете сделать правильный выбор.
