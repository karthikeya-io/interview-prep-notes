## Data Definition Language (DDL)

### Common DDL Keywords:

1. **CREATE**: Used to create database objects like tables, views, indexes, etc.

   - `CREATE TABLE`: Creates a new table.
   - `CREATE INDEX`: Creates an index on one or more columns.
   - `CREATE VIEW`: Creates a view based on the result of a SELECT statement.

2. **ALTER**: Used to modify existing database objects.

   - `ALTER TABLE`: Modifies an existing table. You can use it to add, delete, or modify columns, and to add or drop constraints.

3. **DROP**: Used to delete database objects.

   - `DROP TABLE`: Deletes an existing table and all its data.
   - `DROP INDEX`: Deletes an index.
   - `DROP VIEW`: Deletes a view.

4. **PRIMARY KEY**: A constraint that uniquely identifies each record in a table. Each table can have only one primary key.

5. **FOREIGN KEY**: A key used to link two tables together. It is a field (or collection of fields) in one table that refers to the primary key in another table.

6. **UNIQUE**: A constraint that ensures that all values in a column are distinct.

7. **AUTO_INCREMENT**: A keyword used in some databases (like MySQL) to automatically generate a unique value for a primary key column.

8. **DEFAULT**: Specifies a default value for a column when a new record is inserted.

9. **CHECK**: A constraint that ensures that all values in a column satisfy certain conditions.

10. **INDEX**: Used to create and retrieve data from the database more quickly.

### Common Data Types:

1. **INTEGER (or INT)**: Represents whole numbers, both positive and negative.

2. **DECIMAL (or NUMERIC)**: Represents numbers with decimal points. You can define the maximum number of digits to the left and right of the decimal point.

3. **VARCHAR**: Represents variable-length character strings. You must specify the maximum length.

4. **CHAR**: Represents fixed-length character strings. You specify the string length.

5. **TEXT**: Used for long character strings.

6. **DATE**: Represents date values in the format YYYY-MM-DD.

7. **TIME**: Represents time values in the format HH:MM:SS.

8. **DATETIME**: Represents a combination of date and time.

9. **BOOLEAN (or BOOL)**: Represents true or false values.

10. **BLOB**: Used to store binary data, like images or files.

11. **FLOAT (or REAL)**: Represents numbers with decimal points. They are approximate numeric values.

12. **DOUBLE**: Represents double-precision floating point numbers.

Different databases might have variations or additional data types specific to them. It's essential to refer to the documentation of the specific database system you're working with to understand the nuances and best practices associated with each data type.

## Example: Online Bookstore

### CREATE command Examples:

### 1. Authors Table:

```sql
CREATE TABLE Authors (
    AuthorID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Biography TEXT
);
```

### 2. Books Table:

```sql
CREATE TABLE Books (
    BookID INT AUTO_INCREMENT PRIMARY KEY,
    Title VARCHAR(100) NOT NULL,
    AuthorID INT NOT NULL,
    Genre VARCHAR(50),
    Price DECIMAL(10,2) NOT NULL,
    ISBN VARCHAR(13) UNIQUE NOT NULL,
    PublicationDate DATE,
    StockCount INT NOT NULL DEFAULT 0,
    FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
);
```

### 3. Customers Table:

```sql
CREATE TABLE Customers (
    CustomerID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Password VARCHAR(255) NOT NULL, -- Assuming hashed password storage
    Address TEXT,
    Phone VARCHAR(15)
);
```

### 4. Orders Table:

```sql
CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT NOT NULL,
    OrderDate DATE NOT NULL DEFAULT CURRENT_DATE,
    TotalAmount DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

### 5. OrderDetails Table:

```sql
CREATE TABLE OrderDetails (
    OrderDetailID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT NOT NULL,
    BookID INT NOT NULL,
    Quantity INT NOT NULL,
    SubTotal DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (BookID) REFERENCES Books(BookID)
);
```

These `CREATE TABLE` commands will set up the necessary tables for our online bookstore. The `AUTO_INCREMENT` attribute is used to automatically generate a unique value for the primary key columns. The `FOREIGN KEY` constraints establish relationships between tables, ensuring data integrity.

If you need to make modifications to the table structure in the future, you can use the `ALTER` command. For instance, to add a new column or modify an existing one. If you need to remove a table, you can use the `DROP` command.

### ALTER Command Examples:

1. **Add a New Column**:
   Suppose you want to add a new column named "MiddleName" to the "Customers" table.

   ```sql
   ALTER TABLE Customers ADD MiddleName VARCHAR(50);
   ```

2. **Modify an Existing Column**:
   If you want to change the data type or size of the "Email" column in the "Customers" table.

   ```sql
   ALTER TABLE Customers MODIFY Email VARCHAR(150);
   ```

3. **Rename a Column**:
   To rename the "Phone" column to "ContactNumber" in the "Customers" table.

   ```sql
   ALTER TABLE Customers RENAME COLUMN Phone TO ContactNumber;
   ```

4. **Drop a Column**:
   If you decide that the "MiddleName" column is no longer needed in the "Customers" table.

   ```sql
   ALTER TABLE Customers DROP COLUMN MiddleName;
   ```

5. **Add a Primary Key**:
   To add a primary key constraint to the "BookID" column in the "Books" table.

   ```sql
   ALTER TABLE Books ADD PRIMARY KEY (BookID);
   ```

6. **Add a Foreign Key**:
   To add a foreign key constraint between the "AuthorID" columns of the "Books" and "Authors" tables.

   ```sql
   ALTER TABLE Books ADD FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID);
   ```

7. **Drop a Constraint**:
   To remove a foreign key constraint from the "Books" table.
   ```sql
   ALTER TABLE Books DROP FOREIGN KEY [constraint_name];
   ```
   Note: Replace `[constraint_name]` with the actual name of the foreign key constraint.

### DROP Command Examples:

1. **Drop a Table**:
   If you decide that the "TempData" table is no longer needed.

   ```sql
   DROP TABLE TempData;
   ```

2. **Drop an Index**:
   To remove an index named "idx_book_title" from the "Books" table.

   ```sql
   DROP INDEX idx_book_title ON Books;
   ```

3. **Drop a View**:
   If you have a view named "TopSellingBooks" and want to remove it.
   ```sql
   DROP VIEW TopSellingBooks;
   ```

Remember, the `DROP` command deletes objects permanently, so use it with caution. Always ensure you have backups of your data and understand the implications of the changes you're making.
