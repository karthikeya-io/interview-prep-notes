## Grouping Data

The `GROUP BY` and `HAVING` clauses in SQL are used to arrange identical data into groups and filter the grouped data, respectively. Let's explore these clauses using the online bookstore example:

### 1. GROUP BY:

The `GROUP BY` statement groups rows that have the same values in specified columns into summary rows, like "find the total quantity of each product sold". It is often used with aggregate functions to perform calculations on each group of rows.

**Example 1**: Count the number of books in each genre.

```sql
SELECT Genre, COUNT(*) AS NumberOfBooks
FROM Books
GROUP BY Genre;
```

**Example 2**: Calculate the average price of books in each genre.

```sql
SELECT Genre, AVG(Price) AS AveragePrice
FROM Books
GROUP BY Genre;
```

**Example 3**: Find the total stock count for books by each author.

```sql
SELECT AuthorID, SUM(StockCount) AS TotalStockCount
FROM Books
GROUP BY AuthorID;
```

### 2. HAVING:

The `HAVING` clause was added to SQL because the `WHERE` keyword could not be used with aggregate functions. It is used to filter the results of a `GROUP BY` query based on a condition applied to the aggregated data.

**Example 1**: Find genres where the average price of books is greater than $20.

```sql
SELECT Genre, AVG(Price) AS AveragePrice
FROM Books
GROUP BY Genre
HAVING AVG(Price) > 20;
```

**Example 2**: List authors who have more than 3 books published.

```sql
SELECT AuthorID, COUNT(BookID) AS NumberOfBooks
FROM Books
GROUP BY AuthorID
HAVING COUNT(BookID) > 3;
```

**Example 3**: Find genres that have a total stock count of more than 100 books.

```sql
SELECT Genre, SUM(StockCount) AS TotalStockCount
FROM Books
GROUP BY Genre
HAVING SUM(StockCount) > 100;
```

The combination of `GROUP BY` and `HAVING` allows you to perform sophisticated data analysis by grouping data into meaningful categories and applying conditions to the aggregated results.
