## Data Manipulation Language (DML)

Data Manipulation Language (DML) is used to retrieve, insert, modify, and delete data in database tables. Let's explore each of the DML commands:

### 1. SELECT:

The `SELECT` statement is used to retrieve data from one or more tables.

**Example 1**: Retrieve all columns from the "Books" table.

```sql
SELECT * FROM Books;
```

**Example 2**: Retrieve specific columns (Title and Price) from the "Books" table.

```sql
SELECT Title, Price FROM Books;
```

**Example 3**: Retrieve books with a price greater than $20.

```sql
SELECT Title, Price FROM Books WHERE Price > 20;
```

**Example 4**: Retrieve books sorted by publication date in descending order.

```sql
SELECT Title, PublicationDate FROM Books ORDER BY PublicationDate DESC;
```

### 2. INSERT:

The `INSERT` statement is used to add new records to a table.

**Example**: Insert a new book into the "Books" table.

```sql
INSERT INTO Books (BookID, Title, AuthorID, Genre, Price, ISBN, PublicationDate, StockCount)
VALUES (101, 'Sample Book', 1, 'Fiction', 19.99, '1234567890123', '2023-01-01', 100);
```

### 3. UPDATE:

The `UPDATE` statement is used to modify existing records in a table.

**Example 1**: Update the price of a book with BookID = 101 to $25.

```sql
UPDATE Books
SET Price = 25
WHERE BookID = 101;
```

**Example 2**: Decrease the stock count by 1 for a book with ISBN '1234567890123'.

```sql
UPDATE Books
SET StockCount = StockCount - 1
WHERE ISBN = '1234567890123';
```

### 4. DELETE:

The `DELETE` statement is used to remove records from a table.

**Example 1**: Delete the book with BookID = 101 from the "Books" table.

```sql
DELETE FROM Books WHERE BookID = 101;
```

**Example 2**: Delete all books that have a stock count of 0.

```sql
DELETE FROM Books WHERE StockCount = 0;
```

**Note**: It's essential to be cautious when using the `UPDATE` and `DELETE` commands, especially without a `WHERE` clause, as they can modify or remove multiple records at once. Always ensure you have backups of your data and understand the implications of the changes you're making.
