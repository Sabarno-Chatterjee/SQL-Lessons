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

    Eg of using substring along with other string functions like 'Concat';

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




* LIKE:


    SELECT title, author_fname FROM books WHERE author_fname LIKE '%da%';

        {this will display all the books where author's there is a "da" present in the author's first name}

    SELECT title, author_fname FROM books WHERE author_fname LIKE 'da%';


        {this will display all the books where the author's name begin's with "da"}

        {% is basically like a wildcard, leaves the option to filter anything before or after the 'da' it}


    SELECT title, stock_quantity FROM books WHERE stock_quantity LIKE '____';

        {In this case '____' will search for that many characters in the stock, lets say you want to look for books which have a stock in 2 digits... '__' can be used for that}

    

* COUNT()


    SELECT COUNT(*) FROM <table_name>;


* GROUP BY()


    {Using GROUP BY, by itself isn't of much use, instead it's used with other aggregator functions like COUNT(), MIN(),MAX()... which in turn helps derive sense out of the data.}


    SELECT author_fname, author_lname, COUNT(*) FROM books GROUP BY author_lname;


* MAX() OR MIN()



    SELECT MIN(released_year) FROM books;
     
    
* SUB-QUERIES:


    SELECT title, pages FROM books 
    WHERE pages = (SELECT Max(pages) 
                FROM books); 

                {Here we run one query inside another query, for eg: the above example first finds the book with max pages and then displays the corresponding title and pages}




* MAX OR MIN WITH GROUP BY:



    SELECT CONCAT(author_fname,' ',author_lname) AS 'author', MIN(released_year) AS 'first release'
    FROM books
    GROUP BY author_lname, author_fname;


* SUM() WITH GROUP BY


    SELECT author_fname,
       author_lname,
       Sum(pages)
    FROM books
    GROUP BY
        author_lname,
        author_fname;

    {This will display the total number of pages qritten by each author}

        OR


    SELECT CONCAT(author_fname,' ',author_lname) AS 'AUTHOR', SUM(pages)
    FROM books
    GROUP BY author_lname, author_fname
    ORDER BY SUM(pages) DESC;


    {this will display the same output but the data will be organised on the basis of number of pages in an desc order}


* To find difference or subtract:

    SELECT (COUNT(CITY)-COUNT(DISTINCT(CITY))) FROM STATION;

    {A hypothetical case where we are subtracting the number of distinct cities from total number of cities}

    



* AVG()


    SELECT released_year, AVG(pages), COUNT(*)
    FROM books
    GROUP BY released_year;



        {this will displayed the number of books published in a year and the average number of pages}




    
* DATE, TIME & DATE TIME:



    CREATE TABLE people (name VARCHAR(100), birthdate DATE, birthtime TIME, birthdt DATETIME);
 
    INSERT INTO people (name, birthdate, birthtime, birthdt)
    VALUES('Padma', '1983-11-11', '10:07:35', '1983-11-11 10:07:35');

    DATE format [YYYY-MM-DD]
    TIME format [HH:MM:SS]
    DATE TIME   [YYYY-MM-DD HH:MM:SS]


    SELECT CURDATE():  Prints the current time.
    SELECT CURTIME(): Prints the current time.
    SELECT  NOW()   : Prints the currentitme.

    SELECT DAYNAME(birthdate) FROM people; 

        {Will display the day}


    Check documentation:


    https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html


    Other types:


    DAY()      : Returns the day of the month.
    DAYOFYEAR(): Returns the day of the year.
    DAYOFWEEK(): Returns the day of the week.



* DATE_FORMAT():


    SELECT DATE_FORMAT(birthdate, '%W %M %Y') FROM people;

    {Returns the day of the year, month and date like "Wednesday December 1974"}

    Check docs for more:

    https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format
   


    SELECT DATE_FORMAT(birthdt, '%m/%d/%Y at %h:%i') FROM people;

    {This will add the timestamp too.}


* DATE MATH:


    SELECT DATEDIFF(NOW(), birthdate) FROM people;

    {Prints the number of days since birth}

    SELECT birthdt, birthdt - INTERVAL 5 MONTH FROM people;

    {+/- INTERVAL is used to add or subtract date and time}

    For more check docs:

    https://dev.mysql.com/doc/refman/8.0/en/expressions.html#temporal-intervals



* TIMESTAMP:


    CREATE TABLE comments (
    content VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW()
    );

    https://www.udemy.com/course/the-ultimate-mysql-bootcamp-go-from-sql-beginner-to-expert/learn/lecture/7019870#overview


* UPDATE A TIMESTAMP:

    CREATE TABLE comments2 (
    content VARCHAR(100),
    changed_at TIMESTAMP DEFAULT NOW() ON UPDATE NOW()
    );


    https://www.udemy.com/course/the-ultimate-mysql-bootcamp-go-from-sql-beginner-to-expert/learn/lecture/7019870#overview




* LOGICAL OPERATORS:

    1. NOT EQUAL 

        SELECT title FROM books WHERE released_year != 2017;


    2. NOT LIKE

        SELECT title FROM books WHERE title NOT LIKE 'w%';


    3. [GREATER THAN] OR [LESS THAN] OR [>= OR <=]

        SELECT title FROM books WHERE released_year > 2000;


    4. LOGICAL AND (&&):


        SELECT title FROM books WHERE author_lname = 'eggers' && released_year > 2010; 


    5. LOGICAL OR (||)


        SELECT title FROM books WHERE author_lname = 'eggers' || released_year > 2010;    


    6. BETWEEN AND NOT BETWEEN

        SELECT title, released_year FROM books WHERE released_year BETWEEN 2000 AND 2010 ORDER BY released_year;


    7. IN AND NOT IN

        SELECT title, author_lname 
        FROM books
        WHERE author_lname IN('lahiri','smith','eggers');


    8. % OPERATOR


        SELECT title, released_year FROM books
        WHERE released_year % 2 != 0;

        {will print book titles from all the odd years.}


    
CASE STATEMENTS



1. WHEN : THEN


    SELECT title, released_year,
    CASE
    WHEN released_year >= 2000 THEN 'modern lit'
    ELSE '20th century classic'
    END AS 'Genre'
    FROM books;


    --> Another use with multiple cases:


        SELECT title, stock_quantity,
        CASE
            WHEN stock_quantity < 50 THEN '*'
            WHEN stock_quantity <100 THEN '**'
            WHEN stock_quantity < 200 THEN '***'
            WHEN stock_quantity <500 THEN '****'
            ELSE '*****'
        END AS 'Stock Levels'
        FROM books
        ORDER BY stock_quantity;

    --> {Try out this case with the book shop data}

         SELECT title, author_lname,
        CASE 
        WHEN COUNT(*) = 1 THEN '1 book'
        ELSE CONCAT(COUNT(*),' books') 
         END AS TYPE
         FROM books
         GROUP BY author_lname, author_fname;


         {basically we are using the CASE statement to alter our print on the basis of the number of books}

        









# TYPE CAST:


    [Can be used when comparing two different data types for eg: date in DATETIME format and in STRING format]


    SELECT  name, birthdt 
    FROM people
    WHERE 
    birthdt BETWEEN CAST('1980-01-01' AS DATETIME)
    AND CAST('2000-01-01' AS DATETIME);





***MULTIPLE TABLES***

TYPES:

    1. ONE TO ONE.
    2. ONE TO MANY.
    3. MANY TO MANY. 


    Refer: https://www.sqlshack.com/learn-sql-types-of-relations/#:~:text=There%20are%203%20different%20types,many%2Dto%2Dmany



*** JOIN ***

[for additional reference; https://www.w3schools.com/sql/sql_join.asp]

1. INNER JOIN


    (INNER) JOIN: Returns records that have matching values in both tables.

    Implicit Join: 

    SELECT * FROM customers, orders WHERE customers.id = orders.customer_id;

    Explicit Join: {Easier Way}

    SELECT * FROM customers
    JOIN orders
    ON customers.id = orders.customer_id;



2. LEFT JOIN


    LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table.


    SELECT * FROM customers
    LEFT JOIN orders
    ON customers.id = orders.customer_id;




3. RIGHT JOIN


    RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table

    SELECT * FROM customers
    RIGHT JOIN orders
    ON customers.id = orders.customer_id;








# ISNULL


    SELECT 
    f_name, 
    l_name,
    IFNULL(SUM(amount),0) AS 'Total_purchase'

    FROM customers
    LEFT JOIN orders
    ON customers.id = orders.customer_id
    GROUP BY 2, 1
    ORDER BY amount DESC;


# ON DELETE CASCADE


    Option to specify whether you want rows deleted in a child table when corresponding rows are deleted in the parent table.


    

# ROUND


    SELECT ROUND(235.415, 2) AS RoundValue;

    The ROUND() function rounds a number to a specified number of decimal places.


# ABS VALUE


    SELECT Abs(-243.5) AS AbsNum;

    The ABS() function returns the absolute value of a number. |-1| = 1.


# FLOOR

    SELECT FLOOR(25.75) AS FloorValue;

    The FLOOR() function returns the largest integer value that is smaller than or equal to a number.

    
# CEILING()

    Rounds off to the nearest higher integer.
    
    SELECT CEILING(AVG(Salary)) 


# LOWER()


    SELECT LOWER("SQL Tutorial is FUN!");


# UNION

    SELECT column_name(s) FROM table1
    UNION
    SELECT column_name(s) FROM table2;

    {Can be used for same table as well}


# CASE Syntax


    CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
    END;




# MySQL IFNULL() Function


    IFNULL(expression, alt_value)

    e.g:

    SELECT students.first_name, papers.title, IFNULL(AVG(papers.grade),0) AS average
    FROM students
    LEFT JOIN papers ON 
    students.id = papers.student_id
    GROUP BY first_name
    ORDER BY AVG(papers.grade) DESC;

    

# JOINING THREE TABLES:


    SELECT * FROM reviewers
    INNER JOIN reviews ON 
    reviewers.id = reviews.reviewer_id
    INNER JOIN series ON
    reviews.series_id = series.id;








    
















