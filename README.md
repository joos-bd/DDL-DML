# DDL-DML
Работа с данными (DDL/DML)

**SQL — историческая справка**

В начале 1970-х годов в одной из исследовательских лабораторий компании IBM была разработана экспериментальная реляционная СУБД IBM System R, для которой затем был создан специальный язык SEQUEL, позволявший относительно просто управлять данными в этой СУБД. Аббревиатура SEQUEL расшифровывалась как Structured English QUEry Language — «структурированный английский язык запросов». Позже язык SEQUEL был переименован в SQL. Когда в 1986 году первый стандарт языка SQL был принят ANSI (American National Standards Institute), официальным произношением стало [,es kju:' el] — эс-кью-эл

Целью разработки было создание простого непроцедурного языка, которым мог воспользоваться любой пользователь, даже не имеющий навыков программирования. Разработкой языка запросов занимались Дональд Чэмбэрлин (Donald D. Chamberlin) и Рэй Бойс (Ray Boyce). Пэт Селинджер (Pat Selinger) занималась разработкой стоимостного оптимизатора (cost-based optimizer), Рэймонд Лори (Raymond Lorie) занимался компилятором запросов.

SEQUEL был не единственным языком подобного назначения. В Калифорнийском Университете Беркли была разработана некоммерческая СУБД Ingres (являвшаяся дальним прародителем популярной сейчас некоммерческой СУБД PostgreSQL), которая являлась реляционной СУБД, но использовала свой собственный язык QUEL, который, не выдержал конкуренции по количеству поддерживающих его СУБД по сравнению с языком SQL.

Первыми СУБД, поддерживающими новый язык SQL, стали в 1979 году Oracle V2 для машин VAX от компании Relational Software (впоследствии ставшей компанией Oracle) и System/38 от IBM, основанная на System/R.

В 1986 году ANSI представил свою первую версию стандарта, описанную в документе ANSI X3.135-1986 под названием «Database Language SQL». Неофициально этот стандарт SQL-86 получил название SQL1. В 1987 году была завершена работа над версией стандарта ISO 9075-1987 под тем же названием. Разработка этого стандарта велась под патронажем Технического Комитета TC97. Именно его подразделение, именуемое как Подкомитет SC21, курировало разработку стандарта, что стало залогом идентичности стандартов ISO и ANSI для SQL1 (SQL-86).

**MySQL по CAP и PACELC**

Теоремы CAP и PACELC предназначены для распределенных баз данных. По умолчанию MySQL имеет репликацию master-slave. Таким образом, MySQL имеет просто первичные и вторичные узлы, соответственно для обработки данных используется только master и следовательно нарушается толерантность к разделению.

Получаем, что MySQL по теореме САР является СА системой. Но при этом MySQL можно сконфигурировать в CP систему, сформировав несколько распределенных master-slave узлов. По теореме PACELC MySQL относится к PC/EC системам, так как данные в системе должны быть согласованы в ущерб доступности данных и времени ответа кластера.

**MySQL архитектура**

MySQL — это открыто распространяемая СУБД и функционирует по модели клиент-сервер. Отличительной особенностью MySQL является возможность выбора подсистемы хранения, в которой обработка запросов и другие серверные задачи отделены от хранения и извлечения данных. Подобное разделение задач позволяет выбирать способ хранения данных, а также настраивать производительность, ключевые характеристики и так далее.

- Клиентские соединения
- Службы и утилиты
- Интерфейс
- Синтаксический анализатор
- Оптимизатор
- Кеши и буферы
- Подключаемые механизмы хранения
- Файловая система

**MySQL механизмы хранения**

Самыми популярными встроенными системами хранения в MySQL являются InnoDB и MyISAM. Менее популярными и востребованными являются Archive, Blackhole, CSV, Federated, Memory, Merge, Example и NDB Cluster. При этом с версии MySQL 8.0 поддержка механизма MyISAM прекращена, использование возможно, но дальнейшая судьба неизвестна.

**MySQL. InnoDB.**

Это механизм хранения по умолчанию для MySQL 5.5 и выше:
- придерживается требований ACID;
- поддерживает ограничения ссылочной целостности FOREIGN KEY;
- поддерживает функции фиксации, отката и восстановления после сбоя для защиты данных;
- поддерживает блокировку на уровне строк — это «согласованное чтение без блокировки» повышает производительность при использовании в многопользовательской среде;
- хранит данные в кластерных индексах, что уменьшает количество операций ввода-вывода для запросов на основе первичных ключей.

**MySQL. MyISAM.**

Это механизм хранения по умолчанию для MySQL 5.3 и ниже:
- управляет нетранзакционными таблицами;
- обеспечивает высокоскоростное хранение и извлечение;
- поддерживает полнотекстовый поиск;
- данные хранятся в кроссплатформенном формате, что позволяет переносить базы с сервера непосредственным копированием файлов, минуя промежуточные формы;
- допускается индексирование текстовых столбцов, в том числе и переменной длины и т.д

**Логический порядок**

SQL, как любой язык программирования имеет свою структуру и синтаксис. Прежде чем перейти к работе с этим языком, нужно запомнить, что структура запросов имеет свой порядок, но «под капотом» интерпретатор будет выполнять запрос в определенной логической последовательности, и от этого будут зависеть области видимости и с какими данными, что будет происходить.

**DDL**

Data Definition Language (DDL) – это группа операторов определения данных. С помощью этих операторов определяется структура базы данных и происходит работа с объектами базы данных.
В эту группу входят следующие операторы:
- CREATE – используется для создания объектов базы данных;
- ALTER – используется для изменения объектов базы данных;
- DROP – используется для удаления объектов базы данных.

**DML**

Data Manipulation Language (DML) – это группа операторов для манипуляции данными. С помощью этих операторов можно добавлять, изменять, удалять и получать данные из базы данных.
В эту группу входят самые распространенные операторы:
- SELECT – осуществляет выборку данных;
- INSERT – добавляет новые данные;
- UPDATE – изменяет существующие данные;
- DELETE – удаляет данные.

**DСL**

Data Control Language (DCL) – группа операторов определения доступа к данным. Эти операторы нужны для управления разрешениями доступа к данным и выполнения операций над объектами базы данных. Права назначаются на пользователя или на роли.
В данную группу входят следующие операторы:
- GRANT – предоставляет пользователю или группе разрешения на определенные операции с объектами;
- REVOKE – отзывает выданные разрешения;
- DENY – задает запрет, имеющий приоритет над разрешением (Отсутствует в MySQL)

**TCL**

Transaction Control Language (TCL) – группа операторов для управления транзакциями.
Эта группа состоит из следующих операторов:
- START TRANSACTION – служит для определения начала транзакции;
- COMMIT – применяет транзакцию;
- ROLLBACK – откатывает все изменения, сделанные в контексте текущей транзакции;
- SAVEPOINT – устанавливает промежуточную точку сохранения внутри транзакции.

