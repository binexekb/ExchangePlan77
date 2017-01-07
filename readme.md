
## Назначение ##

Обработка предназначена для автоматической синхронизации данных между решением **[Агрегатор EDI](http://infostart.ru/public/344684/ "Агрегатор EDI")** и информационной базе на платформе 1C:Предприятие 7.7. Формат обмена **EnterpriseData 1.2**.

Обработка настроена для работы в конфигурации 1С:Предприятие 7.7 "Торговля и Склад", ред. 9.2 на выгрузку и загрузку измененных документов Реализация и Заказ покупателя. В ручном режиме возможно добавить к выгрузке элементы справочников Номенклатура, Контрагенты, Организации.  

## Требования ##

- 1С Предприятие 7.7 для SQL
- Наличие внешней компоненты *1cpp.dll* (для прямых запрос к SQL)  
- Наличие внешней компоненты *v7plus.dll* (для работы с XML)
- Наличие УРБД (для регистрации изменных данных)


## Установка ##

В режиме конфигуратора, через меню *Администрирование - Распределенная ИБ - Управление*, добавляем новую периферийную ИБ (код EDI, только получатель). Выгрузку данных не производить.

![Добавление нового узла ИБ](http://infostart.ru/upload/iblock/67e/67e69db5eb54a5ad9c5be4eeea85b97a.png) 

В режиме конфигуратора, для документов **Реализация** и **Заказ покупателя** изменим параметры миграции. Область распространения либо *Все информационные базы*, либо *Место создания и центр* с дополнением "EDI". Автоматическая регистрация изменений включена.

![Параметры миграции](http://infostart.ru/upload/iblock/6da/6daba77b04fed2cf1e0a36fc83d3b9b2.png)

В режиме предприятия, запускаем обработку и через кнопку "Дополнительно..." выбираем пункт меню "Активировать новый узел". После активации, необходимо перезапустить базу.

![Активация узла](http://infostart.ru/upload/iblock/561/561090aa71781fe83f426af67e28c5c8.png)

Для программного вызова обмена, нужно открыть форму с параметром "ЗапуститьСинхронизацию". Например:

    ОткрытьФорму("Отчет","ЗапуститьСинхронизацию","c:\REPO\ExchangePlan77\EnterpriseData_1_2_1.ert");

## Техническая информация ##

Для хранения идентификаторов из периферийного узла, в каталоге ИБ создается файл **ref7ref8.DBF**.  
GUID ссылочных данных в ИБ создается на основании данных функции **ЗначениеВСтрокуВнутр**.  
Каталог обмена и номер последнего полученного пакета сообщения сохраняется в каталоге ИБ, в файле **EnterpriseData.cfg**.  
Номер отправляемого сообщения вычисляется по данным УРБД.

## Материалы ##

[Структура таблиц УРБД (УРИБ) 1С 7.7](http://1c911.by/stati_1s/statya-struktura-tablic-urbd-urib-1s-77.htm)  
[Статья: УРБД 1С 7.7. Как быстро создать новую периферийную базу](http://1c911.by/stati_1s/statya-urbd-1s-77-kak-bystro-sozdat-novuyu-periferiynuyu-bazu.htm)  
[Описание таблиц 1С V77](http://www.script-coding.com/v77tables.html)  
[Структура и технология работы 1С:УРБД](http://oksla.narod.ru/urib.htm)  
[Нетипичное использование компоненты УРБД в системе 1С:Предприятие 7.7](http://kb.mista.ru/article.php?id=45)  
[Средства встроенного языка, ориентированные на работу с распределенной ИБ](http://tvs-sm.narod.ru/domains/1C/v77/articles/urbd/urbd006.html)    
[Обмен данными с прикладными решениями на платформе «1С:Предприятие» в формате EnterpriseData](https://its.1c.ru/db/metod8dev#content:5851:hdoc)
