
| Function Name | Example Usage     | Description                                       |
| ------------- | ----------------- | ------------------------------------------------- |
| AVG(column)   | AVG(salary)       | Returns the average value of a numeric column.    |
| COUNT(column) | COUNT(student_id) | Counts the number of non-NULL values in a column. |
| MAX(column)   | MAX(score)        | Returns the highest value in a set.               |
| MIN(column)   | MIN(score)        | Returns the lowest value in a set.                |
| SUM(column)   | SUM(amount)       | Returns the total sum of a numeric column.        |


| Function Name                                     | Example Usage                                     | Description                                                                |
| ------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------- |
| CASE WHEN condition THEN result [ELSE result] END | CASE WHEN grade >= 75 THEN 'Pass' ELSE 'Fail' END | Performs conditional logic; returns different results based on conditions. |
| IF(condition, true_value, false_value)            | IF(age >= 18, 'Adult', 'Minor')                   | Returns one value if condition is true, another if false.                  |
| IFNULL(expr, alt_value)                           | IFNULL(address, 'Unknown')                        | Returns alternative value if expression is NULL.                           |
| NULLIF(expr1, expr2)                              | NULLIF(a, b)                                      | Returns NULL if both expressions are equal, else returns expr1.            |

| Function Name | Example Usage | Description |
|----------------|----------------|--------------|
| ABS(x) | ABS(-10) | Returns the absolute value of a number. |
| CEIL(x) / CEILING(x) | CEIL(3.2) | Rounds a number up to the nearest integer. |
| FLOOR(x) | FLOOR(3.8) | Rounds a number down to the nearest integer. |
| GREATEST(a, b, ...) | GREATEST(5, 10, 3) | Returns the largest value among the given arguments. |
| LEAST(a, b, ...) | LEAST(5, 10, 3) | Returns the smallest value among the given arguments. |
| MOD(x, y) | MOD(10, 3) | Returns the remainder of x divided by y. |
| POWER(x, y) | POWER(2, 3) | Raises x to the power of y. |
| RAND() | RAND() | Returns a random number between 0 and 1. |
| ROUND(x, d) | ROUND(123.456, 2) | Rounds a number to d decimal places. |
| SQRT(x) | SQRT(16) | Returns the square root of x. |

| Function Name | Example Usage | Description |
|----------------|----------------|--------------|
| CURDATE() | CURDATE() | Returns the current date. |
| CURTIME() / CURRENT_TIME() | CURTIME() | Returns the current time. |
| DATEDIFF(date1, date2) | DATEDIFF('2025-10-13', '2025-10-01') | Returns the number of days between two dates. |
| DAY(date) | DAY('2025-10-13') | Extracts the day part from a date. |
| DAYNAME(date) | DAYNAME('2025-10-13') | Returns the name of the weekday. |
| MONTH(date) | MONTH('2025-10-13') | Extracts the month (as a number) from a date. |
| MONTHNAME(date) | MONTHNAME('2025-10-13') | Returns the full month name. |
| NOW() | NOW() | Returns the current date and time. |
| TIMESTAMPDIFF(unit, datetime1, datetime2) | TIMESTAMPDIFF(YEAR, '2020-01-01', '2025-01-01') | Returns the difference between two datetimes in the specified unit (e.g. YEAR, MONTH, DAY). |
| YEAR(date) | YEAR('2025-10-13') | Extracts the year part from a date. |

| Function Name                            | Example Usage                      | Description                                    |
| ---------------------------------------- | ---------------------------------- | ---------------------------------------------- |
| CHAR_LENGTH(str)                         | CHAR_LENGTH('MySQL')               | Returns the number of characters in a string.  |
| CONCAT(str1, str2, ...)                  | CONCAT(first_name, ' ', last_name) | Joins two or more strings together.            |
| CONCAT_WS(separator, str1, str2, ...)    | CONCAT_WS('-', '2025', '10', '13') | Concatenates strings with a separator.         |
| LEFT(str, n)                             | LEFT('Database', 4)                | Returns the leftmost n characters of a string. |
| LENGTH(str)                              | LENGTH('Hello')                    | Returns the length of a string in bytes.       |
| LOCATE(substr, str) / INSTR(str, substr) | LOCATE('a', 'data')                | Finds the position of a substring.             |
| LOWER(str)                               | LOWER('HELLO')                     | Converts text to lowercase.                    |
| LTRIM(str) / RTRIM(str)                  | LTRIM('  text ')                   | Removes spaces from the left/right side.       |
| REPLACE(str, from_str, to_str)           | REPLACE('2025-10-13', '-', '/')    | Replaces all occurrences of a substring.       |
| REVERSE(str)                             | REVERSE('abc')                     | Reverses a string.                             |
| RIGHT(str, n)                            | RIGHT('Database', 4)               | Returns the rightmost n characters.            |
| SUBSTRING(str, start, length)            | SUBSTRING('Database', 5, 3)        | Extracts part of a string.                     |
| TRIM(str)                                | TRIM('  hello  ')                  | Removes leading and trailing spaces.           |
| UPPER(str)                               | UPPER('hello')                     | Converts text to uppercase.                    |

| Function Name | Example Usage | Description |
|----------------|----------------|--------------|
| CAST(expr AS type) | CAST('2025-10-13' AS DATE) | Converts a value to a specified data type. |
| CONVERT(expr, type) | CONVERT('123', UNSIGNED) | Converts a value to a specified type (similar to CAST). |
| DATE_FORMAT(date, format) | DATE_FORMAT(NOW(), '%M %d, %Y') | Formats a date according to the given format string. |
| FORMAT(number, decimals) | FORMAT(12345.6789, 2) | Formats a number with grouped thousands and decimal places. |

