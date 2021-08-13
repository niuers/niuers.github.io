---
title: "Database Related Problems"
date: 2021-08-12
categories:
  - blog
tags:
  - algorithm
  - database
  - summary
---

1. Join
    1. Left Join:
        * `select FirstName, LastName, City, State from Person left join Address on Person.PersonId = Address.PersonId;`

2. Select the k-th
    1. `select DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 1`
        * N.B. If there's only 1 row, it will return empty result
    2. The OFFSET  clause skips the offset rows before beginning to return the rows. The OFFSET clause is optional so you can skip it. If you use both LIMIT and OFFSET clauses the OFFSET  skips offset rows first before the LIMIT  constrains the number of rows.
        * `select from table limit 5 offset 3`: skip 3 rows first, then take the first 5 rows from the rest


3. Set result to NULL if the query doesn't return anything
    1. `select ifnull( (select DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1 OFFSET 1), NULL)`
        * You must use parentheses within `ifnull` to make it work.

4. Declare a variable
    ```
    CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
    BEGIN
    DECLARE M INT;
    SET M=N-1;
      RETURN (
          SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT M, 1
      );
    END
    ```

5. Select from multiple tables
    1. `select t1.name, t2.amount from table1 as t1, table2 as t2 where t1.id = t2.id`    
        * If there's no `where` condition, we'll get Cartesian product in results, i.e. number of rows in table 1 times number of rows in table 2.
    2. You can also use `join` and `on`

6. Groupby
    1. Use it with `having` condition
    ```
    select Email from Person group by Email having count(Email) > 1
    ```
7. Check if a field is NULL
    1. `where isnull(column_name)`
    2. `where column_name is null`
[LC48. Rotate Image]: https://leetcode.com/problems/rotate-image/
[LC54. Spiral Matrix]: https://leetcode.com/problems/spiral-matrix/
[LC59. Spiral Matrix II]: https://leetcode.com/problems/spiral-matrix-ii/




    


