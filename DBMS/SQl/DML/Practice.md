## Practice SQL

Absolutely, let's create a SQL exam with a mix of questions covering various topics. We'll use the online bookstore example with tables `Books` and `Authors`. Here are the first few questions:

1. **Question 1:**

   - **Task:** Create a table named `Authors` with columns `AuthorID` (integer, primary key), `FirstName` (varchar), and `LastName` (varchar).
   - **Answer:**
     ```sql
     CREATE TABLE Authors (
       AuthorID INT PRIMARY KEY,
       FirstName VARCHAR(255),
       LastName VARCHAR(255)
     );
     ```

2. **Question 2:**

   - **Task:** Insert the following authors into the `Authors` table:
     - AuthorID: 1, FirstName: 'John', LastName: 'Doe'
     - AuthorID: 2, FirstName: 'Jane', LastName: 'Smith'
     - AuthorID: 3, FirstName: 'Michael', LastName: 'Johnson'
   - **Answer:**
     ```sql
     INSERT INTO Authors (AuthorID, FirstName, LastName) VALUES
     (1, 'John', 'Doe'),
     (2, 'Jane', 'Smith'),
     (3, 'Michael', 'Johnson');
     ```

3. **Question 3:**

   - **Task:** Retrieve all columns from the `Authors` table.
   - **Answer:**
     ```sql
     SELECT * FROM Authors;
     ```
   - **Output:**
     ```
     AuthorID | FirstName | LastName
     ---------|-----------|---------
     1        | John      | Doe
     2        | Jane      | Smith
     3        | Michael   | Johnson
     ```

4. **Question 4:**

   - **Task:** Create a table named `Books` with columns `BookID` (integer, primary key), `Title` (varchar), `AuthorID` (integer, foreign key referencing `Authors`), `Genre` (varchar), `Price` (decimal), `PublicationDate` (date), and `StockCount` (integer).
   - **Answer:**
     ```sql
     CREATE TABLE Books (
       BookID INT PRIMARY KEY,
       Title VARCHAR(255),
       AuthorID INT,
       Genre VARCHAR(255),
       Price DECIMAL(10, 2),
       PublicationDate DATE,
       StockCount INT,
       FOREIGN KEY (AuthorID) REFERENCES Authors(AuthorID)
     );
     ```

5. **Question 5:**

   - **Task:** Insert the following books into the `Books` table:
     - BookID: 101, Title: 'Mystery Novel', AuthorID: 1, Genre: 'Mystery', Price: 19.99, PublicationDate: '2023-01-01', StockCount: 50
     - BookID: 102, Title: 'Science Fiction', AuthorID: 2, Genre: 'Sci-Fi', Price: 24.99, PublicationDate: '2023-02-01', StockCount: 30
     - BookID: 103, Title: 'Fantasy Adventure', AuthorID: 3, Genre: 'Fantasy', Price: 29.99, PublicationDate: '2023-03-01', StockCount: 20
   - **Answer:**
     ```sql
     INSERT INTO Books (BookID, Title, AuthorID, Genre, Price, PublicationDate, StockCount) VALUES
     (101, 'Mystery Novel', 1, 'Mystery', 19.99, '2023-01-01', 50),
     (102, 'Science Fiction', 2, 'Sci-Fi', 24.99, '2023-02-01', 30),
     (103, 'Fantasy Adventure', 3, 'Fantasy', 29.99, '2023-03-01', 20);
     ```

6. **Question 6:**

   - **Task:** Retrieve the title and price of all books where the price is greater than $20, and order the result by price in descending order.
   - **Answer:**
     ```sql
     SELECT Title, Price FROM Books WHERE Price > 20 ORDER BY Price DESC;
     ```
   - **Output:**
     ```
     Title              | Price
     -------------------|-------
     Fantasy Adventure  | 29.99
     Science Fiction    | 24.99
     ```

7. **Question 7:**
   - **Task:** Find the total number of books and the average price of books in each genre.
   - **Answer:**
     ```sql
     SELECT Genre, COUNT(*) AS NumberOfBooks, AVG(Price) AS AveragePrice FROM Books GROUP BY Genre;
     ```
   - **Output:**
     ```
     Genre    | NumberOfBooks | AveragePrice
     ---------|---------------
     ```

|--------------
Mystery | 1 | 19.99
Sci-Fi | 1 | 24.99
Fantasy | 1 | 29.99

````

8. **Question 8:**
   - **Task:** Retrieve the full names of authors who have written books in the 'Fantasy' genre.
   - **Answer:**
     ```sql
     SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Authors WHERE AuthorID IN (SELECT AuthorID FROM Books WHERE Genre = 'Fantasy');
     ```
   - **Output:**
     ```
     FullName
     ----------------
     Michael Johnson
     ```


9. **Question 9:**

   - **Task:** Update the price of all 'Sci-Fi' books by increasing it by 10%, and then retrieve the title and updated price of these books.
   - **Answer:**
     ```sql
     UPDATE Books SET Price = Price * 1.1 WHERE Genre = 'Sci-Fi';
     SELECT Title, Price FROM Books WHERE Genre = 'Sci-Fi';
     ```
   - **Output:**
     ```
     Title            | Price
     -----------------|-------
     Science Fiction  | 27.49
     ```

10. **Question 10:**

- **Task:** Delete all books that have a stock count less than 30, and then retrieve all columns from the `Books` table.
- **Answer:**
  ```sql
  DELETE FROM Books WHERE StockCount < 30;
  SELECT * FROM Books;
````

- **Output:**
  ```
  BookID | Title          | AuthorID | Genre   | Price | PublicationDate | StockCount
  -------|----------------|----------|---------|-------|-----------------|------------
  101    | Mystery Novel  | 1        | Mystery | 19.99 | 2023-01-01      | 50
  ```

11. **Question 11:**

- **Task:** Alter the `Books` table to add a new column `Rating` (decimal) to store book ratings.
- **Answer:**
  ```sql
  ALTER TABLE Books ADD COLUMN Rating DECIMAL(3, 2);
  ```

12. **Question 12:**

- **Task:** Update the `Rating` column for the following books:
  - 'Mystery Novel': 4.5
  - 'Science Fiction': 4.0
- **Answer:**
  ```sql
  UPDATE Books SET Rating = 4.5 WHERE Title = 'Mystery Novel';
  UPDATE Books SET Rating = 4.0 WHERE Title = 'Science Fiction';
  ```

13. **Question 13:**

- **Task:** Retrieve the titles of books that have a rating higher than 4 and are priced below $25.
- **Answer:**
  ```sql
  SELECT Title FROM Books WHERE Rating > 4 AND Price < 25;
  ```
- **Output:**
  ```
  Title
  --------------
  Mystery Novel
  ```

14. **Question 14:**

- **Task:** Find the author who has written the most books and retrieve the author's full name and the number of books written.
- **Answer:**
  ```sql
  SELECT CONCAT(FirstName, ' ', LastName) AS FullName, COUNT(BookID) AS NumberOfBooks
  FROM Authors
  JOIN Books ON Authors.AuthorID = Books.AuthorID
  GROUP BY Authors.AuthorID, FirstName, LastName
  ORDER BY NumberOfBooks DESC
  LIMIT 1;
  ```
- **Output:**
  ```
  FullName       | NumberOfBooks
  ---------------|---------------
  John Doe       | 1
  ```

15. **Question 15:**

- **Task:** Retrieve the titles of books that have the word 'Novel' in the title and were published in the year 2023.
- **Answer:**
  ```sql
  SELECT Title FROM Books WHERE Title LIKE '%Novel%' AND YEAR(PublicationDate) = 2023;
  ```
- **Output:**
  ```
  Title
  --------------
  Mystery Novel
  ```

16. **Question 16:**

- **Task:** Calculate the total revenue generated by each genre and retrieve the genre and total revenue, ordered by total revenue in descending order.
- **Answer:**
  ```sql
  SELECT Genre, SUM(Price * StockCount) AS TotalRevenue
  FROM Books
  GROUP BY Genre
  ORDER BY TotalRevenue DESC;
  ```
- **Output:**
  ```
  Genre    | TotalRevenue
  ---------|--------------
  Mystery  | 999.50
  ```

17. **Question 17:**

- **Task:** For each author, retrieve the author's full name and the average rating of their books, excluding authors who have not written any books.
- **Answer:**
  ```sql
  SELECT CONCAT(FirstName, ' ', LastName) AS FullName, AVG(Rating) AS AverageRating
  FROM Authors
  JOIN Books ON Authors.AuthorID = Books.AuthorID
  GROUP BY Authors.AuthorID, FirstName, LastName;
  ```
- **Output:**
  ```
  FullName       | AverageRating
  ---------------|---------------
  John Doe       | 4.5
  ```

18. **Question 18:**

- **Task:** Retrieve the title and genre of books that are the only book in their genre.
- **Answer:**
  ```sql
  SELECT Title, Genre FROM Books
  WHERE Genre IN (
    SELECT Genre FROM Books
    GROUP BY Genre
    HAVING COUNT(*) = 1
  );
  ```
- **Output:**
  ```
  Title          | Genre
  ---------------|-------
  Mystery Novel  | Mystery
  ```

19. **Question 19:**

- **Task:** Update the stock count of all books by decreasing it by 5, and then retrieve the title and updated stock count of books that have a stock count less than 10.
- **Answer:**
  ```sql
  UPDATE Books SET StockCount = StockCount - 5;
  SELECT Title, StockCount FROM Books WHERE StockCount < 10;
  ```
- **Output:**
  ```
  Title | StockCount
  ------|------------
  ```

20. **Question 20:**

- **Task:** Delete authors who have not written any books, and then retrieve all columns from the `Authors` table.
- **Answer:**
  ```sql
  DELETE FROM Authors WHERE AuthorID NOT IN (SELECT AuthorID FROM Books);
  SELECT * FROM Authors;
  ```
- **Output:**
  ```
  AuthorID | FirstName | LastName
  ---------|-----------|---------
  1        | John      | Doe
  ```

21. **Question 21:**

- **Task:** Alter the `Authors` table to add a new column `Country` (varchar) to store the country of the authors.
- **Answer:**
  ```sql
  ALTER TABLE Authors ADD COLUMN Country VARCHAR(255);
  ```

22. **Question 22:**

- **Task:** Update the `Country` column for the following authors:
  - John Doe: 'USA'
  - Jane Smith: 'UK'
  - Michael Johnson: 'Canada'
- **Answer:**
  ```sql
  UPDATE Authors SET Country = 'USA' WHERE FirstName = 'John' AND LastName = 'Doe';
  UPDATE Authors SET Country = 'UK' WHERE FirstName = 'Jane' AND LastName = 'Smith';
  UPDATE Authors SET Country = 'Canada' WHERE FirstName = 'Michael' AND LastName = 'Johnson';
  ```

23. **Question 23:**

- **Task:** Retrieve the full names and countries of authors who are from the 'USA'.
- **Answer:**
  ```sql
  SELECT CONCAT(FirstName, ' ', LastName) AS FullName, Country FROM Authors WHERE Country = 'USA';
  ```
- **Output:**
  ```
  FullName   | Country
  -----------|---------
  John Doe   | USA
  ```

24. **Question 24:**

- **Task:** Find the genre that has the highest average book price and retrieve the genre and the average price.
- **Answer:**
  ```sql
  SELECT Genre, AVG(Price) AS AveragePrice
  FROM Books
  GROUP BY Genre
  ORDER BY AveragePrice DESC
  LIMIT 1;
  ```
- **Output:**
  ```
  Genre    | AveragePrice
  ---------|--------------
  Mystery  | 19.99
  ```

25. **Question 25:**

- **Task:** Retrieve the titles of books that have no corresponding author in the `Authors` table.
- **Answer:**
  ```sql
  SELECT Title FROM Books LEFT JOIN Authors ON Books.AuthorID = Authors.AuthorID WHERE Authors.AuthorID IS NULL;
  ```
- **Output:**
  ```
  Title
  ------
  ```

These questions cover a variety of SQL operations, including altering tables, updating records, joining tables, aggregating data, and handling NULL values. They should help reinforce your understanding of SQL and prepare you for different scenarios you might encounter in interviews or while working with databases.

For mastering these topics I recommed to solve SQL problems on Leetcode.
