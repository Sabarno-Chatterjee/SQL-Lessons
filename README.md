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






