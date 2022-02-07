# **Reference manual for LessSQL client**

## **LOGGING INTO THE SERVER**

### **Credential entering screen**

    USER-NAME: <Default user-name is 'root'; Enter your user-name>
    PASSWORD: <Password's input will be hidden>
    HOST-NAME: <Default host is 'localhost'; Enter the ip-address of the server>

*Note! The root's ("root is the default username and root is also the default server administrator") password is the password entered while configuring/installing the MySQL server and other users will have passwords assigned to them by their server administrator.*

#### **Example**

    USER-NAME: root
    PASSWORD: 
    HOST-NAME: localhost

</br>

### **Main screen**

    LOGGED IN AS: root@localhost
    TIME: 21:48:59 PM

    MySQL server version: 8.0.27
    Connection ID: 8

    +------------------------------------------------------------+
    | Welcome to LessSQL Database Management Client              |
    | Version: 5.7.2                                             |
    |                                                            |
    | Copyright (c) 2021 Shahibur Rahaman                        |
    |                                                            |
    | This program comes with ABSOLUTELY NO WARRANTY.            |
    |                                                            |
    | For more info and updates visit:                           |
    | https://github.com/Shahibur50/LessSQL                      |
    |                                                            |
    | Commands end with ;                                        |
    |                                                            |
    | To cancel any input statement type '\c'                    |
    |                                                            |
    | Type "license;" to see the license.                        |
    | Type 'help;' or '\h;' for help. To exit type 'exit;'       |
    +------------------------------------------------------------+

    LessSQL|>

</br>

---

## **COMMANDS FOR DATABASE MANIPULATION**

- ### **show databases;**

        LessSQL|> show databases;
        +--------------------+
        | Database           |
        +--------------------+
        | information_schema |
        | mysql              |
        | performance_schema |
        | sakila             |
        | sys                |
        | world              |
        +--------------------+
        Database(s) count: 6

</br>

- ### **create database;**

        LessSQL|> create database;
            -> DATABASE NAME: student_marks  

        Query OK, created database [student_marks]

</br>

- ### **use database;**

        LessSQL|> use database;
               -> DATABASE NAME: student_marks

        Query OK, now using database [student_marks]

</br>

- ### **delete database;**

        LessSQL|> delete database;
               -> DATABASE NAME: student_marks

        IRREVERSIBLE CHANGE! Do you really want to delete the database [student_marks]? (y/[n]) y

        Query OK, deleted database [student_marks]

</br>

---

## **COMMANDS FOR TABLE MANIPULATION**

- ### **create table;**

        LessSQL|> create table;
               -> NAME OF TABLE: UT_I  
               -> NO. OF COLUMNS: 5
               -> COLUMN (1) NAME AND DATA-TYPE: Roll_No INT
               -> COLUMN (2) NAME AND DATA-TYPE: Name VARCHAR(30)
               -> COLUMN (3) NAME AND DATA-TYPE: Class VARCHAR(5)
               -> COLUMN (4) NAME AND DATA-TYPE: Section CHAR(1)
               -> COLUMN (5) NAME AND DATA-TYPE: Marks FLOAT(3, 2)
               -> PRIMARY KEY: Roll_No

        Query OK, created table [UT_I]

</br>

- ### **show tables;**

        LessSQL|> show tables;
        +-------------------------+
        | Tables_in_student_marks |
        +-------------------------+
        | ut_i                    |
        +-------------------------+
        Table(s) count: 1

</br>

- ### **describe table;**

        LessSQL|> describe table;
               -> TABLE NAME: ut_i
        +---------+----------------+------+-----+---------+-------+
        | Field   | Type           | Null | Key | Default | Extra |
        +---------+----------------+------+-----+---------+-------+
        | Roll_No | b'int'         | NO   | PRI | None    |       |
        | Name    | b'varchar(30)' | YES  |     | None    |       |
        | Class   | b'varchar(5)'  | YES  |     | None    |       |
        | Section | b'char(1)'     | YES  |     | None    |       |
        | Marks   | b'float(3,2)'  | YES  |     | None    |       |
        +---------+----------------+------+-----+---------+-------+
        Column(s) count: 5

</br>

- ### **delete table;**

        LessSQL|> delete table;
               -> TABLE NAME: old_students_table

        IRREVERSIBLE CHANGE! Do you really want to delete the table [old_students_table]? (y/[n]) y

        Query OK, deleted the table [old_students_table]

</br>

---

## **COMMANDS FOR COLUMN MANIPULATION**

- ### **add column;**

        LessSQL|> add column;
               -> TABLE NAME: ut_i
               -> COLUMN NAME AND DATA-TYPE: Maximum_Marks FLOAT(3, 2)

        Query OK, added column [Maximum_Marks] with data-type [FLOAT(3, 2)] to the table [ut_i]

</br>

- ### **modify column;**

        LessSQL|> modify column;
                -> TABLE NAME: ut_i
                -> COLUMN NAME AND DATA-TYPE: Name VARCHAR(35)

        Query OK, modified column [Name] to new data-type [VARCHAR(35)] in table [ut_i]

</br>

- ### **delete column;**
  
        LessSQL|> delete column;
                -> TABLE NAME: ut_i
                -> NAME OF COLUMN TO BE DELETED: old_address

        IRREVERSIBLE CHANGE! Do you really want to delete the column [old_address]? (y/[n]) y

        Query OK, Deleted column [old_address] from table [ut_i]

</br>

---

## **COMMANDS FOR IN-TABLE QUERIES**

- ### **reveal;**

        LessSQL|> reveal;
               -> TABLE NAME: ut_i
               -> COLUMN NAME(S): all
        +---------+---------+-------+---------+--------+---------------+
        | Roll_No | Name    | Class | Section | Marks  | Maximum_Marks |
        +---------+---------+-------+---------+--------+---------------+
        | 1       | Ajay    | XII   | D       | 452.75 | None          |
        | 2       | Ashish  | XII   | E       | 423.21 | None          |
        | 3       | Suraj   | XII   | C       | 434.32 | None          |
        | 4       | Vedant  | XII   | E       | 412.36 | None          |
        | 5       | Bhaskar | XII   | E       | 441.53 | None          |
        +---------+---------+-------+---------+--------+---------------+
        Row(s) count: 5

</br>

- ### **distict reveal;**

        LessSQL|> distinct reveal; 
               -> TABLE NAME: ut_i
               -> COLUMN NAME(S): Section
        +---------+
        | Section |
        +---------+
        | D       |
        | E       |
        | C       |
        +---------+
        Row(s) count: 3

</br>

- ### **search;**

        LessSQL|> search;
               -> TABLE NAME: ut_i
               -> COLUMN NAMES: Name, Marks, Section
               -> CONDITION: Marks > 450
        +------+--------+---------+
        | Name | Marks  | Section |
        +------+--------+---------+
        | Ajay | 452.75 | D       |
        +------+--------+---------+
        Row(s) count: 1

</br>

- ### **distinct search;**

        LessSQL|> distinct search; 
               -> TABLE NAME: ut_i
               -> COLUMN NAMES: Section
               -> CONDITION: Marks > 420 and Marks < 450
        +---------+
        | Section |
        +---------+
        | E       |
        | C       |
        +---------+
        Row(s) count: 2

</br>

---

## **COMMANDS FOR IN-TABLE MANIPULATION**

- ### **insert;**
  
        LessSQL|> insert;
               -> TABLE NAME: ut_i
               -> COLUMN NAMES: Roll_No, Name, Class, Section, Marks
               -> VALUES: 6, 'Ram', 'XII', 'A', 407.56 

        Query OK, values inserted successfully

        Affected row(s): 1

</br>

- ### **update;**

        LessSQL|> update;
               -> TABLE NAME: ut_i
               -> CONDITION: Maximum_Marks is NULL
               -> COLUMN TO BE UPDATED: Maximum_Marks
               -> UPDATED VALUE OF DATA-ITEM: 500.00

        Query OK, updated the data-items(s) in column/field [Maximum_Marks] to [500.00] where condition [Maximum_Marks is NULL] was satisfied.

        Affected row(s): 6

</br>

- ### **delete;**

        LessSQL|> delete;
               -> TABLE NAME: ut_i
               -> CONDITION: Name = 'Ram'

        Query OK, deleted the row(s) where condition [Name = 'Ram'] was satisfied

        Affected row(s): 1

</br>

---

## **COMMANDS FOR SPECIAL OPERATIONS**

- ### **group insert;**

        LessSQL|> group insert;
               -> TABLE NAME: ut_i
               -> NO. OF ROWS: 5
               -> COLUMN NAMES: Roll_No, Name, Class, Section, Marks
                             -> 1, 'Ajay', 'XII', 'D', 452.75
                             -> 2, 'Ashish', 'XII', 'E', 423.21
                             -> 3, 'Suraj', 'XII', 'C', 434.32
                             -> 4, 'Vedant', 'XII', 'E', 412.36
                             -> 5, 'Bhaskar', 'XII', 'E', 441.53
     
        Query OK, inserted the given value(s) in column(s) [Roll_No, Name, Class, Section, Marks] in table [ut_i]

        Affected row(s): 5

</br>

- ### **average;**

        LessSQL|> average;
               -> TABLE NAME: ut_i
               -> COLUMN NAME: Marks
               -> TITLE: Average Marks
        +---------------+
        | Average Marks |
        +---------------+
        | 432.83        |
        +---------------+

</br>

- ### **count;**

        LessSQL|> count;
               -> TABLE NAME: ut_i
               -> COLUMN NAME: Roll_No
               -> TITLE: Total Number of Students
        +--------------------------+
        | Total Number of Students |
        +--------------------------+
        | 5                        |
        +--------------------------+

</br>

- ### **max;**
  
        LessSQL|> max;
               -> TABLE NAME: ut_i
               -> COLUMN NAME: Marks
               -> TITLE: Maximum Marks Achived By Students
        +-----------------------------------+
        | Maximum Marks Achieved By Students |
        +-----------------------------------+
        | 452.75                            |
        +-----------------------------------+

</br>

- ### **min;**

        LessSQL|> min;
               -> TABLE NAME: UT_I
               -> COLUMN NAME: Marks
               -> TITLE: Minimum Marks Achieved By Students
        +------------------------------------+
        | Minimum Marks Achieved By Students |
        +------------------------------------+
        | 412.36                             |
        +------------------------------------+

</br>

- ### **sum;**

        LessSQL|> sum;
               -> TABLE NAME: UT_I
               -> COLUMN NAME: Marks
               -> TITLE: Total Marks Achived By All Students Combined
        +----------------------------------------------+
        | Total Marks Achived By All Students Combined |
        +----------------------------------------------+
        | 2164.17                                      |
        +----------------------------------------------+

</br>

## **ADVANCE MODE FOR DIRECT MySQL QUERY EXECUTION**

- ### **advance mode;**
  
        LessSQL|> advance mode;

        NOTE! Current Database: [student_marks]

        mysql> show databases;
        +--------------------+
        | Database           |
        +--------------------+
        | information_schema |
        | mysql              |
        | performance_schema |
        | sakila             |
        | student_marks      |
        | sys                |
        | world              |
        +--------------------+
        7 rows in set

        mysql> show tables;
        +-------------------------+
        | Tables_in_student_marks |
        +-------------------------+
        | ut_i                    |
        +-------------------------+
        1 rows in set

        mysql> SELECT * FROM UT_I WHERE Marks > 430;
        +---------+---------+-------+---------+--------+---------------+
        | Roll_No | Name    | Class | Section | Marks  | Maximum_Marks |
        +---------+---------+-------+---------+--------+---------------+
        | 1       | Ajay    | XII   | D       | 452.75 | 500.0         |
        | 3       | Suraj   | XII   | C       | 434.32 | 500.0         |
        | 5       | Bhaskar | XII   | E       | 441.53 | 500.0         |
        +---------+---------+-------+---------+--------+---------------+
        3 rows in set

</br>

- ### **exit advance mode;**

        mysql> exit advance mode;

        NOTE! Current Database: [student_marks]

        LessSQL|>
