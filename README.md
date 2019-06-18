# Northwind Data Services

![Overview](images/northwind-overview.png)

Обучающая задача по разработке веб-приложений, в которых используется клиент-серверное взаимодействие с внешней информационной системой через внешнее API этой системы для управления внутренними сущностями этой системы. В качестве модели данных используется Northwind.

Используемые технологии:
* todo
* todo
* todo
* todo


## Задача 1 - Northwind OData Service

Цели:

* Изучить модель базы данных Northwind.
* Изучить основы протокола HTTP.
* Научиться использовать Postman для выполнения запросов к внешним REST API.
* Научиться использовать язык запросов OData для доступа к данным Northwind OData Service.
* Научиться создавать клиентское приложение для сервисов OData.


### Модель Northwind

В качестве основной модели данных в задаче используется модель учебной базы данных Northwind, схема которой находится в документе [Northwind Sample Database](https://www.zentut.com/wp-content/uploads/downloads/2013/06/Northwind-Sample-Database-Diagram.pdf). Связи между таблицами в диаграмме обозначены с помощью графической нотации "воронья лапка", объяснение которой дано в статье ["Data Modelling using ERD with Crow Foot Notation"](https://www.codeproject.com/Articles/878359/Data-Modelling-using-ERD-with-Crow-Foot-Notation).


#### Выполнение

1. Используя диаграмму, выясните, какие данные хранят в себе сущности модели.
2. Выясните кардинальность для связей между таблицами PK Table (таблица, которая содержит первичный ключ сущности) и FK Table (таблица, содержащая внешний ключ сущности). Заполните колонки Cardinality в таблице:

| PK Table      | Cardinality PK Table | FK Table             | Cardinality FK Table | Relationship |
| ------------- | -------------------- | -------------------- | -------------------- | ------------ |
| shippers      | Zero-or-One          | orders               |  One-or-Many         | One-to-Many  |
| employees     |                      | orders               |                      |              |
| employees     |                      | employees            |                      |              |
| employees     | -                    | territories          | -                    |              |
| customers     |                      | orders               |                      |              |
| customers     | -                    | customerdemographics | -                    |              |
| orders        |                      | orderdetails         |                      |              |
| products      |                      | orderdetails         |                      |              |
| suppliers     |                      | products             |                      |              |
| categories    |                      | products             |                      |              |
| region        |                      | territories          |                      |              |

3. Выясните тип отношений между таблицами базы данных. Заполните колонку Relationship в таблице выше. Используйте статью [Many-to-Many Relationship in the Northwind database](http://blog.codeontime.com/2012/04/many-to-many-relationship-in-northwind.html), чтобы найти связи типа "многие-ко-многим".


#### Дополнительные материалы

* Гудов, Завозкин, Пфайф. Учебное пособие ["Базы данных"](http://unesco.kemsu.ru/study_work/method/DB/book/index.html)
* Сабитов, Пирогов. Учебный курс ["Введение в СУБД"](https://cmd.inp.nsk.su/~pirogov/DB/slides)


### Northwind OData Service

[OData](https://ru.wikipedia.org/wiki/Open_Data_Protocol) - это открытый стандартизированный протокол для запроса и обновления данных, который позволяет выполнять операции с ресурсами, используя команды ("методы") протокола HTTP.


#### Выполнение

1. Изучите основы протокола HTTP - структуру, основные методы (GET, POST, PUT, DELETE), коды состояния, заголовки. Используйте статьи ["Обзор протокола HTTP"](https://developer.mozilla.org/ru/docs/Web/HTTP/Overview) и ["Простым языком об HTTP"](https://habr.com/ru/post/215117/) в качестве обучающего материала, и [статью в википедии](https://ru.wikipedia.org/wiki/HTTP) в качестве справочика.
2. Научитесь использовать Postman, инструмент для работы с HTTP-сервисами и REST API.
    * Установите [Postman](https://www.getpostman.com/downloads/).
    * Освойте базовые сценарии работы c Postman. Можно использовать примеры из видео "[Postman: от простого API-теста до конечного сценария"](https://www.youtube.com/watch?v=hGmJMeE_ok0).
    * Используйте руководство ["Learning OData on Postman"](https://www.odata.org/getting-started/learning-odata-on-postman/), чтобы добавить в Postman коллекцию с готовыми URL.
    * Пройдите ["Basic Tutorial](https://www.odata.org/getting-started/basic-tutorial).
3. Создайте в Postman новую коллекцию с именем Northwind, в этой коллекции создайте такие запросы к [Northwind OData Service](https://services.odata.org/V2/Northwind/Northwind.svc/), которые будут удовлетворять описанию из таблицы ниже. После проверки запроса, занесите необходимые параметры в таблицу:

| Query Description                                                 | HTTP Verb | Url                        |
| ----------------------------------------------------------------- | --------- | -------------------------- |
| Get service metadata.                                             | GET       | /$metadata                 |
| Get all customers.                                                | GET       | /Customers                 |
| Get a customer with "ALFKI" id.                                   | GET       | /Customers('ALFKI')        |
| Get all orders.                                                   | GET       | /Orders                    |
| Get an order with "10248" id.                                     | GET       | /Orders(10248)             |
| Get all orders for a customer with "ANATR" id.                    | GET       | /Customers('ANATR')/Orders |
| Get a customer for an order with "10248" id.                      | GET       | /Orders(10248)/Customer    |

TODO: Add more queries here or use Postman collection?


#### Дополнительные материалы

* OData REST API — мелкие хитрости ([часть 1](https://habr.com/ru/company/databoom/blog/262937/), [часть 2](https://habr.com/ru/company/databoom/blog/263167/), [часть 3](https://habr.com/ru/company/databoom/blog/263435/))
* [What’s New with OData 4: OData 2 vs OData 4](https://www.progress.com/blogs/whats-new-with-odata-4-odata-2-vs-odata-4)


### Создание клиента для Northwind OData Service

Протокол OData имеет несколько версий (на текущий момент - четыре). Версии 1, 2 и 3 являются обратно совместимыми, но не версия 4 - она не является обратно совместимой. Работа с сервисами разных версий отличается с точки зрения реализации клиента. Также реализация клиента зависит от целевой платформы - .NET Framework или .NET Core. Поэтому подход к работе с сервисами OData на стороне клиента может значительно разниться в зависимости от версии сервиса и платформы.

Документация протокола OData
* [OData Version 3.0](https://www.odata.org/documentation/odata-version-3-0/)
* [OData Version 4.0](https://www.odata.org/documentation/odata-version-4-0/)


#### Сервисы WCF

[WCF](https://docs.microsoft.com/en-us/dotnet/framework/wcf/) - это фреймворк, который в прошлом широко использовался для [построения распределенных приложений](http://sergeyteplyakov.blogspot.com/2011/02/wcf.html) на базе платформы .NET. Существует много рабочих приложений, которые построены на его основе и успешно работают. На текущий момент [популярность фреймворка сильно упала](https://github.com/dotnet/wcf/issues/1784), однако поддержка работающих сервисов и работа с ними по-прежнему является актуальной задачей для крупных промышленных программных систем.

Url сервиса выглядит следующим образом:

```
https://services.odata.org/V3/Northwind/Northwind.svc/
```

Наличие [".svc" в пути сервиса](https://stackoverflow.com/questions/17363429/does-a-wcf-service-always-use-an-svc-file) намекает на реализацию сервиса с помощью WCF.


#### Создание клиента сервиса OData v3 для приложения .NET Framework

Работать с сервисом OData можно с помощью вызовов HTTP-методов, однако часто для связи с сервисом используются прокси-классы, которые генерируются автоматически с помощью [дополнительного инструментария](https://docs.microsoft.com/en-us/dotnet/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services). Кодогенерация значительно упрощает написание клиента, снижает количество кода, которое требуется для полноценной работы с сервисом, а также снижает количество ошибок, которые может допустить разработчик.

Visual Studio имеет функциональность [Add Service Reference](https://docs.microsoft.com/en-us/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference?view=vs-2019), с помощью которой можно сгенерировать [прокси-классы для клиента](https://docs.microsoft.com/ru-ru/dotnet/framework/wcf/how-to-create-a-wcf-client). Однако в версиях 2017 и выше эта функциональность может работать некорректно.

1. Используя Postman, получите метаданные [сервиса v3](https://services.odata.org/V3/Northwind/Northwind.svc/) и сохраните их в файл _northwind-data-service.edmx_.
2. Замените в файле версию сервиса с 1.0 на 3.0, чтобы код метаданных выглядел следующим образом:

```
edmx:DataServices m:DataServiceVersion="3.0" m:MaxDataServiceVersion="3.0"
```

3. Используйте утилиту [DataSvcUtil](https://docs.microsoft.com/en-us/dotnet/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe) из пакета .NET Framework, чтобы [сгенерировать прокси-классы](https://docs.microsoft.com/en-us/dotnet/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services) для сущностей сервиса:

```
"%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /in:northwind-data-service.edmx /out:NorthwindDataService3.cs
```

Какая возникла ошибка?

4. Узнайте, какие версии поддерживает DataSvcUtil:

```
"%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /?
```

Используйте утилиту DataSvcUtil снова, но на этот раз укажите номер версии 2.0. Какая возникла ошибка?

(Несмотря на то, что сервис Northwind OData реализует версию протокола 3.0, он отдает метаданные в формате версии 1.0. Поэтому, чтобы продемонстрировать ограничения версии утилиты DataSvcUtil, потребовалась замена версии в пункте 2.)

5. Установите [WCF Data Services 5.6.3](https://www.microsoft.com/en-us/download/details.aspx?id=45308), найдите DataSvcUtil на диске (C:\Program Files (x86)\Microsoft WCF Data Services). Узнайте, какие версии формата метаданных поддерживает эта версия утилиты.
6. Используйте DataSvcUtil версии 5.6.3 с указанием версии метаданных 3.0. После этого на диске должен появиться файл _NorthwindDataService.cs_.
7. Создайте клиента для сервиса для приложения .NET Framework.
    * Создайте консольное приложение .NET Framework.
    * Скопируйте файл _NorthwindDataService.cs_ в папку проекта и добавьте его в проект.
    * Добавьте сборки версии 5.6.3 из папки пакета WCF Data Services 5.6.3:
        * Microsoft.Data.Edm
        * Microsoft.Data.OData
        * Microsoft.Data.Services
        * Microsoft.Data.Services.Client
    * Соберите проект. В случае возникновения ошибок, проверьте версию сборок.
    * Добавьте следующий код, соберите проект и запустите его.

```cs
NorthwindModel.NorthwindEntities entities = new NorthwindModel.NorthwindEntities(new Uri("https://services.odata.org/V3/Northwind/Northwind.svc"));
var customers = entities.Customers.ToArray();
Console.WriteLine("{0} customers in the service found.", customers.Length);
```

Программа должна вернуть:

```
20 customers in the service found.
```

Базовый клиент готов.


#### Создание клиента сервиса OData v3 для приложения .NET Core

Прокси-классы, которые генерирует утилита DataSvcUtil, годятся и для приложений .NET Core.

1. Создайте консольное приложение .NET Core.
2. Скопируйте файл _NorthwindDataService.cs_ в папку проекта, файл в Solution Explorer в Visual Studio появится автоматически.
3. Добавьте сборки версии 5.6.3 из папки ".NETPortable" (не .NETFramework):
    * Microsoft.Data.Edm.dll
    * Microsoft.Data.OData.dll
    * Microsoft.Data.Services.Client.dll
4. Добавьте код предыдущего приложения, соберите проект, запустите приложение. Какая возникла ошибка?
5. Примените [подхода APM](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/asynchronous-programming-model-apm), чтобы сделать вызов к сервису асинхронным:

```cs
NorthwindModel.NorthwindEntities entities = new NorthwindModel.NorthwindEntities(new Uri("https://services.odata.org/V3/Northwind/Northwind.svc"));
IAsyncResult asyncResult;
asyncResult = entities.Customers.BeginExecute((ar) =>
{
	var customers = entities.Customers.EndExecute(ar).ToArray();
	Console.WriteLine("{0} customers in the service found.", customers.Length);
}, null);
WaitHandle.WaitAny(new[] { asyncResult.AsyncWaitHandle });
Console.ReadLine();
```

Запустите приложение.

6. Удалите из проекта сборки версии 5.6.3, которые вы добавили в проект в шаге 3.
7. Установите nuget-пакет [Microsoft.Data.Services.Client](https://www.nuget.org/packages/Microsoft.Data.Services.Client/). Пакет _Microsoft.Data.Services.Client_ является основным для создания клиентов к сервисам OData в .NET Core. Можно не устанавливать пакет _WCF Data Services_, вместо этого в приложениях .NET Core следует использовать nuget-пакет _Microsoft.Data.Services.Client_. Соберите проект и запустите приложение.
8. Использование APM подхода при написании асинхронного кода усложняет структуру кода, делает код запутанным. Вместо подхода APM можно использовать подход [TAP](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap), который [уменьшает количество кода и упрощает его структуру](http://jqyblogger.blogspot.com/2013/11/linq-query-error-message-on-windows.html). :

```cs
NorthwindModel.NorthwindEntities entities = new NorthwindModel.NorthwindEntities(new Uri("https://services.odata.org/V3/Northwind/Northwind.svc"));
var taskFactory = new TaskFactory<IEnumerable<NorthwindModel.Customer>>();
var customers = (await taskFactory.FromAsync(entities.Customers.BeginExecute(null, null), iar => entities.Customers.EndExecute(iar))).ToArray();
Console.WriteLine("{0} customers in the service found.", customers.Length);
Console.ReadLine();
```

9. Для того, чтобы вызывать асинхронные методы, которые помечены модификатором async, метод _Main_ тоже должен быть помечен модификатором async. Второе требование - метод _Main_ должен возвращать _Task_. Перепишите код и соберите проект.

```cs
static async Task Main(string[] args)
```

10. [Возможность помечать метод _Main_ модификатором async](https://blogs.msdn.microsoft.com/mazhou/2017/05/30/c-7-series-part-2-async-main/) появилась в C# только в версии 7.1. В случае ошибок компиляции ("Program does not contain a static 'Main' method suitable for an entry point"), [измените номер версии языка на 7.1 или выше](https://dailydotnettips.com/choosing-the-c-language-latest-version-minor-release-in-visual-studio-2017/). Соберите проект и запустите приложение.

Базовый клиент готов.


#### Создание клиента сервиса OData v4 для приложения .NET Core

TODO


### REST API

https://www.restapitutorial.com/index.html
https://restfulapi.net/


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


* [Northwind and pubs sample databases for Microsoft SQL Server](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)
* [Database agnostic DB Script to create Northwind Data Model](https://github.com/mrin9/northwind)


http://northwind.servicestack.net/
https://www.hanselman.com/blog/ExploringServiceStacksSimpleAndFastWebServicesOnNETCore.aspx


https://dzone.com/articles/migrating-a-northwind-database-to-nosql-database


https://dzone.com/articles/collection-sql-server-sample-databases

sql tutorial
https://www.zentut.com/sql-tutorial/%20-

4. Найдите в схеме базы данных примеры (если они есть) 1NF, 2NF, 3NF, BCNF, 4NF, 5NF.

* Гудов, Завозкин, Пфайф. Учебное пособие ["Базы данных"](http://unesco.kemsu.ru/study_work/method/DB/book/index.html)
* Сабитов, Пирогов. Учебный курс ["Введение в СУБД"](https://cmd.inp.nsk.su/~pirogov/DB/slides)


OLAP
http://lib.kstu.kz:8300/tb/books/2016/IVS/Sistemy%20avtomatizirovannyh%20eksperimentov/%D0%9A%D0%BE%D0%BD%D1%82%D1%80%D0%BE%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0/kontr2.htm

Trader, powerapps
https://powerapps.microsoft.com/en-us/blog/northwind-traders-relational-data-sample/