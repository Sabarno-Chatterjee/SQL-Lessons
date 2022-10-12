# SQL-Lessons

This file consists of all the notes from SQL classes.

* mysql-ctl cli

    This is used to start the mysql server.

* SHOW DATABASES;

    This is use to see the existing databases on the server.


* CREATE DATABASE database_name;

    As the name suggests, used to create a database.

* DROP DATABASE database_name;

    To delete a database.

* USE <database name>;

    To use a specific database.

* SELECT database();

    To check the current database.

*  CREATE TABLE tablename
  (
    column_name data_type,
    column_name data_type
  );

* SHOW TABLES;

    All the tables present in the current database is displayed.

* SHOW COLUMNS FROM tablename;

    All the types of columns from the selected table is displayed.

* DESC tablename;

    Has a similar output as the previous. Has a different use which is yet to learn.


* INSERT INTO table_name(column_name) VALUES (data);

    eg : INSERT INTO cats(name, age) VALUES ('Jetson', 7);

* SELECT * FROM <table_name>;

    To view all the data of the selected table.


* Multiple Inserts:

    INSERT INTO table_name 
            (column_name, column_name) 
    VALUES      (value, value), 
                (value, value), 
                (value, value);

* SHOW WARNINGS;

    To check for the warnings in the CLI(Command LIne Interface)


* NOT NULL constraints:


    CREATE TABLE tablename
  (
    column_name data_type NOT NULL,
    column_name data_type NOT NULL
  );


* DEFAULT VALUES:

    CREATE <table_name>
  (
    name VARCHAR(20) DEFAULT 'no name provided',
    age INT DEFAULT 99
  );


* PRIMARY KEYS:

    CREATE TABLE <table_name>
  (
    cat_id INT NOT NULL,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
  );


* AUTO_INCREMENT:


    CREATE TABLE <table_name>
    (
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
    );


* ALIASES:

    Used to change the name of the columns during display.

    eg:

    SELECT cat_id AS id, name FROM cats;
 
    SELECT name AS 'cat name', breed AS 'kitty breed' FROM cats;
 
    DESC cats;


***CRUD OPERATIONS***



* CREATE 

    Which is basically entering some data.

    eg:

    INSERT INTO cats(name, age) VALUES(‘Taco’, 14);


* SELECT OR READ


    Used to view to content as per our need. "*" is used to view all the coloumnf of the table.


    SELECT * FROM <table_name>; 

    SELECT <column_name> FROM <table_name>; 


* UPDATE:



    Used to update a piece of data.


    eg:


    UPDATE cats SET breed='Shorthair' WHERE breed='Tabby';


* DELETE 


    DELETE FROM cats WHERE name='Egg';

    OR 

    DELETE FROM cats; (This will remove all the data but the table still exists.)


***STRING FUNCTIONS***




*   CONCAT


    Combine data for cleaner output.

    eg:


    SELECT
    CONCAT(author_fname, ' ', author_lname)
    AS 'full name'  
    FROM books;



* SUBSTRING:


    SELECT SUBSTRING('Hello World', 1, 4);

    Output: Hell

    Eg of usig substring along with other string functions like 'Concat';

    SELECT CONCAT(SUBSTRING(title,1,10),'...') AS 'Short title' FROM books;



* REPLACE:


    SELECT REPLACE('Hello World', 'Hell', '%$#@');


* REVERSE:


    SELECT REVERSE('Hello World');


* CHARACTER LENGTH:


    SELECT CHAR_LENGTH('Hello World');


* UPPER & LOWER:


    SELECT UPPER('Hello World');
 
    SELECT LOWER('Hello World');


* DISTINCT:


    SELECT DISTINCT author_lname FROM books;


* ORDER BY:


    SELECT author_lname FROM books ORDER BY author_lname;

    OR 

    SELECT title, author_fname, author_lname 
    FROM books ORDER BY 2;
     
     ('2' will basically select 'author_fname' in this case).



* LIMIT:


    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 5;

        {Will display 5 rows in desc order}

    or

    SELECT title, released_year FROM books 
    ORDER BY released_year DESC LIMIT 5,3;

        {In this case the list will begin from 5 from row and display the next 3 rows.}













