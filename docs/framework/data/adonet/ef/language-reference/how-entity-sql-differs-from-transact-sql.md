---
title: Отличия Entity SQL от Transact-SQL
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c9ee36d-f294-4c8b-a196-f0114c94f559
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: 3f80ec1ac51dded1f91d1a18c4d4e24836cf92cd
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2018
---
# <a name="how-entity-sql-differs-from-transact-sql"></a>Отличия Entity SQL от Transact-SQL
В этом разделе описываются различия между [!INCLUDE[esql](../../../../../../includes/esql-md.md)] и [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)].  
  
## <a name="inheritance-and-relationships-support"></a>Поддержка наследования и связей  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] работает непосредственно с концептуальными схемами сущности и поддерживает функции концептуальной модели, как наследование и связи.  
  
 При работе с наследованием часто полезно выбрать экземпляры подтипа из коллекции экземпляров супертипа. [Oftype](../../../../../../docs/framework/data/adonet/ef/language-reference/oftype-entity-sql.md) оператор в [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (аналогично `oftype` в последовательностях C#) предоставляет эту возможность.  
  
## <a name="support-for-collections"></a>Поддержка коллекций  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] коллекции рассматриваются как сущности первого класса. Пример:  
  
-   Выражения коллекций допускаются в предложении `from`.  
  
-   Вложенные запросы `in` и `exists` были обобщены, чтобы разрешить любые коллекции.  
  
     Вложенный запрос - один из видов коллекций. `e1 in e2` и `exists(e)` - конструкции языка [!INCLUDE[esql](../../../../../../includes/esql-md.md)] для выполнения этих операций.  
  
-   Операторы работы с наборами, такие как `union`, `intersect` и `except`, теперь работают с коллекциями.  
  
-   Операции соединения с коллекциями.  
  
## <a name="support-for-expressions"></a>Поддержка выражений  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] имеет вложенные запросы (таблицы) и выражения (строки и столбцы).  
  
 Для поддержки коллекций и вложенных коллекций [!INCLUDE[esql](../../../../../../includes/esql-md.md)] делает все выражения. Код [!INCLUDE[esql](../../../../../../includes/esql-md.md)] является более легко компонуемым по сравнению с кодом [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] - любое выражение может использоваться в любом месте. Результатом выражения запроса всегда является коллекция проецируемых типов, которая может быть использована везде, где разрешено выражение коллекции. Сведения о [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] выражения, которые не поддерживаются в [!INCLUDE[esql](../../../../../../includes/esql-md.md)], в разделе [неподдерживаемые выражения](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md).  
  
 Допустимы все приведенные ниже запросы [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
1+2 *3  
"abc"  
row(1 as a, 2 as b)  
{ 1, 3, 5}   
e1 union all e2  
set(e1)  
```  
  
## <a name="uniform-treatment-of-subqueries"></a>Единая обработка вложенных запросов  
 Ориентированности на таблицы, [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] выполняет контекстную интерпретацию вложенных запросов. Например, вложенный запрос в `from` предложение считается мультинабором (таблица). Тот же вложенный запрос в предложении `select` считается скалярным вложенным запросом. Аналогичным образом, вложенный запрос, используемый в левой части `in` оператор считается скалярным вложенным запросом, а с правой стороны предполагается вложенный запрос мультинабора.  
  
 Эти различия устранены в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Выражение имеет единую интерпретацию, которая не зависит от контекста, в котором оно использовано. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] рассматривает всех вложенных запросов к будет мультинабора. Если из вложенного запроса, скалярное значение [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предоставляет `anyelement` оператор обращается к коллекции (в данном случае вложенный запрос), который извлекает одноэлементное значение из коллекции.  
  
### <a name="avoiding-implicit-coercions-for-subqueries"></a>Устранение неявных приведений для вложенных запросов  
 Побочный эффект единообразной обработки вложенных запросов - неявное преобразование вложенных запросов к скалярным значениям. В частности, в языке [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] мультинабор строк (с единственным полем) неявно преобразуется в скалярную величину, тип данных которой совпадает с типом данных поля.  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает такое неявное приведение. В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предусмотрены оператор ANYELEMENT, который извлекает одноэлементное значение из коллекции, и предложение `select value`, позволяющее избежать создания оболочки строк в выражении запроса.  
  
## <a name="select-value-avoiding-the-implicit-row-wrapper"></a>Выбранное значение: устранение неявной оболочки строк  
 Предложение select во [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] вложенный запрос неявно создает оболочку строк вокруг элементов в предложении. Это означает, что нельзя создавать коллекции скалярных величин или объектов. [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] обеспечивает неявное приведение между rowtype с одним полем и одноэлементным значением того же типа данных.  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] предоставляет предложение `select value`, чтобы пропустить неявное построение строки. В предложении `select value` можно указать только один элемент. При использовании такого предложения не создается оболочка строк вокруг элементов в предложении `select`, что позволяет получить коллекцию необходимой формы, например: `select value a`.  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает также конструктор строк, позволяющий создавать произвольные строки. Предложение `select` принимает один или несколько элементов в проекции и возвращает результаты в записи данных с полями, следующим образом:  
  
 `select a, b, c`  
  
## <a name="left-correlation-and-aliasing"></a>Левая корреляция и задание псевдонимов  
 В языке [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] выражения в данной области (отдельное предложение, такое как `select` или `from`) не могут ссылаться на выражения, определенные ранее в той же области. Некоторые диалекты SQL (в том числе [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]) поддерживают их ограниченные формы в предложении `from`.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] обобщает левые корреляции в `from` предложения и одинаково их обрабатывает. Выражения в предложении `from` могут содержать ссылки на более ранние определения (определения слева) в том же предложении без дополнительных синтаксических конструкций.  
  
 В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] также налагаются дополнительные ограничения на запросы, включающие предложения `group by`. Выражения в `select` предложение и `having` предложение таких запросов могут ссылаться только на `group by` ключи через псевдонимы. Следующая конструкция допустима в [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] , но не находится в [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select t.x + t.y from T as t group by t.x + t.y  
```  
  
 На языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] необходимо написать:  
  
```  
select k from T as t group by (t.x + t.y) as k  
```  
  
## <a name="referencing-columns-properties-of-tables-collections"></a>Ссылочные столбцы (свойства) таблиц (коллекций)  
 Все ссылочные столбцы в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] должны быть квалифицированы с псевдонимом таблицы. Следующая конструкция (предполагается, что `a` является допустимым столбцом таблицы `T`) является допустимым в [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] , но не в [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
```  
select a from T  
```  
  
 Форма [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select t.a as A from T as t  
```  
  
 Псевдонимы таблицы в предложении `from` необязательны. Имя таблицы используется как неявный псевдоним. В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] допустима также следующая форма:  
  
```  
select Tab.a from Tab  
```  
  
## <a name="navigation-through-objects"></a>Перемещение по объектам  
 В языке [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] для ссылок на столбцы (строки) таблицы используется символ «.». В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] этот подход (заимствованный из языков программирования) расширен и позволяет перемещаться по свойствам объекта  
  
 Например, если `p` - выражение типа Person, с помощью следующего синтаксиса [!INCLUDE[esql](../../../../../../includes/esql-md.md)] можно ссылаться на город в его адресе.  
  
```  
p.Address.City   
```  
  
## <a name="no-support-for-"></a>Не поддерживается *  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] поддерживает * синтаксис в качестве псевдонима для всей строки и уточненного \* синтаксис (t.\*) для быстрого поля этой таблицы. Кроме того [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] позволяет ввести число специальных (\*) статистическое выражение, включающее значения NULL.  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает конструкцию «*». Запросы [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] в форме `select * from T` и `select T1.* from T1, T2...` могут быть выражены в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] как `select value t from T as t` и `select value t1 from T1 as t1, T2 as t2...`, соответственно. Эти конструкции также обеспечивают наследование (заменяемость значений), в то время как варианты `select *` ограничены свойствами верхнего уровня объявленного типа.  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает статистическую функцию `count(*)`. Взамен рекомендуется использовать `count(0)`.  
  
## <a name="changes-to-group-by"></a>Изменения на предложение Group By  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает псевдонимы ключей `group by`. Выражения в предложении `select` и предложении `having` таких запросов должны ссылаться на ключи `group by` через псевдонимы. Например, синтаксическая конструкция [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
```  
select k1, count(t.a), sum(t.a)  
from T as t  
group by t.b + t.c as k1  
```  
  
 ...эквивалентна следующей конструкции [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]:  
  
```  
select b + c, count(*), sum(a)   
from T  
group by b + c  
```  
  
## <a name="collection-based-aggregates"></a>Статистические функции на основе коллекций  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает два типа статистических функций.  
  
 Статистические функции на основе коллекций работают с коллекциями и возвращают результат статистической обработки. Они могут применяться в любом месте в запросе и не требуют предложения `group by`. Например:  
  
```  
select t.a as a, count({1,2,3}) as b from T as t     
```  
  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] также поддерживает статистические функции в стиле SQL. Например:  
  
```  
select a, sum(t.b) from T as t group by t.a as a  
```  
  
## <a name="order-by-clause-usage"></a>Использование предложения ORDER BY  
 В языке [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] предложения ORDER BY могут быть указаны только в самом верхнем блоке инструкции SELECT .. FROM . WHERE. В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] можно использовать вложенное выражение ORDER BY, которое может быть размещено в любом месте запроса, однако упорядочение во вложенном запросе не сохраняется.  
  
```  
-- The following query will order the results by the last name  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="identifiers"></a>Идентификаторы  
 В языке [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] сравнение идентификаторов всегда осуществляется с учетом параметров сортировки текущей базы данных. В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] регистр символов в идентификаторах не учитывается, однако учитываются диакритические знаки (в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] различаются символы с диакритическими знаками и без таковых; например «a» не равно «ấ»). В языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)] версии символов, которые внешне кажутся одинаковыми, но определены на разных кодовых страницах, считаются различными символами. Дополнительные сведения см. в разделе [набор символов ввода](../../../../../../docs/framework/data/adonet/ef/language-reference/input-character-set-entity-sql.md).  
  
## <a name="transact-sql-functionality-not-available-in-entity-sql"></a>Функциональность Transact-SQL, недоступная в Entity SQL  
 Следующая функциональность [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] недоступна в языке [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
 DML  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] в настоящее время не поддерживает инструкции DML (Вставка, обновление и удаление).  
  
 DDL  
 Текущая версия [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает DDL.  
  
 Командное программирование  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает командное программирование в отличие от [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]. Используйте вместо этого языки программирования.  
  
 Функции группирования  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] пока не поддерживает функции группирования (например, CUBE, ROLLUP и GROUPING_SET).  
  
 Функции аналитики  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не предоставляет (пока) поддержку функций аналитики.  
  
 Встроенные функции, операторы  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает подмножество [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]встроенных функций и операторов. Вероятно, эти операторы и функции будут реализованы ведущими поставщиками хранилищ. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] использует функции конкретного хранилища, объявленные в манифесте поставщика. Кроме того [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] позволяет объявлять встроенные и пользовательские функции хранилища для [!INCLUDE[esql](../../../../../../includes/esql-md.md)] для использования.  
  
 Подсказки  
 Язык [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не предоставляет механизм подсказок в запросах.  
  
 Пакетирование результатов запроса  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживает пакетирование результатов запросов. Например, следующее выражение допустимо [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] (отправляемый как пакет):  
  
```  
select * from products;  
select * from catagories;  
```  
  
 Однако эквивалент [!INCLUDE[esql](../../../../../../includes/esql-md.md)] не поддерживается.  
  
```  
Select value p from Products as p;  
Select value c from Categories as c;  
```  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] поддерживает только запросы, которые выдают один результат на одну команду.  
  
## <a name="see-also"></a>См. также  
 [Общие сведения об Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)  
 [Неподдерживаемые выражения](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)
