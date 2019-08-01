# Митап \#5 – 30.07

{% embed url="https://www.youtube.com/watch?v=qjiWop0ZcVg&feature=youtu.be" %}

### **Family Crypto Inheritance**

Нужно пошейрить секреты с тем, кто остался жив \(или не потерял память\)

General подход – вы шифруете все свои секреты, а потом делаете что-то со своим ключем шифрования. Например, вы можете потом поделить ключ на несколько частей и поделить это между кем-то, близкими людьми, например, они потом как офчейновый мультисиг работают – если с чуваком что-то случается, то держатели частей могут достать секреты и полуичть крипту. Но не защищает от bad actors, что ваши любимые сговорятся против вас.

Идя Леши – мы делаем 1 из трех мультисигов, где каждый имеет минимальный сетап 2 из 4. 1 это вы и ваш партнер, 2 ваша семья, 3 ваши друзья \(или другая семья\). Для того чтобы это работало надо какой-то суперпростой интерфейс. Чтобы не сговорились 2 и 3 надо давать голосам какой-то вес, т.е. вес себя и партнера будет больше, чем семей.

Ищем решение, что надо сделать чтобы деньги переходили родне, детям, благотворительному фонду, но точно никогда не будут wasted.

Идея: субъект 1 \(с деньгами\), субъект 2 \(наследник\) и субъект 3 \(сервер в кладовке\). Если субъект 1 перестает делать какие-либо движения, то сервер отдает все деньги субъект 2.

Вопрос в доверии серверу – переносить на не-домашний сервак значит нужно доверять провайдеру.

Архитектура с пингами уже есть заимплеменчена и работает – это чисто для наследования чтобы кто-то получил секреты через полгода. А хотелось бы чтобы прям сейчас получить наследования.

Решение с третьей стороной как с escrow?

Есть возможность убрать из этой схемы третье лицо. Например, в битке, если я умру – когда идет spend транзакция еще и подписывается change output на наследника с тайм локом и эта транзакция должна где-то сохраняться. Таким образом можно строить политику, что если за полгода деньги не сняли, то деньги автоматически перевелись. При помощи тайм-локов можно строить структуру и отдавать более дальним родственникам. Тайм-лок с месяцами это обязательное условие – за день если можно получить деньги, то могут прийти злодеи и угрожать чтобы ты забрал деньги СЕЙЧАС и отдал им.

Кто будет получать деньги? Для этого надо всю семью заблокчейнить, каждому открыть адреса – речь идет об одном адресе, где активы, и об одном пароле к нему. Мы сталкиваемся тут с тематикой, что нам надо валидировать личность на блокчейне и тут мы либо делегируем определение факта смерти человека оракулу либо надо идентифицировать всех в блокчейне.

Нам надо какой-то валидатор, который бы из внешнего мира давал информацию в блокчейн. 

Бабушка с приватным ключем не сможет вывести биток\)

Это не столько про inheritance, сколько про завещание – т.е. фиксация адреса на совести того, кто делает завещание.

Часто было то, что жена выкинула ключ :\)

Как потенциально решается: что жена никогда не выкинет – свой паспорт. Что такое паспорт? – ID карта с подписью, которая меняется и перегенерируется. Но, в общем-то это решение, которое имеет свой оверхед, но и выход – если подвязываться на inheritance, то я бы подвязывался на существующую инфраструктуру паспортов \(европейских допустим\). Ну и сложно с тем, что надо генерить сертификаты, совместимые с блокчейном.

* Можно сделать смарт контракт, который проверит подпись и даст из этого уже настоящий адрес?Жена подписывает паспортом адрес, а контракт...

Контракт не может проверить подпись – потому что сертификат не совместимый и пока центр сертификации не начнет делать сертификаты на блокчейне\(или совместимые с ним\), то это работать не будет.  
Поинт основной в том, что если использовать документы, которые были by design, то это будет работать\)

Вероятность того, что кто-то выкинет ключ мала, особенно если он железный.

Еще идея в том, что потеря одного из ключей не должна отбирать доступ – должен быть фолбек механизм. Если много ключей потеряно одновременно, вот тогда да.

Если банально взять – трезор с сидом из 16ти слов – можно взять сейф, куда сложить сид фразу с трезора и инструкцией как получить деньги.

Что является событием для передачи завещания – пока не будет валидации того, что человек умер и надо передать завещание.. с другой стороны можно взять систему, которая валидирует событие смерти через документ, который должен быть стандартен, ну и наверное мы никогда не решим задачу чтобы нас не хотели убить люди для получения денег.

* А вот последнее решается тем, что субъект не должен знать, что он наследник или он должен не знать, что он наследует.

Кажется интересной идеей, мы делали небольшое юзабилити исследование про то, как хранят ключи – на компе, в облаке, etc – была такая идея, что при создании кошелька ты выбираешь уровень паранойи и в зависимости от этого будет куча путей хранения, один из которых был сошиал бекап – у нас такого раньше не было, например.

Еще механика – две семьи, муж и жена, семьи могут быть разными.. или ДАО ранее были организации, а теперь предлагают семейные дао, где ты сам определяешь права и можешь так определить наследников.

Про наследие – точно есть одно решение kasa? у них идея втом, что 3 ключа отдаются тебе, 1 ключ kasa и один юристу, который оперирует наследованием. Идея в том, что надо один из своих ключей передать наследнику.

Если мы говорим об индетификации людей – то что может персонализировать человека? Если глобально выбирается идентификация и она будет криптографически и анонимно защищена – в общей этой некой сети, то тогда будет, наверное, определяться как будет эта одна личность идентифицироваться....

Идея такая, наиболее близкая к реализации, о том, чтобы составить смарт контракт со всеми активами, есть адрес B, куда надо отправить все. Контракт бы просто отслеживал Адрес А на наличие активности – никто бы не знал что передается и кому и когда. И серверов и третьих лиц тут нет, которые могли бы вмешаться.

Если весь залоченый эфир залочен, то правильно ли, что он повышает стоимость незалоченому эфиру и это некоторые инхеританс.. который возвращается всем... а не твоей семье\)

У Парити был залоченый эфир для выдачи их токенов, при том, что эфир был залочен можно было сигналить токенами другого блокчейна – можно ли при залоченом эфире делать что-то с ним?

### Ethereum 2.0

Был некоторый скептицизм на счет того, как скоро он придет, насколько он централизован и насколько все сложно – на встрече Ethmagicians было мнение, что это будет совсем не скоро.

Не знаем как работают EF, consensys, как гранты распределяются и т.п. какие мотивации. Кто участвовал в обсуждениях БИПов и ЕИПов, могут больше рассказать. Как сказал Леша – решения из ethereum 2.0 компромиссные и улучшают scalability за счет принесения в жертву ненадобности в доверии – т.к. это не какое-то радикальное решение, то все, наверное, понимают, что оно не решит кучу проблем и с этим падает мотивация, что его надо пушить и что не хотелось бы загубить то, что есть уже. Не видится, что шардинг решит какие-то глобальные проблемы. Непонятно насколько есть спрос на локальные децентрализированые приложения, как например голосования в ОСББ\)\) например, локальная очень валюта, которая нигде кроме вашего района не нужна.

Шард можен не обязательно быть локальным, сколько должен быть ограниченным объем стейта и пользователей.

Идея в том, что куча децентрализированных приложений и все хотят общаться друг с другом – чем больше вы общаетесь между шардами, тем меньше пользы от шарда.

Например, DAI – ты локаешь в своем шарде даи, вы торгуете, а потом ты выходишь, тогда имеет значение. Общение между шардами будет в самом протоколе эфира.

Я не знаю есть ли сейчас спрос на сегрегированные локальные децентрализованные приложения – узко-децентрализованные приложения, ограниченное взаимодействием и/или локацией.

Я хотел сказать пару слов про шардинг – так или иначе валидаторы будут разбиты на шарды и если у нас есть модель adaptive corruption – атакующий может выбрать и дать какую-то публичную оферту, например "вы будете в шарде 48, продайте мне ключи в два раза дороже, чем у вас есть денег" и таким образом тот или иной пользователь может корумпировать шард. Если у нас корумпируется хотябы один шард, то это катастрофа – пользователь может напечатать себе денег и использовать их в других шардах и это будет как снежный ком и сценарий будет не очень красивый. Ассампшны не выглядят слишком секюрными.

### ZK & Rollup

Что такое pollup – представим плазму– у нас есть коммит чейн, который мы коммитим в меинчейн – стейт самого блока либо стейт, к которому мы пришли после добавления блока. Возьмем пример стейта, как в блокчейне и меркл рут. Если мы запостим новый хеш, который невалидный, то из-за того, что эфир не проверяет весь стейт, то можно запостить валидный хеш, но убежать со всеми деньгами. Но пользователи это видят – могут опротестовать с доказательствами, данными. В тот момент, когда данные стают недоступными все пользователи должны одновременно выйти – это проблема. Из-за этого есть только один оператор.

Как решается – мы можем в эфир кинуть все данные, мы могли бы запостить cold data, например, но это все равно много.

Ролап использует две идеи – мы используем front proves – на каждый блок операторы должны послать прувы. И мы отправляем все данные в блокчейн – без подписи. Плюс немного буфера на прувы.

Можно сделать rollup для general purpose \(не трансфер\), надо будет делать рекурсии \(снарки в снарках\). Но с текущими языками это боль – ждем EIP1962, который будет поддерживать нужные кривые.

В ролапе можно использовать и UTXO и балансную модель. UTXO будет требовать больше места.

В ролапе всегда паблишится дельта данных.

### Конец :\)

Сегодня мы попробовали записать дискуссию и сделать подкаст – всем ли ок? Решили, что не.

### Фидбеки

Хорошо, нравицо.

Больше времени на тему для разговора – есть смыл на некоторые темы давать больше времени на обсуждения или спич.

Интересно просто послушать про блокчейн – философский вопрос – как бабушек заставить этим пользоваться, хотелось бы увидеть хоть одно живое приложение чтобы бабушка пользовалась – массово, а не в разрезе узкого круга

Очень понравились доклады в этот раз, было бы круто такие и дальше

Понравились доклады, негативного фидбека нет.

Хотелось бы дольше слушать Лешу про ZK.
