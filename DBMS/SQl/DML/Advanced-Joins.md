## Advanced SQL Queries

let's delve into these advanced SQL queries using our online bookstore example:

### 1. JOIN:

`JOIN` is used to combine rows from two or more tables based on a related column. There are several types of JOIN:

- **INNER JOIN**: Returns records that have matching values in both tables.

  ```sql
  SELECT Books.Title, Authors.FirstName, Authors.LastName
  FROM Books
  INNER JOIN Authors ON Books.AuthorID = Authors.AuthorID;
  ```

- **LEFT JOIN (or LEFT OUTER JOIN)**: Returns all records from the left table, and the matched records from the right table. If no match is found, NULL values are returned.

  ```sql
  SELECT Books.Title, Authors.FirstName, Authors.LastName
  FROM Books
  LEFT JOIN Authors ON Books.AuthorID = Authors.AuthorID;
  ```

- **RIGHT JOIN (or RIGHT OUTER JOIN)**: Returns all records from the right table, and the matched records from the left table. If no match is found, NULL values are returned.

  ```sql
  SELECT Books.Title, Authors.FirstName, Authors.LastName
  FROM Books
  RIGHT JOIN Authors ON Books.AuthorID = Authors.AuthorID;
  ```

- **FULL JOIN (or FULL OUTER JOIN)**: Returns all records when there is a match in either left or right table records.

  ```sql
  SELECT Books.Title, Authors.FirstName, Authors.LastName
  FROM Books
  FULL JOIN Authors ON Books.AuthorID = Authors.AuthorID;
  ```

- **CROSS JOIN**: Returns the Cartesian product of the sets of records from the joined tables.
  ```sql
  SELECT Books.Title, Authors.FirstName, Authors.LastName
  FROM Books
  CROSS JOIN Authors;
  ```

### 2. UNION and UNION ALL:

- **UNION**: Combines the result sets of two or more SELECT statements and removes duplicate rows.

  ```sql
  SELECT Title FROM Books
  UNION
  SELECT FirstName AS Title FROM Authors;
  ```

- **UNION ALL**: Similar to UNION, but it does not remove duplicate rows.
  ```sql
  SELECT Title FROM Books
  UNION ALL
  SELECT FirstName AS Title FROM Authors;
  ```

### 3. INTERSECT and EXCEPT:

- **INTERSECT**: Returns the common records in the result sets of two SELECT statements.

  ```sql
  SELECT AuthorID FROM Books
  INTERSECT
  SELECT AuthorID FROM Authors;
  ```

- **EXCEPT**: Returns the records in the first SELECT statement that are not in the second SELECT statement.
  ```sql
  SELECT AuthorID FROM Authors
  EXCEPT
  SELECT AuthorID FROM Books;
  ```

### 4. Subqueries:

- **IN**: The IN keyword is used to filter the results based on a list of values.

  ```sql
  SELECT * FROM Authors WHERE AuthorID IN (SELECT AuthorID FROM Books);
  ```

- **EXISTS**: The EXISTS keyword is used to filter the results based on whether a subquery returns any results.

  ```sql
  SELECT * FROM Authors WHERE EXISTS (SELECT * FROM Books WHERE Books.AuthorID = Authors.AuthorID);
  ```

- **ANY and ALL**: These keywords are used with comparison operators to filter results based on a subquery.
  ```sql
  SELECT * FROM Books WHERE Price > ANY (SELECT AVG(Price) FROM Books GROUP BY AuthorID);
  ```

### 5. Common Table Expressions (CTEs) with WITH clause:

CTEs are temporary result sets that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement.

```sql
WITH AuthorBooks AS (
  SELECT Authors.AuthorID, FirstName, LastName, COUNT(Books.BookID) AS BookCount
  FROM Authors
  LEFT JOIN Books ON Authors.AuthorID = Books.AuthorID
  GROUP BY Authors.AuthorID, FirstName, LastName
)
SELECT * FROM AuthorBooks WHERE BookCount > 1;
```

### 6. Derived Tables:

Derived tables are subqueries used in the FROM clause of another SQL statement.

```sql
SELECT * FROM (
  SELECT Authors.AuthorID, FirstName, LastName, COUNT(Books.BookID) AS BookCount
  FROM Authors
  LEFT JOIN Books ON Authors.AuthorID = Books.AuthorID
  GROUP BY Authors.AuthorID, FirstName, LastName
) AS AuthorBooks WHERE BookCount > 1;
```

These advanced SQL queries and techniques allow you to perform complex data manipulations and analyses, enabling you to extract meaningful insights from your datasets.
