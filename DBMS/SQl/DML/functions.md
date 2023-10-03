## SQL Functions

Let's explore various SQL functions using the online bookstore example:

### 1. Aggregate Functions:

Aggregate functions perform calculations on a set of values and return a single value.

- **COUNT**: Returns the number of rows in a set.

  ```sql
  SELECT COUNT(*) FROM Books;
  ```

- **SUM**: Returns the sum of the values in a numeric column.

  ```sql
  SELECT SUM(Price) FROM Books WHERE Genre = 'Fiction';
  ```

- **AVG**: Returns the average value of a numeric column.

  ```sql
  SELECT AVG(Price) FROM Books WHERE Genre = 'Fiction';
  ```

- **MIN**: Returns the minimum value in a set.

  ```sql
  SELECT MIN(Price) AS LowestPrice FROM Books;
  ```

- **MAX**: Returns the maximum value in a set.
  ```sql
  SELECT MAX(PublicationDate) AS LatestPublicationDate FROM Books;
  ```

### 2. Date Functions:

Date functions allow you to perform operations on date values.

- **DATEPART**: Extracts a part of a date value.

  ```sql
  SELECT DATEPART(year, PublicationDate) AS PublicationYear FROM Books;
  ```

- **DATEDIFF**: Calculates the difference between two date values.

  ```sql
  SELECT DATEDIFF(day, '2023-01-01', PublicationDate) AS DaysSince2023 FROM Books;
  ```

- **GETDATE**: Returns the current date and time.
  ```sql
  SELECT Title, GETDATE() AS CurrentDateTime FROM Books;
  ```

### 3. String Functions:

String functions allow you to manipulate string data.

- **CONCAT**: Concatenates two or more strings.

  ```sql
  SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Authors;
  ```

- **SUBSTRING**: Extracts a substring from a string.

  ```sql
  SELECT SUBSTRING(Title, 1, 10) AS ShortTitle FROM Books;
  ```

- **UPPER** and **LOWER**: Convert string to uppercase or lowercase.
  ```sql
  SELECT UPPER(Title) AS UppercaseTitle, LOWER(Title) AS LowercaseTitle FROM Books;
  ```

### 4. Mathematical Functions:

Mathematical functions perform mathematical operations.

- **ROUND**: Rounds a numeric value to the nearest integer or decimal.

  ```sql
  SELECT ROUND(Price, 0) AS RoundedPrice FROM Books;
  ```

- **ABS**: Returns the absolute value of a number.

  ```sql
  SELECT ABS(-Price) AS AbsolutePrice FROM Books;
  ```

- **CEILING** and **FLOOR**: Return the smallest integer greater than or equal to, and the largest integer less than or equal to a number, respectively.
  ```sql
  SELECT CEILING(Price) AS CeilingPrice, FLOOR(Price) AS FloorPrice FROM Books;
  ```

### 5. Conversion Functions:

Conversion functions convert a value from one data type to another.

- **CAST**: Converts a value to a specified data type.

  ```sql
  SELECT CAST(Price AS INT) AS IntegerPrice FROM Books;
  ```

- **CONVERT**: Similar to CAST, but with a different syntax and additional options.
  ```sql
  SELECT CONVERT(INT, Price) AS IntegerPrice FROM Books;
  ```

These functions are essential tools for transforming and analyzing data in SQL, allowing you to derive meaningful insights from your dataset.
