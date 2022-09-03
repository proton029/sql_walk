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

- `show warnings` to see what the warning for a particular query was.

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

- **SUBSTRING** : to work with parts of a string. 
    
    
