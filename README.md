lab 5: student enrollment in course
and books adopted each course
LAB 6 :ASSIGNMENT : LIBRARY

6. Consider the following database for library management system 

PUBLISHER(PName,Address,Phone)
BOOK(Book_id,Title,Publisher_Name,Pub_Year)
BOOK_AUTHORS(#Book_id,Author_Name)
LIBRARY_BRANCH(Branch_id,Branch_Name,Address)
BOOK_COPIES(#Book_id,#Branch_id,No of_Copies)
BOOK_LENDING(#Book_id,#Branch_id,Card_No,Date_Out,Due_Date) 
Create the above tables by properly specifying the primary keys and the foreign Keys Enter at least five tuples for each relation.
 Write SQL queries to
 i. Retrieve details of all books in the library  –  id, title, name of publisher, authors, number of copies in each branch, etc.
 ii. Get the particulars of borrowers who have borrowed more than 3 books, but from Jan 2017 to Jun2017
 iii. Delete a book in BOOK table. Update the contents of other tables to reflect this data manipulation operation.
 iv. Create a view of all books and its number of copies that a recurrently available in the Library.
Write PL/SQL program to demonstrate implicit cursor.
*************************************************************************
mysql> use lab6_library;
Database changed
mysql> CREATE TABLE PUBLISHER(PNAME VARCHAR(15),
    -> ADDRESS VARCHAR(25),
    -> PHONE VARCHAR(10),
    -> CONSTRAINT PK_PN PRIMARY KEY(PNAME))engine=innodb;
Query OK, 0 rows affected (0.02 sec)




mysql> CREATE TABLE BOOK(BOOK_ID INT,
    -> TITLE VARCHAR(25),
    -> PUBLISHER_NAME VARCHAR(25),
    -> PUB_YEAR INT,
    -> CONSTRAINT PK_BID PRIMARY KEY(BOOK_ID),
    -> CONSTRAINT FK_N FOREIGN KEY (PUBLISHER_NAME) REFERENCES
    -> PUBLISHER (PNAME) ON DELETE CASCADE)engine=innodb;
Query OK, 0 rows affected (0.02 sec)


mysql> CREATE TABLE BOOK_AUTHORS(BOOK_ID INT,
    -> AUTHOR_NAME VARCHAR(25),
    -> CONSTRAINT FK_B FOREIGN KEY(BOOK_ID) REFERENCES BOOK(BOOK_ID) ON DELETE CASCADE)engine=innodb;
Query OK, 0 rows affected (0.00 sec)


mysql> CREATE TABLE LIBRARY_BRANCH(BRANCH_ID INT,
    -> BRANCH_NAME VARCHAR(5),
    -> ADDRESS VARCHAR(15),
    -> CONSTRAINT PK_ID PRIMARY KEY(BRANCH_ID))engine=innodb;
Query OK, 0 rows affected (0.01 sec)


mysql> CREATE TABLE BOOK_COPIES(BOOK_ID INT,
    -> BRANCH_ID INT,
    -> NO_OF_COPIES INT,
    -> CONSTRAINT CPK_BBI PRIMARY KEY(BOOK_ID,BRANCH_ID),
    -> CONSTRAINT FK_BI FOREIGN KEY(BOOK_ID) REFERENCES BOOK(BOOK_ID) ON DELETE CASCADE,
    -> CONSTRAINT FK_I FOREIGN KEY(BRANCH_ID) REFERENCES
    -> LIBRARY_BRANCH(BRANCH_ID) ON DELETE CASCADE)engine=innodb;
Query OK, 0 rows affected (0.00 sec)







mysql> CREATE TABLE BOOK_LENDING(BOOK_ID INT,
    -> BRANCH_ID INT,
    -> CARD_NO INT,
    -> DATE_OUT DATE,
    -> DUE_DATE DATE,
    -> CONSTRAINT CPK_BBC PRIMARY KEY (BOOK_ID, BRANCH_ID, CARD_NO),
    -> CONSTRAINT FK_A FOREIGN KEY (BOOK_ID) REFERENCES BOOK(BOOK_ID) ON DELETE CASCADE,
    -> CONSTRAINT FK_C FOREIGN KEY (BRANCH_ID) REFERENCES
    -> LIBRARY_BRANCH(BRANCH_ID) ON DELETE CASCADE)engine=innodb;
Query OK, 0 rows affected (0.01 sec)


mysql> INSERT INTO PUBLISHER VALUES('PHI','PUNE,INDIA',9080700000);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('PEARSON','MUMBAI,INDIA',8080707060);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('MCGRAWHILL','HOUSTIN,USA',120707070);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('WILEY','CALIFORNIA,USA',1108080808);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('SSI','FLORIDA',1208080909);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('SP','BANGALORE,INDIA',9090909080);
Query OK, 1 row affected (0.00 sec)

SELECT * FROM PUBLISHER;

NAME		 	ADDRESS 			PHONE
--------------- ------------------------- - ---------------------------------------------
PHI 			PUNE,INDIA 			908070000
PEARSON 		MUMBAI,INDIA 		8080707060
MCGRAWHILL	 	HOUSTIN,USA 			120707070
WILEY 			CALIFORNIA,USA 		1108080808
SSI	        		FLORIDA			1208080909
SP 			BANGALORE,INDIA 		9090909080
--------------------------------------------------------------------------------------------------------
mysql> INSERT INTO PUBLISHER VALUES('PHI','PUNE,INDIA',9080700000);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('PEARSON','MUMBAI,INDIA',8080707060);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('MCGRAWHILL','HOUSTIN,USA',120707070);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('WILEY','CALIFORNIA,USA',1108080808);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('SSI','FLORIDA',1208080909);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO PUBLISHER VALUES('SP','BANGALORE,INDIA',9090909080);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(1111,'FUNNDAMENTALS OF DATABASE','PHI',2009);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(2222,'BASICS OF LOGIC DESIGN','PEARSON',2009);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(3333,'DATASTRUCTURES','MCGRAWHILL',2015);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(4444,'ARTIFICIAL INTELLIGENCE','WILEY',2017);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(5555,'PROGRAMMING SKILLS','SSI',2014);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(6666,'DESIGN OF ALGORITHMS','SP',2013);
Query OK, 1 row affected (0.00 sec)

SELECT * FROM BOOK;
BOOK_ID   	  TITLE	  	  			PUBLISHER_NAME		PUB_YEAR
---------- ------------------------- -------------------------------------------------------------------------------------
1111 		FUNNDAMENTALS OF DATABASE 	PHI 				2009
2222 		BASICS OF LOGIC DESIGN 		PEARSON 			2009
3333	 	DATASTRUCTURES		        	MCGRAWHILL 			2015
4444	 	ARTIFICIAL INTELLIGENCE 		WILEY	              		  2017
5555 		PROGRAMMING SKILLS	        	SSI 				2014 
6666 		DESIGN OF ALGORITHMS 		SP 				2013

---------------------------------------------------------------------------------------------
mysql> INSERT INTO BOOK VALUES(1111,'FUNNDAMENTALS OF DATABASE','PHI',2009);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(2222,'BASICS OF LOGIC DESIGN','PEARSON',2009);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(3333,'DATASTRUCTURES','MCGRAWHILL',2015);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(4444,'ARTIFICIAL INTELLIGENCE','WILEY',2017);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(5555,'PROGRAMMING SKILLS','SSI',2014);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK VALUES(6666,'DESIGN OF ALGORITHMS','SP',2013);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(1111,'NAVATHE');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(2222,'GODSE');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(3333,'SAHANI');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(4444,'RITCHIE KNIGHT');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(5555,'BALAGURUSWAMY');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_AUTHORS VALUES(6666,'COREMEN');
Query OK, 1 row affected (0.01 sec)

SELECT * FROM BOOK_AUTHORS;

BOOK_ID 	AUTHOR_NAME
---------- -------------------------
1111 		NAVATHE
2222 		GODSE
3333 		SAHANI
4444 		RITCHIE KNIGHT
5555	        BALAGURUSWAMY
6666 		COREMEN


---------------------------------------------------------------------------------------

mysql> INSERT INTO LIBRARY_BRANCH VALUES(1000,'SMVIT','H.MARANAHALLI');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO LIBRARY_BRANCH VALUES(2000,'SVIT','DODDABALLAPUR');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO LIBRARY_BRANCH VALUES(3000,'BMSIT','AVANAHALLI');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO LIBRARY_BRANCH VALUES(4000,'SVCE','VIDYANAGAR');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO LIBRARY_BRANCH VALUES(5000,'MSCE','CHIKKAJALA');
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO LIBRARY_BRANCH VALUES(6000,'NMIT','YELAHANKA');
Query OK, 1 row affected (0.00 sec)




SELECT * FROM LIBRARY_BRANCH;

BRANCH_ID 	BRANCH_NAME 	ADDRESS
---------- ----- ---------------------------------------------
1000 		SMVIT 		H.MARANAHALLI
2000 		SVIT 		DODDABALLAPUR
3000 		BMSIT 		AVANAHALLI
4000 		SVCE 		VIDYANAGAR
5000 		MSCE 		CHIKKAJALA
6000 		NMIT 		YELAHANKA

--------------------------------------------------------------------------------
mysql> INSERT INTO BOOK_COPIES VALUES(1111,1000,10);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(2222,2000,5);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(3333,3000,7);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(4444,4000,9);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(5555,5000,6);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(6666,6000,12);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO BOOK_COPIES VALUES(2222,1000,15);
Query OK, 1 row affected (0.00 sec)

SELECT * FROM BOOK_COPIES;

BOOK_ID 	BRANCH_ID 	NO_OF_COPIES
---------- ---------- ----------------------
1111 		1000 		10
2222 		2000 		5
3333 		3000 		7
4444 		4000		9
5555 		5000 		6
6666	              6000 		12
2222 		1000 		15


---------------------------------------------------------------------------
mysql> INSERT INTO BOOK_LENDING VALUES(1111,1000,10,'2017-02-15','2017-06-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(2222,2000,10,'2017-03-10','2017-08-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(3333,3000,10,'2017-04-15','2017-09-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(4444,4000,10,'2017-06-10','2017-11-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(5555,5000,20,'2017-02-15','2017-06-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(6666,6000,30,'2017-03-10','2017-08-15');
Query OK, 1 row affected (0.00 sec)

mysql>  INSERT INTO BOOK_LENDING VALUES(5555,5000,10,'2016-01-15','2016-06-15');
Query OK, 1 row affected (0.00 sec)

select * from book_lending;

BOOK_ID, 	BRANCH_ID,      CARD_NO, 	DATE_OUT, 	DUE_DATE
1111, 		1000, 		  10, 		2017-02-15,     2017-06-15
2222, 		2000, 		  10, 		2017-03-10,     2017-08-15
3333, 		3000, 		  10,		 2017-04-15,     2017-09-15
4444, 		4000,		10, 		2017-06-10,      2017-11-15
5555,		 5000, 		10, 		2016-01-15,      2016-06-15
5555,		 5000, 		20, 		2017-02-15,      2017-06-15
6666,		 6000, 		30, 		2017-03-10,     2017-08-15


---------------------------------------------------------------------------------
1] Retrieve details of all books in the library i.e ID, Title, name of publisher, authors, number  of copies etc in each branch etc.

 Solution 1:-
SELECT
B.Book_id, B.Title, B.Publisher_Name,
BA.Author_Name, BC.Branch_id, BC.No_of_Copies
FROM
BOOK B
JOIN
BOOK_AUTHORS BA ON B.Book_id = BA.Book_id
JOIN
BOOK_COPIES BC ON B.Book_id = BC.Book_id
join 
LIBRARY_BRANCH L  on L.BRANCH_ID=BC.BRANCH_ID ;

 or


solution2: 
mysql> SELECT C.BRANCH_ID,
        L.BRANCH_NAME,
          B.BOOK_ID,
             B.TITLE,
            B.PUBLISHER_NAME,
         A.AUTHOR_NAME,
       C.NO_OF_COPIES
    FROM BOOK B,BOOK_AUTHORS A,LIBRARY_BRANCH L,BOOK_COPIES C
     WHERE B.BOOK_ID=A.BOOK_ID AND
     B.BOOK_ID=C.BOOK_ID AND
     L.BRANCH_ID=C.BRANCH_ID AND
     (C.BRANCH_ID,C.BOOK_ID) IN
     (SELECT BRANCH_ID,BOOK_ID
     FROM BOOK_COPIES
     GROUP BY BRANCH_ID,BOOK_ID);
+-----------+-------------+---------+---------------------------+----------------+----------------+--------------+--------------------------------------------------------------
| BRANCH_ID | BRANCH_NAME | BOOK_ID | TITLE                    	 | PUBLISHER_NAME | AUTHOR_NAME    | NO_OF_COPIES |
+-----------+-------------+---------+---------------------------+----------------+----------------+--------------+---------------------------------------------------------------
|      1000 | SMVIT       |    1111 | FUNNDAMENTALS OF DATABASE 	| PHI           	 | NAVATHE        		|           10 	|
|      1000 | SMVIT       |    2222 | BASICS OF LOGIC DESIGN   	 | PEARSON        	| GODSE         		 |           15 	|
|      2000 | SVIT        |    2222 | BASICS OF LOGIC DESIGN   		 | PEARSON        	| GODSE         		 |            5 	|
|      3000 | BMSIT       |    3333 | DATASTRUCTURES            		| MCGRAWHILL   	  | SAHANI        		 |            7 	|
|      4000 | SVCE        |    4444 | ARTIFICIAL INTELLIGENCE 		  | WILEY          	| RITCHIE KNIGHT 		|            9		 |
|      5000 | MSCE        |    5555 | PROGRAMMING SKILLS     	  	 | SSI            	| BALAGURUSWAMY 	 |            6 	|
|      6000 | NMIT        |    6666 | DESIGN OF ALGORITHMS      	| SP             	| COREMEN       		 |           12	 |
+-----------+-------------+---------+---------------------------+----------------+----------------+--------------+----------------------------------------------------------------
7 rows in set (0.00 sec)
-------------------------------------------------------------------------------------------------------------------------
2] Get the particulars of borrowers who have borrowed more than 3 books but from Jan 2017 to Jun  2017

SOLUTION:=

    
 SOLUTION:=

 mysql> SELECT bl.card_no, COUNT(distinct bl.book_id) AS total_books
    -> FROM book_lending bl WHERE date_out  BETWEEN '2017-01-01' AND '2017-06-30'
    -> GROUP BY bl.card_no HAVING COUNT(book_id) > 3;
+---------+-------------+-----------
| card_no | total_books       |
+---------+-------------+-----------
|      10          |           4             |
+---------+-------------+-----------
1 row in set (0.02 sec)

------------------------------------------------------------------------------------------------------------------
3] Delete a book in book table.Update the contents of other tables to reflect this data manipulation operation.

SOLUTION:= 

DELETE FROM BOOK WHERE BOOK_ID=5555;

 Note: IN BELOW TABLES OUTPUT, BOOK_ID=5555  HAS  BEEN DELETED  INALL TE TABLES WHERE BOOK_ID=5555 IS THERE , BUT IF YOU OBSERVE THE ORIGINAL TABLES BEFORE DELETE OPERATION WE HAVE BOOK_ID=5555 DETAILS . In the below tables we have book_id , so we need to check in these tables

BOOK(Book_id,  Title,Publisher_Name,Pub_Year)
BOOK_AUTHORS(#Book_id,  Author_Name)
BOOK_COPIES(#Book_id,  #Branch_id,No of_Copies)
BOOK_LENDING(#Book_id,  #Branch_id,Card_No,Date_Out,Due_Date) 

AFTER ABOVE DELETE OPERATION:

mysql> select * from book;
+---------+---------------------------+----------------+----------+-----------------------------------------
| BOOK_ID | TITLE                   			  | PUBLISHER_NAME 	| PUB_YEAR |
+---------+---------------------------+----------------+----------+------------------------------------------
|    1111 | FUNNDAMENTALS OF DATABASE 	| PHI           		 |     2009 |
|    2222 | BASICS OF LOGIC DESIGN   		 | PEARSON       	 |     2009 |
|    3333 | DATASTRUCTURES            		| MCGRAWHILL     	|     2015 |
|    4444 | ARTIFICIAL INTELLIGENCE   		| WILEY          		|     2017 |
|    6666 | DESIGN OF ALGORITHMS     		 | SP             		|     2013 |
+---------+---------------------------+----------------+----------+------------------------------------------
5 rows in set (0.00 sec)

mysql> select * from book_authors;
+---------+----------------+------------
| BOOK_ID | AUTHOR_NAME    |
+---------+----------------+---------------
|    1111 	| NAVATHE        	|
|    2222 	| GODSE         	 	|
|    3333 	| SAHANI         		|
|    4444 	| RITCHIE KNIGHT 	|
|    6666 	| COREMEN      	  |
+---------+----------------+---------------
5 rows in set (0.00 sec)

mysql> select * from book_copies;
+---------+-----------+--------------+
| BOOK_ID | BRANCH_ID | NO_OF_COPIES |
+---------+-----------+--------------+------------------
|    1111 |      1000 	|           10 	|
|    2222 |      1000		 |           15 	|
|    2222 |      2000 	|            5 	|
|    3333 |      3000 	|            7 	|
|    4444 |      4000 	|            9 	|
|    6666 |      6000 	|           12 	|
+---------+-----------+--------------+--------------
6 rows in set (0.00 sec)

mysql> select * from book_lending;
+---------+-----------+---------+------------+------------+------------------------
| BOOK_ID | BRANCH_ID | CARD_NO | DATE_OUT   | DUE_DATE   |
+---------+-----------+---------+------------+------------+----------------------------
|    1111 |      1000 	|      10 	| 2017-02-15 | 2017-06-15 |
|    2222 |      2000 	|      10 	| 2017-03-10 | 2017-08-15 |
|    3333 |      3000 	|      10 	| 2017-04-15 | 2017-09-15 |
|    4444 |      4000 	|      10 	| 2017-06-10 | 2017-11-15 |
|    6666 |      6000 	|      30 	| 2017-03-10 | 2017-08-15 |
+---------+-----------+---------+------------+------------+----------------------------------
5 rows in set (0.00 sec)


-------------------------------------------------------------------------------------------------------------------------------------
4].Create a view all books and its no. of copies that are currently available in the library

SOLUTION:=

mysql> CREATE  VIEW  CURRENT_BOOKS  AS SELECT  B.BOOK_ID,
    -> B.TITLE, C.NO_OF_COPIES, L.BRANCH_NAME FROM  BOOK  B,BOOK_COPIES  C,LIBRARY_BRANCH  L
    -> WHERE  B.BOOK_ID=C.BOOK_ID
    -> AND L.BRANCH_ID=C.BRANCH_ID;
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT * FROM CURRENT_BOOKS;
+---------+---------------------------+--------------+-------------+----------------------------------------------
| BOOK_ID | TITLE                 			    | NO_OF_COPIES | BRANCH_NAME |
+---------+---------------------------+--------------+-------------+----------------------------------------------------
|    1111 | FUNNDAMENTALS OF DATABASE	 |           10 		| SMVIT       |
|    2222 | BASICS OF LOGIC DESIGN    		|           15 		| SMVIT       |
|    2222 | BASICS OF LOGIC DESIGN   		 |            5 		| SVIT        |
|    3333 | DATASTRUCTURES          		  |            7 		| BMSIT       |
|    4444 | ARTIFICIAL INTELLIGENCE  		 |            9 		| SVCE        |
|    6666 | DESIGN OF ALGORITHMS     		 |           12 		| NMIT        |
+---------+---------------------------+--------------+-------------+-------------------------------------------------
6 rows in set (0.00 sec)

----------------------------------------------------------------------------------------------------------------------

Write PL/SQL program to demonstrate implicit cursor.

*******************************************************************************

SELECT * FROM BOOK;
BOOK_ID   	  TITLE	  	  			PUBLISHER_NAME		PUB_YEAR
---------- ------------------------- -------------------------------------------------------------------------------------
1111 		FUNNDAMENTALS OF DATABASE 	PHI 				2009
2222 		BASICS OF LOGIC DESIGN 		PEARSON 			2009
3333	 	DATASTRUCTURES		        	MCGRAWHILL 			2015
4444	 	ARTIFICIAL INTELLIGENCE 		WILEY	              		  2017
5555 		PROGRAMMING SKILLS	        	SSI 				2014 
6666 		DESIGN OF ALGORITHMS 		SP 				2013

example for implicit cursors[ for lab journal]

mysql> delimiter //
mysql> CREATE PROCEDURE  get_book_details()
    -> BEGIN
    -> DECLARE  title11  VARCHAR(25);
    -> DECLARE  publisher_name11  varchar(25);
    -> SELECT  title, publisher_name  INTO   title11 , publisher_name11  FROM book where book_id=1111;
    ->     SELECT  title11 , publisher_name11 ;
    -> end//
Query OK, 0 rows affected (0.02 sec)

mysql> delimiter ;
mysql> call get_book_details();
+---------------------------+------------------+--------------------------
| title11                                                   | publisher_name11 |
+---------------------------+------------------+---------------------------
| FUNNDAMENTALS OF DATABASE     | PHI                       |
+---------------------------+------------------+---------------------------
