#### Зачем использовать Batch update ? 
* Допустим мы хотим за 1 рас поместить 1000 записей, не как мы до этого делали помещали по 1 человеку в БД а хотим сразу 1000 записей.
* Если мы будем это делать с помощью обычного update, например исользуя тот же Jdbc Template нам необходимо будет сделать 1000 update'ов, соответственно мы сделаем 1000 запросов к БД и от БД получим 1000 ответов. (если мы делаем 1000 запросов на по сети к нашей БД -- это влечет `повышенную нагрузку на сеть`)
* Но если мы пошлём запрос 1 к БД, говоря ей о том что хотим сразу вставить 1000 записей, то БД сможет распаралелить этот запрос (если же у нас каждый INSERT отправляется отдельно то соответственно у нас операции не как не могу распаралелится)

#### Batch Update
* Поэтому если нам необходимо вставлять множество записей в таблицы, мы используем Batch Update. (вообще идея простая, и заключается она в том что вот эти 1000 записей которые хотим поместить в БД, мы их упаковываем в 1 Пакет -- и этот 1 пакет, 1-им запросом мы отправляем к БД. Всего 1 запрос к БД и 1 ответ от БД)