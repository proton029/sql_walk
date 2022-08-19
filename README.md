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
    
