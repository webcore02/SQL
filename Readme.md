# Базы данных и SQL. Обучение в записи
## Урок 12. Семинар: SQL – Транзакции. Временные таблицы, управляющие конструкции, циклы

1. Создайте функцию, которая принимает кол-во сек и формат их в кол-во дней часов.
Пример: 123456 ->'1 days 10 hours 17 minutes 36 seconds '

```
CREATE FUNCTION format_seconds(@seconds INT)
RETURNS VARCHAR(100)
AS
BEGIN
    DECLARE @days INT, @hours INT, @minutes INT, @secs INT;
    SET @days = @seconds / 86400;
    SET @hours = (@seconds % 86400) / 3600;
    SET @minutes = (@seconds % 3600) / 60;
    SET @secs = @seconds % 60;
    
    RETURN CAST(@days AS VARCHAR) + ' days ' +
           CAST(@hours AS VARCHAR) + ' hours ' +
           CAST(@minutes AS VARCHAR) + ' minutes ' +
           CAST(@secs AS VARCHAR) + ' seconds';
END;

SELECT dbo.format_seconds(123456);
```

2. Выведите только чётные числа от 1 до 10.
Пример: 2,4,6,8,10
```
CREATE FUNCTION get_even_numbers()
RETURNS TABLE
AS
RETURN
(
    SELECT number
    FROM (VALUES (1), (2), (3), (4), (5), (6), (7), (8), (9), (10)) AS Numbers(number)
    WHERE number % 2 = 0
);


SELECT * FROM dbo.get_even_numbers();
```
