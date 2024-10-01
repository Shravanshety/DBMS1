# DBMS1
mysql> use Insurance;
Database changed
mysql> create table person(driver_id varchar(10),name varchar(20),address varchar(30),primary key(driv
er_id));
Query OK, 0 rows affected (0.02 sec)

mysql> desc person;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| driver_id | varchar(10) | NO   | PRI | NULL    |       |
| name      | varchar(20) | YES  |     | NULL    |       |
| address   | varchar(30) | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> create table car(reg_num varchar(10),model varchar(10),year int,primary key(reg_num));
Query OK, 0 rows affected (0.02 sec)

mysql> show tables;
+---------------------+
| Tables_in_insurance |
+---------------------+
| car                 |
| person              |
+---------------------+
2 rows in set (0.00 sec)

mysql> create table accident(report_num int,accident_date date,location varchar(20),primary key(driver_name,reg_no));
ERROR 1072 (42000): Key column 'driver_name' doesn't exist in table
mysql> create table accident(report_num int,accident_date date,location varchar(20),primary key(reg_no
));
ERROR 1072 (42000): Key column 'reg_no' doesn't exist in table
mysql> create table accident(report_num int,accident_date date,location varchar(20),primary key(report_num));
Query OK, 0 rows affected (0.02 sec)

mysql> desc accident;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| report_num    | int         | NO   | PRI | NULL    |       |
| accident_date | date        | YES  |     | NULL    |       |
| location      | varchar(20) | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> create table owns(driver_id varchar(10),reg_num varchar(10),primary key(driver_id,reg_num),foreign key(driver_id) references person(driver_id),foriegn key(reg_num) references car(reg_num));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'key(reg_num) references car(reg_num))' at line 1
mysql> create table owns(driver_id varchar(10),reg_num varchar(10),primary key(driver_id,reg_num),foreign key(driver_id) references person(driver_id),foreign key(reg_num) references car(reg_num));
Query OK, 0 rows affected (0.03 sec)

mysql> show tables;
+---------------------+
| Tables_in_insurance |
+---------------------+
| accident            |
| car                 |
| owns                |
| person              |
+---------------------+
4 rows in set (0.00 sec)

mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    -> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report_num),
    -> foriegn key(driver_id) references person(driver_id),
    -> foriegn key(reg_num) references car(reg_num),
    -> foriegn key(report_num) references accident(report_num));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'key(driver_id) references person(driver_id),
foriegn key(reg_num) references car' at line 4
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     -> report_num int,damage_amount int,
    ->     -> primary key(driver_id,reg_num,report_num),
    ->     -> foriegn key(driver_id) references person(driver_id),
    ->     -> foriegn key(reg_num) references car(reg_num),
    -> foreign key(report_num) references accident(report_num));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report' at line 2
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     -> report_num int,damage_amount int,
    ->     -> primary key(driver_id,reg_num,report_num),
    ->     -> foriegn key(driver_id) references person(driver_id),
    ->     -> foriegn key(reg_num) references car(reg_num),
    ->     -> foriegn key(reg_num) references car(reg_num),
    ->
    ->
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report' at line 2
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     -> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report_num),
    -> create table owns(driver_id varchar(10),reg_num varchar(10),primary key(driver_id,reg_num),foreign key(driver_id) references person(driver_id),foriegn key(reg_num) references car(reg_num));create table participated(driver_id varchar(10),reg_num varchar(10),
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> report_num int,damage_amount int,
primary key(driver_id,reg_num,report_num),
' at line 2
    ->     -> report_num int,damage_amount int,
    ->     -> primary key(driver_id,reg_num,report_num),
    ->     -> foriegn key(driver_id) references person(driver_id),
    ->     -> foriegn key(reg_num) references car(reg_num),
    -> create table owns(driver_id varchar(10),reg_num varchar(10),primary key(driver_id,reg_num),foreign key(driver_id) references person(driver_id),foriegn key(reg_num) references car(reg_num));create table participated(driver_id varchar(10),reg_num varchar(10),
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report' at line 2
    ->
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 1
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     -> report_num int,damage_amount int,
    ->     -> primary key(driver_id,reg_num,report_num),
    ->     -> foriegn key(driver_id) references person(driver_id),
    ->     -> foriegn key(reg_num) references car(reg_num),
    ->     -> foreign key(report_num) references accident(report_num));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-> report_num int,damage_amount int,
    -> primary key(driver_id,reg_num,report' at line 2
mysql>  create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     ->     -> report_num int,damage_amount int,
    ->     ->     -> primary key(driver_id,reg_num,report_num),
    ->     ->     -> foriegn key(driver_id) references person(driver_id),
    ->     ->     -> foriegn key(reg_num) references car(reg_num),
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '->     -> report_num int,damage_amount int,
    ->     -> primary key(driver_id,' at line 2
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    ->     ->     ->     -> report_num int,damage_amount int,
    ->     ->     ->     -> primary key(driver_id,reg_num,report_num),
    -> fo;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '->     ->     -> report_num int,damage_amount int,
    ->     ->     -> primary ' at line 2
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),
    -> reprt_num int,damage_amount int,
    -> reprt_num int,damage_amount int,;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 3
mysql> create table participated(driver_id varchar(10).reg_num varchar(10),report_num int,damage_amoun
t int,primary key(driver_id,reg_num,report_num),foreign key(driver_id)references person(driver_id),for
eign key(reg_num) references car(reg_num),
    -> foreign key(report_num) references accident(report_num));
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.reg_num varchar(10),report_num int,damage_amount int,primary key(driver_id,reg_' at line 1
mysql> create table participated(driver_id varchar(10),reg_num varchar(10),report_num int,damage_amount int,primary key(driver_id,reg_num,report_num),foreign key(driver_id)references person(driver_id),foreign key(reg_num) references car(reg_num),
    -> foreign key(report_num) references accident(report_num));
Query OK, 0 rows affected (0.03 sec)

mysql> show tables;
+---------------------+
| Tables_in_insurance |
+---------------------+
| accident            |
| car                 |
| owns                |
| participated        |
| person              |
+---------------------+
5 rows in set (0.00 sec)

mysql> insert into person values("A01","Richard","srinivas nagar");
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values("A02","pradeep","rajaji nagar");
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values("A03","smith","ashok nagar");
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values("A04","venu","N R Colony");
Query OK, 1 row affected (0.00 sec)

mysql> insert into person values("A05","jhon","Hanumanth nagar");
Query OK, 1 row affected (0.00 sec)

mysql> select * from person;
+-----------+---------+-----------------+
| driver_id | name    | address         |
+-----------+---------+-----------------+
| A01       | Richard | srinivas nagar  |
| A02       | pradeep | rajaji nagar    |
| A03       | smith   | ashok nagar     |
| A04       | venu    | N R Colony      |
| A05       | jhon    | Hanumanth nagar |
+-----------+---------+-----------------+
5 rows in set (0.00 sec)

mysql> insert into car values("KA052250","Indica",1990);
Query OK, 1 row affected (0.00 sec)

mysql> commit;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into car values("KA031181","Lancer",1957);
Query OK, 1 row affected (0.00 sec)

mysql> insert into car values("KA095477","Toyota",1998);
Query OK, 1 row affected (0.00 sec)

mysql> insert into car values("KA053408","Honda",2008);
Query OK, 1 row affected (0.00 sec)

mysql> insert into car values("KA041702","Audi",2005);
Query OK, 1 row affected (0.00 sec)

mysql> select * from car;
+----------+--------+------+
| reg_num  | model  | year |
+----------+--------+------+
| KA031181 | Lancer | 1957 |
| KA041702 | Audi   | 2005 |
| KA052250 | Indica | 1990 |
| KA053408 | Honda  | 2008 |
| KA095477 | Toyota | 1998 |
+----------+--------+------+
5 rows in set (0.00 sec)

mysql> insert into owns values("A01","KA052250");
Query OK, 1 row affected (0.00 sec)

mysql> insert into owns values("A02","KA053408");
Query OK, 1 row affected (0.00 sec)

mysql> insert into owns values("A03","KA031181");
Query OK, 1 row affected (0.00 sec)

mysql> insert into owns values("A04","KA095477");
Query OK, 1 row affected (0.00 sec)

mysql> insert into owns values("A05","K041702");
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`owns`, CONSTRAINT `owns_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> insert into owns values("A05","K041702");
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`owns`, CONSTRAINT `owns_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> SELECT * FROM OWNS;
+-----------+----------+
| driver_id | reg_num  |
+-----------+----------+
| A03       | KA031181 |
| A01       | KA052250 |
| A02       | KA053408 |
| A04       | KA095477 |
+-----------+----------+
4 rows in set (0.00 sec)

mysql> insert into participate values("A01","K052250",11,10000);
ERROR 1146 (42S02): Table 'insurance.participate' doesn't exist
mysql> insert into participated values("A01","K052250",11,10000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`participated`, CONSTRAINT `participated_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> select * from participated;
Empty set (0.00 sec)

mysql> select * from participate;
ERROR 1146 (42S02): Table 'insurance.participate' doesn't exist
mysql> insert into participated values("A01","K052250",11,10000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`participated`, CONSTRAINT `participated_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> update table name participated to participate;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'table name participated to participate' at line 1
mysql>  create table participated(driver_id varchar(10),reg_num varchar(10),report_num int,damage_amount int,primary key(driver_id,reg_num,report_num),foreign key(driver_id)references person(driver_id),foreign key(reg_num) references car(reg_num),
    -> insert into car values("KA053408","Honda",2008);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'insert into car values("KA053408","Honda",2008)' at line 2
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql>
mysql> desc partipated;
ERROR 1146 (42S02): Table 'insurance.partipated' doesn't exist
mysql> desc participated;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| driver_id     | varchar(10) | NO   | PRI | NULL    |       |
| reg_num       | varchar(10) | NO   | PRI | NULL    |       |
| report_num    | int         | NO   | PRI | NULL    |       |
| damage_amount | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> insert into participated values("A01","K052250",11,10000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`participated`, CONSTRAINT `participated_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> rename table participated to participate;
Query OK, 0 rows affected (0.02 sec)

mysql> insert into participate values("A01","K052250",11,10000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`participate`, CONSTRAINT `participate_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> select * from car;
+----------+--------+------+
| reg_num  | model  | year |
+----------+--------+------+
| KA031181 | Lancer | 1957 |
| KA041702 | Audi   | 2005 |
| KA052250 | Indica | 1990 |
| KA053408 | Honda  | 2008 |
| KA095477 | Toyota | 1998 |
+----------+--------+------+
5 rows in set (0.00 sec)

mysql> insert into owns values("A05","K041702");
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`owns`, CONSTRAINT `owns_ibfk_2` FOREIGN KEY (`reg_num`) REFERENCES `car` (`reg_num`))
mysql> insert into owns values("A05","KA041702");
Query OK, 1 row affected (0.00 sec)

mysql> insert into participate values("A01","KA052250",11,10000);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`insurance`.`participate`, CONSTRAINT `participate_ibfk_3` FOREIGN KEY (`report_num`) REFERENCES `accident` (`report_num`))
mysql> insert into accident values(11,"01-january-03","mysore road");
ERROR 1292 (22007): Incorrect date value: '01-january-03' for column 'accident_date' at row 1
mysql> insert into accident values(11,"01-JAN-03","mysore road");
ERROR 1292 (22007): Incorrect date value: '01-JAN-03' for column 'accident_date' at row 1
mysql> insert into accident values(11,01-JAN-03,"mysore road");
ERROR 1054 (42S22): Unknown column 'JAN' in 'field list'
mysql> DESC ACCIDENT;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| report_num    | int         | NO   | PRI | NULL    |       |
| accident_date | date        | YES  |     | NULL    |       |
| location      | varchar(20) | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

mysql> insert into accident values(11,2003-01-03,"mysore road");
ERROR 1292 (22007): Incorrect date value: '1999' for column 'accident_date' at row 1
mysql> insert into accident values(11,"2003-01-03","mysore road");
Query OK, 1 row affected (0.00 sec)

mysql> insert into accident values(12,"2002-02-04","mysore road");
Query OK, 1 row affected (0.00 sec)

mysql> insert into accident values(13,"2021-01-21","mysore road");
Query OK, 1 row affected (0.01 sec)

mysql> insert into accident values(13,"2017-02-08","mysore road");
ERROR 1062 (23000): Duplicate entry '13' for key 'accident.PRIMARY'
mysql> insert into accident values(14,"2017-02-08","mysore road");
Query OK, 1 row affected (0.00 sec)

mysql> insert into accident values(15,"2015-04-05","mysore road");
Query OK, 1 row affected (0.00 sec)

mysql> COMMIT;
Query OK, 0 rows affected (0.00 sec)

mysql> DESC PARTICIPATE;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| driver_id     | varchar(10) | NO   | PRI | NULL    |       |
| reg_num       | varchar(10) | NO   | PRI | NULL    |       |
| report_num    | int         | NO   | PRI | NULL    |       |
| damage_amount | int         | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> insert into PARTICIPATE values("A01","KA052250",11,10000);
Query OK, 1 row affected (0.00 sec)

mysql>
