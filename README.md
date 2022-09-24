# sql_walk

- SQL is case **INSENSITIVE**
- `show databases;` => to show the databases present
- `use databaseName;` => to use a DB
- `desc tablename;` => to show the description of a table
- `show columns from tableName;` => another way for 'desc tablename'
- `create table 'tableName'(
                            colmnName datatype,
                            colmnName datatype
                            );`=> create a table 
- `DROP TABLE tablename;` => to delete a table 

- `INSERT INTO table_name(column_name) VALUES (data);` => to insert into a column

- `select * from tablename;` => to view all the table row data

- `insert into table_name
                         (column_name, column_name)
                         values (value, value),
                                 (value, value)
                                (value, value)
                                (value, value);`  => to insert multiple values
                                
- To insert quotes inside of inserted values `'This text has \'quotes\' in it'`

- `show warnings` to see the warnings for a particular query.

- `set sql_mode='';` to supress the warnings
- `CREATE TABLE cats3
  (
    name VARCHAR(20) DEFAULT 'no name provided',
    age INT DEFAULT 99
  );` setting a default value when no value is passed to a column.

- `CREATE TABLE cats4
  (
    name VARCHAR(20) NOT NULL DEFAULT 'unnamed',
    age INT NOT NULL DEFAULT 99
  );` combining default and not null 

- ```  
  CREATE TABLE unique_cats
            (
              cat_id INT NOT NULL,
              name VARCHAR(100),
              age INT,
              PRIMARY KEY (cat_id)
            );
     **OR**
    
    CREATE TABLE employees (
    id INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    middle_name VARCHAR(255),
    age INT NOT NULL,
    current_status VARCHAR(255) NOT NULL DEFAULT 'employed'
    );
  ```
  => setting a field as primary key
  
 - ```
    CREATE TABLE unique_cats2 (
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
    );
    ```
    => adding  auto increment
    
  ------------------------------


  # **CRUD OPERATIONS**
  ------------------------------

  - We have already discussed the Insert into method previously.

  - We have already discussed the `Select * from tableName`. Here the '*' Reads all the columns fromt the table specified But also we can specify which column we           want like `select name from cats` or `select name, place, breed from cats`. Note that the columns displayed will be in the order one specifies in the select           command.

  - We can be more specific with the ***Where*** clause `select * from cats where cat_id=2` will fetch all column data where cat_id field equals 2 
    **OR**
    `Select name, breed from cats where place='kollam'`

  - **Aliases** are a useful way to change the way the data is displayed to the user. `select name as dogsName from dogs` with display the name column as 'dogsName'
    but nothing will be changed in the actual table. It is just for users convinience.

  - The **Update** command lets you update the data in the table. A good rule of thumb says that we must use the select statement to target the data first to verify
    whether it is returning the data we want and then go for updating the data.`UPDATE cats SET breed='Shorthair' WHERE breed='Tabby'; `. Here 'cats' is the table         name and **SET** is used to update the column 'breed'.

  - **Delete** To delete and entry from the table `DELETE FROM cats WHERE name='Egg';`. **Note** that `DELETE FROM CATS` will delete all rows in table 'CATS'.
  
  - Note that we should always target the data first using the select statement before going to delete it.
 
 
## **String Functions**

- **concat** used to combine data for cleaner output. Basically takes data from columns and concatenate row wise. 
  ```
        SELECT
        CONCAT(author_fname, ' ', author_lname)
        FROM books;

      SELECT
        CONCAT(author_fname, ' ', author_lname)
        AS 'full name'
      FROM books;

      SELECT author_fname AS first, author_lname AS last, 
        CONCAT(author_fname, ' ', author_lname) AS full
      FROM books;

      SELECT author_fname AS first, author_lname AS last, 
        CONCAT(author_fname, ', ', author_lname) AS full
      FROM books;

      SELECT CONCAT(title, '-', author_fname, '-', author_lname) FROM books;

      SELECT 
          CONCAT_WS(' - ', title, author_fname, author_lname) 
      FROM books;
  ```
-  **CONCAT_WS** is used to add separators. Useful when there are lot of columns to concat.

- **SUBSTRING** : to work with parts of a sring. 
  - ` select substring('Hello Mom and Dad',1, 4 );`  note that the index starts at 1 so the result of this query is "hell".
  - In **SUBSTRING** if we give only one value as index then the query will start at that index and returns the rest of the string
    i.e. ` select substring('Hello Mom and Dad', 4 );` will give "lo M".
  - If we give a negative number then the query will return a substring starting from its end and going reverse direction and fetches the string i.e.
    ` select substring('Hello Mom and Dad', -3 );` will return "Dad"
  - ` SELECT SUBSTRING(title, 1, 10) FROM books;` will return the substring of the entries in "title" column in books table
  -  ``` 
      SELECT CONCAT
        (
          SUBSTRING(title, 1, 10),
          '...'
        )
      FROM books;
     ```
      => this will run the **Subquery** first and then the ***Outer query*** effectivey taking the substring and concatenating "... "    
    
 - **REPLACE**
  
    - Used to replace parts of strings. Ex: ` SELECT REPLACE(title, 'e ', '3') FROM books;`
  
 - **REVERSE**
  
    - Reverses a string. Ex ` SELECT REVERSE(author_fname) FROM books;`
 
 - **CHAR_LENGTH**
  
    - Returns the length of the string.
      Examples...
    ```
      SELECT CHAR_LENGTH('Hello World');
 
      SELECT author_lname, CHAR_LENGTH(author_lname) AS 'length' FROM books;

      SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long') FROM books;
      
    ```
 
 - **UPPER() and LOWER()**
    - to change a string's case, Examples..
    ```
      SELECT UPPER('Hello World');

      SELECT LOWER('Hello World');

      SELECT UPPER(title) FROM books;

      SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;

      SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;

    ```
    - **Note:** UPPER only takes one argument and CONCAT takes two or more arguments, so they can't be switched in that way.
    - **LEFT & RIGHT** `SELECT LEFT('SQL Tutorial', 3) AS ExtractString;` returns SQL as output i.e. starting from left of the string take 3 characters.
        RIGHT us similar to LEFT but starts from the right side of the string. 

## Refining selection statements

- **DISTINCT** is used to select unique items in a column(s) and this keyword is used just after the select statement.
    Run the following to see how DISTINCT can be made useful
    ```
      SELECT author_lname FROM books;
 
      SELECT DISTINCT author_lname FROM books;

      SELECT author_fname, author_lname FROM books;

      SELECT DISTINCT CONCAT(author_fname,' ', author_lname) FROM books; // this concats the two columns and give the unique among them

      SELECT DISTINCT author_fname, author_lname FROM books; // this works on the rows and donot concat
    
    ```
- **ORDER BY** is used to sort the data. works for both Numbers and alphabets.

    ```
      SELECT author_lname FROM books;

      SELECT author_lname FROM books ORDER BY author_lname;

      SELECT title FROM books;

      SELECT title FROM books ORDER BY title;
      SELECT author_lname FROM books ORDER BY author_lname DESC; // to sort decending

      SELECT released_year FROM books;

      SELECT released_year FROM books ORDER BY released_year;

      SELECT released_year FROM books ORDER BY released_year DESC;

      SELECT released_year FROM books ORDER BY released_year ASC;

      SELECT title, released_year, pages FROM books ORDER BY released_year;

      SELECT title, pages FROM books ORDER BY released_year;

      SELECT title, author_fname, author_lname 
      FROM books ORDER BY 2;                      // is a short cut to ORDER BY "author_fname"

      SELECT title, author_fname, author_lname 
      FROM books ORDER BY 3;                      // is a short cut to ORDER BY "author_lname"

      SELECT title, author_fname, author_lname 
      FROM books ORDER BY 1;                      // is a short cut to ORDER BY "title"

      SELECT title, author_fname, author_lname 
      FROM books ORDER BY 1 DESC;

      SELECT author_lname, title
      FROM books ORDER BY 2;

      SELECT author_fname, author_lname FROM books 
      ORDER BY author_lname, author_fname;
    
    ```
 - **LIMIT** : Allows us to specify a limit of how many results are to be returned. The limit condition, in most cases is added at the end of a query.
    - ` SELECT title FROM books LIMIT 3;` OR `SELECT title FROM books LIMIT 0,3;`
    
    - Specifying a huge number as ending point will fetch all data till the end.
    
 - **LIKE** : Basically used for better searching or searching for patterns. ` SELECT title, author_fname FROM books WHERE author_fname LIKE '%da%';`
              Here the query is setup to search for 'da' patterns in author_fname.
    - we can use more wild cards such as the '_' (underscore). We can use four underscores(____) to specify that we are looking for a single character.
    - `SELECT title, stock_quantity FROM books WHERE stock_quantity LIKE '____';` will return rows with stock quantity having 4 digits or characters.
    - If We want to search for data that has '%' in it then '%%%' in LIKE wont work. We need to use '\' `SELECT title FROM books WHERE title LIKE               '%\%%'`. Same for searching Underscores `...LIKE '%\_%'`.
    
## Aggregate Functions

- **COUNT** : To count the entries.
  ```
  SELECT COUNT(*) FROM books;
 
  SELECT COUNT(author_fname) FROM books;
 
  SELECT COUNT(DISTINCT author_fname) FROM books;
 
  SELECT COUNT(DISTINCT author_lname) FROM books;
 
  SELECT COUNT(DISTINCT author_lname, author_fname) FROM books;
  
  SELECT COUNT(*) FROM books WHERE title LIKE '%the%';
  ```
 - **GROUP BY**: Summarizes or aggregates identical data into single rows. Example: is in our books table we can write a query to group the books in the                  year in which they were released.
    For understanding test out the results of below queries
    ```
      SELECT title, author_lname FROM books;
 
      SELECT title, author_lname FROM books
      GROUP BY author_lname;
 
      SELECT author_lname, COUNT(*) 
      FROM books GROUP BY author_lname;
 
 
      SELECT title, author_fname, author_lname FROM books;

      SELECT title, author_fname, author_lname FROM books GROUP BY author_lname;

      SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname;

      SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname, author_fname;

      SELECT released_year FROM books;

      SELECT released_year, COUNT(*) FROM books GROUP BY released_year;

      SELECT CONCAT('In ', released_year, ' ', COUNT(*), ' book(s) released') AS year FROM books GROUP BY released_year;
    
    ```
- **MIN and MAX** : To find max/min entries in a column `SELECT MIN(released_year) FROM books;`
- **The problem with MIN and MAX**: If we run the query `SELECT MAX(pages), title from books;` The result will be wrong because the max pages book wont       be aligned to the book title column that is being displayed. That is the query just picks up the max pages and the first title name of the book in       the table. So an obvious solution will be to use SubQueries `SELECT * FROM books WHERE pages = (SELECT Min(pages) FROM books); ` OR `SELECT * FROM       books ORDER BY pages ASC LIMIT 1;`
- **MIN & MAX with GROUP BY**: `SELECT author_fname, author_lname, Min(released_year) FROM   books GROUP  BY author_lname, author_fname;` Here the Group     by command will take the firstname and lastname , join it and conider it as a group and fetches items mentioned in the select query. Below is a           cleaner output query with the use of aliases.
    ```
      SELECT
      CONCAT(author_fname, ' ', author_lname) AS author,
      MAX(pages) AS 'longest book'
      FROM books
      GROUP BY author_lname,
             author_fname;
    ```
- **SUM** Function `SELECT SUM(pages)FROM books;` Takes the sum of all pages from books table.
  ```
    SELECT author_fname,
       author_lname,
       Sum(released_year)
    FROM books
    GROUP BY
        author_lname,
        author_fname;
  ```
- **AVG**: Similar to sum, it returns the avg value of a column `SELECT AVG(released_year) FROM books;`
