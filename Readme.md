**************************************************
Create a list of students showing first and last names only.
mysql> select first_name, last_name from student;
**************************************************
Create a list of students with all the columns but only if the student has less than 8 years experience
mysql> select * from student where years_of_experience < 8;
**************************************************
Create a list of students showing the lastname, startdate, and id columns only and sorted by last_name in ascending sequence
mysql> select last_name, start_date, student_id from student order by last_name;
**************************************************
Create a list of students showing all columns but only if the student first name is Adam, James, or Frank and sort them in last_name descending sequence.
mysql> select * from student where first_name = 'Adam' or first_name = 'James' or first_name = 'Frank'order by last_name DESC;
**************************************************
Create a list of students showing firstname, lastname and startdate where the startdate is between Jan 1, 2016 and June 30, 2016 and order the list by descending start_date sequence.
select first_name, last_name, start_date from student where start_date between cast('2016-01-01' as date) and cast('2016-06-30' as date);
**************************************************
Advanced Challenge

mysql> explain assignment;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> select * from assignment;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          4 |              1 |        1 |        1 |
|             2 |          6 |              1 |        1 |        2 |
|             3 |          8 |              1 |        1 |        3 |
|             4 |         10 |              1 |        1 |        4 |
|             5 |          2 |              1 |        1 |        5 |
+---------------+------------+----------------+----------+----------+
5 rows in set (0.00 sec)

mysql> explain grade
    -> ;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| grade_id | int(11)     | NO   | PRI | NULL    | auto_increment |
| grade    | varchar(30) | YES  |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> select * from grade;
+----------+-----------------------------+
| grade_id | grade                       |
+----------+-----------------------------+
|        1 | Incomplete                  |
|        2 | Complete and unsatisfactory |
|        3 | Complete and satisfactory   |
|        4 | Exceeds expectations        |
|        5 | Not graded                  |
+----------+-----------------------------+
5 rows in set (0.00 sec)

**************************************************
Pro Challenge

mysql> describe assignment
    -> ;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11) unsigned | NO   | MUL | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> describe student;
+---------------------+------------------+------+-----+---------+----------------+
| Field               | Type             | Null | Key | Default | Extra          |
+---------------------+------------------+------+-----+---------+----------------+
| student_id          | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| first_name          | varchar(30)      | YES  |     | NULL    |                |
| last_name           | varchar(30)      | YES  |     | NULL    |                |
| years_of_experience | tinyint(3)       | YES  |     | NULL    |                |
| start_date          | date             | YES  |     | NULL    |                |
+---------------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

**************************************************
Pro+ Challenge

mysql> select * from major
    -> ;
+----------+------------------------+
| major_id | major                  |
+----------+------------------------+
|        1 | Math                   |
|        2 | Science                |
|        3 | History                |
|        4 | Unraveling the mystery |
+----------+------------------------+
4 rows in set (0.00 sec)

mysql> select * from class
    -> ;
+----------+----------------+
| class_id | class          |
+----------+----------------+
|        1 | English 101    |
|        2 | English 102    |
|        3 | English 103    |
|        4 | Math 103       |
|        5 | Math 112       |
|        6 | Math 225       |
|        7 | Science 101    |
|        8 | Science 104    |
|        9 | Literature 101 |
+----------+----------------+
9 rows in set (0.00 sec)

mysql> describe class_major_relationship;
+----------+---------+------+-----+---------+----------------+
| Field    | Type    | Null | Key | Default | Extra          |
+----------+---------+------+-----+---------+----------------+
| id       | int(11) | NO   | PRI | NULL    | auto_increment |
| class_id | int(11) | NO   | MUL | NULL    |                |
| major_id | int(11) | NO   | MUL | NULL    |                |
+----------+---------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

mysql> describe class
    -> ;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| class_id | int(11)     | NO   | PRI | NULL    | auto_increment |
| class    | varchar(50) | NO   |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> describe major;
+----------+-------------+------+-----+---------+----------------+
| Field    | Type        | Null | Key | Default | Extra          |
+----------+-------------+------+-----+---------+----------------+
| major_id | int(11)     | NO   | PRI | NULL    | auto_increment |
| major    | varchar(50) | NO   |     | NULL    |                |
+----------+-------------+------+-----+---------+----------------+


****************************************
REFERENCES
****************************************

CREATE TABLE major (
    major_id INT(11) PRIMARY KEY AUTO_INCREMENT,
    major VARCHAR(50) NOT NULL,
    student_id INT
);

CREATE TABLE class (
    class_id INT(11) PRIMARY KEY AUTO_INCREMENT,
    class VARCHAR(50) NOT NULL
);
CREATE TABLE class_major_relationship (
    id INT PRIMARY KEY AUTO_INCREMENT,
    class_id INT NOT NULL,
    major_id INT NOT NULL,
    INDEX idx_class_id (class_id),
    FOREIGN KEY (class_id) REFERENCES class(class_id),
    INDEX idx_major_id (major_id),
    FOREIGN KEY (major_id) REFERENCES major(major_id)
);
