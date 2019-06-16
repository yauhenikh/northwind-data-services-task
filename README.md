# Northwind Data Services

![Overview](images/northwind-overview.png)

Обучающая задача по разработке веб-приложений, в которых используется клиент-серверное взаимодействие с внешней информационной системой через внешнее API этой системы для управления внутренними сущностями этой системы. В качестве модели данных используется Northwind.

Используемые технологии:
* ASP.NET
* WCF

## Задача 1

Изучить Northwind database.

### Northwind Data Model

В качестве основной модели данных в задаче используется модель учебной базы данных Northwind. Основные таблицы базы данных Northwind представлены на схеме базы данных:

[Northwind Database Schema](http://merc.tv/img/fig/Northwind_diagram.jpg)



Схема базы данных Northwind ([система обозначений для связей](https://www.lucidchart.com/pages/ER-diagram-symbols-and-meaning))
https://www.zentut.com/wp-content/uploads/downloads/2013/06/Northwind-Sample-Database-Diagram.pdf




### Northwind Data Service

В качестве внешнего сервиса будет использоваться [Northwind OData Test Service](https://services.odata.org/V2/Northwind/Northwind.svc/).

Пример использования сервиса через браузер:

1. Перейти на [страницу сервиса](https://services.odata.org/V2/Northwind/Northwind.svc/).

```
https://services.odata.org/V2/Northwind/Northwind.svc/
```

2. Чтобы посмотреть список всех сущностей Customer - добавить "/Customers"

```
https://services.odata.org/V2/Northwind/Northwind.svc/Customers
```

3. Чтобы найти сущность Customer, уникальный идентификатор которого ALFKI.

```
https://services.odata.org/V2/Northwind/Northwind.svc/Customers('ALFKI')
```

4. 

https://services.odata.org/V2/Northwind/Northwind.svc/Customers('ALFKI')/Orders

![Northwind OData Service](images/northwind-odata-service.png)



## Ссылки

### Northwind

http://www.wilsonmar.com/northwind.htm

* [Схема базы данных Northwind](https://www.zentut.com/wp-content/uploads/downloads/2013/06/Northwind-Sample-Database-Diagram.pdf) ()

Схема базы данных Northwind ([в диаграмме использована система обозначений "воронья лапка"](https://www.codeproject.com/Articles/878359/Data-Modelling-using-ERD-with-Crow-Foot-Notation))



* [Northwind and pubs sample databases for Microsoft SQL Server](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)
* [Database agnostic DB Script to create Northwind Data Model](https://github.com/mrin9/northwind)


http://northwind.servicestack.net/
https://www.hanselman.com/blog/ExploringServiceStacksSimpleAndFastWebServicesOnNETCore.aspx


https://dzone.com/articles/migrating-a-northwind-database-to-nosql-database