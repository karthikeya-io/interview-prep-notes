## Filtering and Sorting Data

Filtering and sorting data using SQL, specifically focusing on the `WHERE`, `ORDER BY`, `DISTINCT`, `LIMIT`, and `OFFSET` clauses. We'll use the online bookstore example for demonstration.

### 1. WHERE Clause with Conditions:

The `WHERE` clause is used to filter records based on one or more conditions. It is used to extract only those records that fulfill a specified condition.

**Example**: Retrieve all books that belong to the 'Fiction' genre.

```sql
SELECT * FROM Books WHERE Genre = 'Fiction';
```

**Example**: Retrieve all books with a price less than $20.

```sql
SELECT * FROM Books WHERE Price < 20;
```

**Example**: Retrieve all books published after '2022-01-01' and have a stock count greater than 10.

```sql
SELECT * FROM Books WHERE PublicationDate > '2022-01-01' AND StockCount > 10;
```

### 2. ORDER BY:

The `ORDER BY` clause is used to sort the result set in ascending or descending order based on one or more columns.

**Example**: Retrieve all books and sort them by title in ascending order.

```sql
SELECT * FROM Books ORDER BY Title ASC;
```

**Example**: Retrieve all books and sort them by price in descending order.

```sql
SELECT * FROM Books ORDER BY Price DESC;
```

**Example**: Retrieve all books and sort them first by genre in ascending order and then by price in descending order within each genre.

```sql
SELECT * FROM Books ORDER BY Genre ASC, Price DESC;
```

### 3. DISTINCT:

The `DISTINCT` keyword is used to return only distinct (unique) values in the result set.

**Example**: Retrieve a list of unique genres available in the "Books" table.

```sql
SELECT DISTINCT Genre FROM Books;
```

**Example**: Retrieve a list of unique author IDs from the "Books" table.

```sql
SELECT DISTINCT AuthorID FROM Books;
```

### 4. LIMIT and OFFSET:

The `LIMIT` clause is used to constrain the number of rows returned by the SQL query. The `OFFSET` clause is used to specify the starting point for the rows to be retrieved.

**Example**: Retrieve the first 5 books from the "Books" table.

```sql
SELECT * FROM Books LIMIT 5;
```

**Example**: Retrieve 5 books from the "Books" table, skipping the first 10 books.

```sql
SELECT * FROM Books LIMIT 5 OFFSET 10;
```

**Example**: Retrieve the top 3 most expensive books in the "Books" table.

```sql
SELECT * FROM Books ORDER BY Price DESC LIMIT 3;
```

These SQL clauses and keywords are fundamental for filtering, sorting, and limiting the data retrieved from the database, allowing you to perform detailed and specific data analysis. By combining these clauses, you can construct complex queries to extract the exact information you need from your dataset.
