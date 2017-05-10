# Об "А другое расширение говорит что заблокировало больше!"
Оригинал [_About "This other extension reports more stuff blocked!"_](https://github.com/gorhill/uBlock/wiki/About-"This-other-extension-reports-more-stuff-blocked%21") от 9 мар. 2016 переведён 9 апр. 2017.

Кратко: **Не** стоит полагаться на счётчик на значке расширения при оценке эффективности фильтра, т.е. насколько хороша защита Вашей конфиденциальности, Вы можете сильно ошибиться.

***

Оба Adblock Plus и uBlock (а также многие подобные расширения) показывают на своей иконке количество заблокированных ими сетевых запросов.

Иногда на одной и той же странице одно расширение может показывать большее число чем другое, при этом блокируя меньше.

Чем меньше блокировщик блокирует, тем больше будет совершено сетевых запросов. Чем больше сетевых запросов, тем вероятнее что некоторые из них нужно будет заблокировать. Поэтому иногда счетчик на иконке расширения может показывать больше заблокированных сетевых запросов, на самом деле пропустив больше запросов.

Ultimately, for me it's the [benchmarks I run](/gorhill/uBlock/wiki/%C2%B5Block-vs.-others:-Blocking-ads,-trackers,-malwares) to report blocking power which tells the real story. The badge is really not a good way to assess blocking power of an extension, you could well end up concluding the opposite of what is really happening.

If you don't want to run a benchmark, I have this [little online tool](http://raymondhill.net/httpsb/har-parser.html) with which you can find out the requests which were **not** prevented from leaving your browser. To use it, open the dev console for the page for which you want a report, and go to the _Network_ tab.

Clear the browser cache by right-clicking somewhere in the _Network_ tab console. Force a reload of the web page, then right-click in the _Network_ tab console, and select _"Copy all as HAR"_. Then paste the result in the text area of [this online tool](http://raymondhill.net/httpsb/har-parser.html), and click _Parse_. You will be shown the hostnames which were hit by the browser for the particular page you loaded.

For example, for the front page of <http://www.cnet.com/>, **uBlock shows 10 request blocked**, while **ABP shows 16 request blocked** (both with a lot of filter lists). However here is what really happened internally:

Remote servers reached:

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

Таким образом, uBlock позволил подключение к меньшему количеству внешних серверов, то есть заблокировал больше, но все равно счетчик на его значке показал меньшее число заблокированных запросов.

Поэтому не стоит полагаться на счётчик на значке расширения при оценке эффективности фильтра, т.е. насколько хороша защита Вашей конфиденциальности, Вы можете сильно ошибиться.

С другой стороны, чрезмерное блокирование может "поломать" отдельные компоненты сайта. В конце концов, попытайтесь разобраться что на самом деле происходит за кадром, и Вы всегда сможете сделать правильный выбор.