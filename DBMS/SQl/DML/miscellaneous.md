## Miscellaneous

### 1. Analytic Functions:

Analytic functions are used to perform complex calculations and are very useful for solving problems requiring calculations across rows in a result set.

#### a) Window Functions:

- **ROW_NUMBER()**: Assigns a unique number to each row within the partition of a result set.

  ```sql
  SELECT Title, Genre, ROW_NUMBER() OVER(PARTITION BY Genre ORDER BY Price) AS RowNum
  FROM Books;
  ```

- **RANK() and DENSE_RANK()**: Assigns a rank to each row within a partition of a result set. `RANK()` leaves gaps in rank sequence when there are tied rows, whereas `DENSE_RANK()` does not.

  ```sql
  SELECT Title, Genre, RANK() OVER(PARTITION BY Genre ORDER BY Price) AS Rank,
         DENSE_RANK() OVER(PARTITION BY Genre ORDER BY Price) AS DenseRank
  FROM Books;
  ```

- **NTILE(n)**: Divides the result set into a specified number of approximately equal parts.

  ```sql
  SELECT Title, Genre, NTILE(2) OVER(PARTITION BY Genre ORDER BY Price) AS Tile
  FROM Books;
  ```

- **LAG() and LEAD()**: Access data from a previous row (LAG) or a following row (LEAD) in the result set.

  ```sql
  SELECT Title, Price, LAG(Price) OVER(ORDER BY Price) AS PrevPrice,
         LEAD(Price) OVER(ORDER BY Price) AS NextPrice
  FROM Books;
  ```

- **FIRST_VALUE() and LAST_VALUE()**: Return the first or last value in an ordered set of values.
  ```sql
  SELECT Title, Genre, FIRST_VALUE(Title) OVER(PARTITION BY Genre ORDER BY Price) AS FirstBook,
         LAST_VALUE(Title) OVER(PARTITION BY Genre ORDER BY Price ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS LastBook
  FROM Books;
  ```

#### b) Running Totals and Moving Averages:

- **Running Total**:

  ```sql
  SELECT Title, Price, SUM(Price) OVER(ORDER BY PublicationDate) AS RunningTotal
  FROM Books;
  ```

- **Moving Average**:
  ```sql
  SELECT Title, Price, AVG(Price) OVER(ORDER BY PublicationDate ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS MovingAverage
  FROM Books;
  ```

### 2. Pivot and Unpivot Data:

#### a) PIVOT:

- Transforms data from rows to columns.
  ```sql
  SELECT * FROM (
    SELECT Title, Genre, Price
    FROM Books
  ) AS SourceTable
  PIVOT (
    AVG(Price)
    FOR Genre IN ([Mystery], [Sci-Fi], [Fantasy])
  ) AS PivotTable;
  ```

#### b) UNPIVOT:

- Transforms data from columns to rows.
  ```sql
  SELECT Title, Genre, Price
  FROM (
    SELECT Title, Mystery, Sci-Fi, Fantasy
    FROM PivotTable
  ) AS SourceTable
  UNPIVOT (
    Price FOR Genre IN (Mystery, Sci-Fi, Fantasy)
  ) AS UnpivotTable;
  ```

### 3. Data Transformation and Cleaning:

#### a) NULL handling:

- **IS NULL, IS NOT NULL**:

  ```sql
  SELECT Title FROM Books WHERE Rating IS NULL;
  ```

- **COALESCE()**: Returns the first non-null value in a list.

  ```sql
  SELECT Title, COALESCE(Rating, 'Not Rated') AS Rating FROM Books;
  ```

- **NULLIF()**: Returns a null value if the two specified expressions are equal.
  ```sql
  SELECT Title, NULLIF(Price, 0) AS Price FROM Books;
  ```

#### b) CASE statement:

- For conditional logic.
  ```sql
  SELECT Title, Price,
         CASE WHEN Price < 20 THEN 'Cheap'
              WHEN Price BETWEEN 20 AND 30 THEN 'Moderate'
              ELSE 'Expensive'
         END AS PriceCategory
  FROM Books;
  ```

#### c) Data type conversion:

- **CAST() and CONVERT()**:
  ```sql
  SELECT Title, CAST(Price AS INT) AS RoundedPrice FROM Books;
  ```

### 4. Indexes and Performance Tuning:

#### a) Understanding Execution Plans:

- Execution plans provide a visual representation of the steps SQL Server takes to execute a query.
- It helps in identifying performance bottlenecks, such as table scans, index scans, or missing indexes.

#### b) Creating and Managing Indexes:

- Indexes are used to speed up the retrieval of rows from a database table.
- Example of creating an index:
  ```sql
  CREATE INDEX idx_books_genre ON Books(Genre);
  ```

#### c) Query Optimization Techniques:

- Use `EXPLAIN` to analyze the execution plan of a query.
- Avoid using `SELECT *`.
- Use appropriate indexing.
- Avoid using non-sargable queries (e.g., using functions on columns in the WHERE clause).

### 5. Stored Procedures and Triggers:

#### a) Creating and Executing Stored Procedures:

- Stored Procedures are precompiled collections of SQL statements stored under a name and processed as a unit.
- Example of creating and executing a stored procedure:

  ```sql
  CREATE PROCEDURE GetBooksByGenre @Genre VARCHAR(255)
  AS
  BEGIN
    SELECT * FROM Books WHERE Genre = @Genre;
  END;

  EXEC GetBooksByGenre 'Mystery';
  ```

#### b) Understanding and Implementing Triggers:

- Triggers are special types of stored procedures that are defined to execute automatically in response to certain events on a particular table or view.
- Example of creating a trigger:
  ```sql
  CREATE TRIGGER trg_after_insert_books
  AFTER INSERT
  ON Books FOR EACH ROW
  BEGIN
    INSERT INTO AuditLog (Action, TableName, RecordID, ChangeDate)
    VALUES ('INSERT', 'Books', NEW.BookID, NOW());
  END;
  ```

### 6. Data Transformation and Cleaning (Continued):

#### d) Data Type Conversion (Continued):

- **CONVERT()** function is used to convert an expression of one data type to another.
  ```sql
  SELECT Title, CONVERT(VARCHAR, PublicationDate, 103) AS FormattedDate FROM Books;
  ```

### 7. Analytic Functions (Continued):

#### c) Pivot and Unpivot Data (Continued):

- **UNPIVOT** Example (Continued):
  ```sql
  SELECT Genre, [John Doe] AS Author, BookTitle
  FROM (SELECT Authors.FirstName + ' ' + Authors.LastName AS Author, Books.Title AS BookTitle, Genre
        FROM Books INNER JOIN Authors ON Books.AuthorID = Authors.AuthorID) AS SourceTable
  UNPIVOT (BookTitle FOR Author IN ([John Doe])) AS UnpivotTable;
  ```
