# sql_walk

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
     OR
    
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
    
    
