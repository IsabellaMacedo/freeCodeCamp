---
title: SQL Create View Statement
localeTitle: SQL Создать представление
---
## SQL Создать представление

### Что такое просмотр?

Просмотр представляет собой объект базы данных, который представляет данные, существующие в одной или нескольких таблицах. Представления используются аналогично таблицам, но они не содержат никаких данных. Они просто «указывают» на данные, которые существуют в другом месте (например, таблицы или представления).

### Почему они нам нравятся?

*   Представления - это способ ограничить представленные данные. Например, данные отдела кадров были отфильтрованы только для предоставления информации, не содержащей информации. Чувствительной информацией в этом случае могут быть номера социального страхования, пол сотрудника, размер оплаты, домашний адрес и т. Д.
*   Сложные данные в более чем одной таблице могут быть объединены в один «вид». Это может сделать жизнь проще для ваших бизнес-аналитиков и программистов.

### Важные советы по безопасности

*   Управление видами осуществляется системой. Когда данные в связанных таблицах изменяются, добавляются или обновляются, представление обновляется системой. Мы хотим использовать их только тогда, когда это необходимо для управления использованием системных ресурсов.
*   В MySQL изменения в дизайне таблицы (то есть новые или удаленные столбцы), созданные ПОСЛЕ создания представления, не обновляются в самом представлении. Представление должно быть обновлено или воссоздано.
*   Представления являются одним из четырех стандартных типов объектов базы данных. Остальные - это таблицы, хранимые процедуры и функции.
*   Обычно представления можно рассматривать как таблицу, но обновления ограничены или недоступны, если представление содержит более одной таблицы.
*   Есть много других подробностей о взглядах, выходящих за рамки этого вводного руководства. Проведите время с руководством по управлению базами данных и получайте удовольствие от этого мощного объекта SQL.

### Синтаксис инструкции Create View (MySQL)

```sql
CREATE 
    [OR REPLACE] 
    [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}] 
    [DEFINER = { user | CURRENT_USER }] 
    [SQL SECURITY { DEFINER | INVOKER }] 
    VIEW view_name [(column_list)] 
    AS select_statement 
    [WITH [CASCADED | LOCAL] CHECK OPTION] 
```

_Это руководство будет охватывать эту часть заявления ...._

```sql
CREATE 
    VIEW view_name [(column_list)] 
    AS select_statement 
```

### Образец создания вида из таблиц учеников

Заметки:

*   Название представления имеет «v» в конце. Рекомендуется, чтобы имя вида указывало, что это как-то способ облегчить жизнь программистам и администраторам баз данных. Ваш ИТ-магазин должен иметь свои собственные правила для именования объектов.
    
*   Столбцы в представлении ограничены SELECT и строками данных по предложению WHERE.
    
*   символ «\` »вокруг имен вида требуется из-за« - »в именах. MySQL сообщает об ошибке без них.
    

```sql
create view `programming-students-v` as 
 select FullName, programOfStudy 
 from student 
 where programOfStudy = 'Programming'; 
 
 select * from `programming-students-v`; 
```

![Изображение-1](https://github.com/SteveChevalier/guide-images/blob/master/create-view-statement01.JPG?raw=true)

### Пример использования представления для объединения данных из нескольких таблиц

Для демонстрации этого использования в базу данных была добавлена ​​таблица демографических данных учащихся. Это представление объединит эти таблицы.

Заметки:

*   Для «объединения» таблиц таблицы должны иметь общие поля (обычно первичные ключи), которые однозначно идентифицируют каждую строку. В этом случае это идентификатор студента. (Подробнее об этом в руководстве по объединению [SQL](../sql-joins/index.md) .)
*   Обратите внимание на «псевдоним», данный каждой таблице («s» для ученика и «sc» для контакта со студентом). Это инструмент для сокращения имен таблиц и упрощения определения используемой таблицы. Это проще, чем повторять длинные имена таблиц. В этом примере это было необходимо, поскольку studentID - это то же имя столбца в обеих таблицах, и система представила бы «неоднозначную ошибку имени столбца» без указания используемой таблицы.

![Изображение-1](https://github.com/SteveChevalier/guide-images/blob/master/create-view-statement02.JPG?raw=true)

_Как со всеми этими вещами, МНОГО БОЛЬШЕ к представлениям. Пожалуйста, ознакомьтесь с руководством для своего менеджера баз данных и получайте удовольствие от различных вариантов._