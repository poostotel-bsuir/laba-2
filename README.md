# 🎯 Lab 2: Planning and implementing a Backup strategy. Importing and exporting DATA. Restoring databases

## 💡 Introduction
The DBMS Semester 2 curriculum involves learning how to administer, maintain and manage data warehouse infrastructure. As part of the curriculum update, it was decided to provide students with the opportunity to perform laboratory work using containerisation tools instead of virtualisation tools. This series of GitHub materials will provide a methodological guide for performing basic tasks from the mandatory labs using Docker containers with MS SQL Server on board.

**The report to the laboratory work should be prepared in Microsoft Word according to ***СТП 2024*** and attached in .pdf format to the repository files.**

Screenshots should show the key points in steps of the lab. It will help you to response, and us – to ask correct questions. Do all possible steps manually, not only TSQL, it is not critical to write SQL, it is critical you could recognize the actions and steps on interview, and prove your answer. 

> Happy Hunger Games and may the odds be ever in your favor!

## 🔗 Resources

- [СТП 2024](https://www.bsuir.by/m/12_100229_1_185586.pdf)

- [Инструкция по установке Docker Desktop и развёртыванию вашего первого контейнера с MS SQL Server](https://github.com/poostotel-bsuir/laba-1/blob/main/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F_%D0%BF%D0%BE_MS_SQL_%D0%BD%D0%B0_%D0%B1%D0%B0%D0%B7%D0%B5_Docker_Desktop.docx)

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

- [Configure Database Engine Instances (SQL Server)](https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/configure-database-engine-instances-sql-server?view=sql-server-ver15)

- [Back Up and Restore of SQL Server Databases](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases?view=sql-server-ver15)

- [Restore a Database Backup Using SSMS](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-ver15)

- [Restore the master database (Transact-SQL)](https://learn.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-the-master-database-transact-sql?view=sql-server-ver15)

- [SQL Constraints](https://www.tutorialspoint.com/sql/sql-constraints.htm)

- [SQL Indexes](https://www.tutorialspoint.com/sql/sql-indexes.htm)

- [SQL Server and Azure SQL index architecture and design guide](https://learn.microsoft.com/en-us/sql/relational-databases/sql-server-index-design-guide?view=sql-server-ver15)

- [Use sqlcmd](https://learn.microsoft.com/en-us/sql/tools/sqlcmd/sqlcmd-use-utility?view=sql-server-ver15)

## 📚 Objective
Develop and test a strategy for backup, data import/export and database recovery in MS SQL Server using Docker containers from previous lab work.

## 📝 Tasks

### 📌 Task 1: Preparing Lab infrastructure
- Attach “AdventureWorks” to one of the SQL instances (if was not done).
- Make Full backup of DB with simple recovery model.
- Restore Database to new database, named it as “your student name”_db (vshulhach_db for example).

### 📌 Task 2: Working with DB backups and recovering
- Set recovery model to FULL. Make backup of DB. Make backup of transaction log. Perform everything using your custom dataset. Backups should be compressed. Compare sizes of backups. Do not forget about screenshots.
- Perform your custom data changes in DB. The purpose of these changes – to make DB different than its backup, so update and change what ever you want. You can use transactions with SELECT statement to show changes, as done on the picture. Use COMMIT TRAN to apply changes to DB. Use right click on the table – select top 1000 to see table structure and data, what you can change. Make changes at least at 3 different tables. (with screenshots of SELECT before – script to change something – SELECT after). Make differential backups for each table you change (before 1 table, before 2nd, before 3rd)

Example

![image](https://github.com/user-attachments/assets/854b5e77-908b-4642-be57-102bfae3c118)


- Make Full backup of DB, create new media set. Use compression, no not overwrite previous media set with backups.
- Restore full backup, which was done in simple model, on the second server (the name should be custom, the same as on 1st server). Try to restore backup via network path from the first server. Skip network restoration if you cannot. Use SELECT statement to show, that data is not the same on both Servers – with the fresh DB and you customized one.

Example

![image](https://github.com/user-attachments/assets/42edeaa6-3125-4316-b57a-cc0f0409ddfc)

- Restore differential backups in correct sequence on 2nd server, show the differences in tables step by step, according the order you changed them on first server.
- Copy full latest backup on second SQL server. Restore it with latest timeline point to newer created DB. Compare data with first server state.
- Restore N-1 timeline point. Show, that data is differ from the original server.
- Create Database “Test_’Student name’” on any instance. Make backup for master database. Create another database “Test_’Student name’_2”. Delete previously created database.
- Recover DB Master from backup. Pay attention, what is the result after recovery and why. See additional materials for help.
> in case of server will be busy by any identity, and you cannot login to it – you can exactly define application to use SQL in the single mode.

> Everything is working using SQLCMD.EXE. That task could be done not using scripting, I hope you will never have to automate master DB recovering.

- Make “Student_name” db the same on both servers.

### ⚡ Extra task 1: Create a PowerShell wrapper for scenario
- Create a backup for Adventure Work DB,  and restore it on the instance 1.
- Make update of any table with SELECT Before and SELECT after.
- Create full compressed backup of DB.
- Restore it on second Instance.
- Write everything in log file, Log file should be Human readable, with commented steps.
> Tee-Object can help

### ⚡ Extra task 2: Perform Task from presentation
> During task creating keep in mind and perform MS recommendation for better performance (Should be in script).

## 📙 Manual

### 🟡 Восстановление базы данных

Присоединим базу данных AdventureWorks2012 к серверу, расположенному на локальном компьютере. Для этого в обозревателе объектов необходимо щелкнуть ПКМ по Базы данных, затем выбрать восстановить базу данных. Выбрать с устройства, и указать необходимый файл.

Выбор устройства резервного копирования

![image](https://github.com/user-attachments/assets/c89bd1ce-feb1-4c28-9c65-e86572313244)

Выбор файла с резервной копией

![image](https://github.com/user-attachments/assets/699118ac-6ece-4e75-bfc8-0bb582a0a14a)

Процесс восстановления базы данных

![image](https://github.com/user-attachments/assets/69c635b2-d32b-4399-a62f-f3668b64c118)

После восстановления базы данных, нужно создать ее резервную копию, после чего удалить саму БД и восстановить ее под новым именем (например myTest_db).

Команда для создания резервной копии, удаления БД и восстановления:

```sql
-- Создание резервной копии базы данных AdventureWorksDM2012
BACKUP DATABASE AdventureWorksDM2012
TO DISK = '/var/opt/mssql/backups/myTest_db.bak';

-- Удаление базы данных для демонстрации восстановления
DROP DATABASE AdventureWorksDM2012;

-- Восстановление базы данных из резервной копии
RESTORE DATABASE myTest_db
FROM DISK = '/var/opt/mssql/backups/myTest_db.bak'
WITH REPLACE,
MOVE 'AdventureWorksDM2012' TO '/var/opt/mssql/data/myTest_db.mdf',
MOVE 'AdventureWorksDM2012_log' TO '/var/opt/mssql/logs/myTest_db_log.ldf';
```

Восстановление базы данных под именем myTest_db

![image](https://github.com/user-attachments/assets/5e13c236-5a37-4ec3-8d1b-5352c8033920)

### 🟡 Полное восстановление базы данных

Для дальнейшей работы необходимо поменять модель восстановления на полную, так как простая модель не поддерживает сохранение логов, дифференциальные бекапы. Для этого необходимо нажать ПКМ по базе данных, выбрать раздел Свойства, и в параметрах указать модель восстановления на полную.

Настройка модели восстановления

![image](https://github.com/user-attachments/assets/190bed14-f491-4497-9576-dae663ea066c)

После этого по заданию необходимо выполнить сжатие бэкапов БД.

Команда для установки сжатых бэкапов:
```sql
-- Настройка сжатия резервных копий по умолчанию
EXEC sys.sp_configure N'backup compression default', N'1';  
GO  
RECONFIGURE WITH OVERRIDE;  
GO
```

Установка сжатых бэкапов

![image](https://github.com/user-attachments/assets/16b69172-3eb5-44bc-a8a1-4030b2dbba83)

Выполним бэкапы базы данных и ее логов.

Команда для создания сжатых резервных копий базы данных и логов:
```sql
-- Создание сжатых резервных копий
BACKUP DATABASE myTest_db
TO DISK = '/var/opt/mssql/backups/myTest_db_compressed.bak'
WITH COMPRESSION;

BACKUP LOG myTest_db
TO DISK = '/var/opt/mssql/backups/myTest_db_compressed.bak'
WITH COMPRESSION;
```

Бэкап базы данных и логов

![image](https://github.com/user-attachments/assets/dd79e2d8-b385-423f-9af9-bb2fab2b27ef)

После этого необходимо выполнить 3 произвольных изменения в базе данных. И делать бэкапы после каждого, чтобы потом можно было отследить изменения.

После каждого выполнения изменения выполните команду COMMIT TRAN и сделайте дифференцированную копию базы данных

Создание дифференцированной копии базы данных

![image](https://github.com/user-attachments/assets/396496f1-ce67-4de3-a0d6-f5ef00629bd2)

Команда для изменения имени человека:

```sql
-- Транзакция обновления клиента
SELECT FirstName FROM DimCustomer
WHERE CustomerKey = 11000;

BEGIN TRAN;
UPDATE DimCustomer
SET FirstName = 'TestName'
WHERE CustomerKey = 11000;

SELECT FirstName FROM DimCustomer
WHERE CustomerKey = 11000;
```

Изменение имени человека

![image](https://github.com/user-attachments/assets/e01de686-818b-41bc-8dc2-f01cce931367)

Команда для изменения класса продуктов:
```sql
-- Транзакция обновления класса продуктов (исправлено)
SELECT Class FROM DimProduct
WHERE ProductKey BETWEEN 1 AND 5;

BEGIN TRAN;
UPDATE DimProduct
SET Class = 'L'
WHERE ProductKey BETWEEN 1 AND 5;

SELECT Class FROM DimProduct
WHERE ProductKey BETWEEN 1 AND 5;
COMMIT TRAN;
```

Изменение класса продуктов

![image](https://github.com/user-attachments/assets/8b2d81df-14da-4111-b8ef-ecbd7e74f936)

Команда для изменения описания продуктов:
```sql
-- Транзакция обновления описания продукта
SELECT EnglishDescription FROM DimProduct
WHERE ProductKey = 1;

BEGIN TRAN;
UPDATE DimProduct
SET EnglishDescription = 'Adjustable Race'
WHERE ProductKey = 1;

SELECT EnglishDescription FROM DimProduct
WHERE ProductKey = 1;
COMMIT TRAN;
```

Изменение описания продукта

![image](https://github.com/user-attachments/assets/a91ae151-8ad0-4aae-9f9b-a9fa012713ba)

Теперь перенесём созданные нами резервные копии базы данных на второй сервер по аналогии с тем, как это было сделано в первой лабораторной работе, выполним последовательное восстановление бэкапов и отследим выполнение.

> При попытке восстановления дифференцированной копии возможно придётся указать конкретную копию для восстановления:
```sql
USE master;
RESTORE DATABASE myTest_db
FROM DISK = '/var/opt/mssql/backups/myTest_db_compressed.bak'
WITH FILE = 2, REPLACE, NORECOVERY;
```
> Иначе может возникнуть ошибка: This differential backup cannot be restored because the database has not been restored to the correct earlier state.

Команда восстановления из первого бэкапа:
```sql
-- Восстановление из дифференциального бэкапа №1
RESTORE DATABASE myTest_db
FROM DISK = '/var/opt/mssql/backups/myTest_db_compressed_Diff1.bak'
WITH REPLACE;

USE myTest_db;

SELECT FirstName FROM DimCustomer
WHERE CustomerKey = 11000;

SELECT Class FROM DimProduct
WHERE ProductKey BETWEEN 1 AND 5;

SELECT EnglishDescription FROM DimProduct
WHERE ProductKey = 1;
```

Результат первого бэкапа

![image](https://github.com/user-attachments/assets/a10f0d43-a3f0-4a2b-bfcc-08326b6575a9)

Команда восстановления из второго бэкапа:
```sql
-- Восстановление из дифференциального бэкапа №2
RESTORE DATABASE myTest_db
FROM DISK = '/var/opt/mssql/backups/myTest_db_compressed_Diff2.bak'
WITH REPLACE;

USE myTest_db;

SELECT FirstName FROM DimCustomer
WHERE CustomerKey = 11000;

SELECT Class FROM DimProduct
WHERE ProductKey BETWEEN 1 AND 5;

SELECT EnglishDescription FROM DimProduct
WHERE ProductKey = 1;
```

Результат второго бэкапа

![image](https://github.com/user-attachments/assets/0250d2a1-bf3b-4bdd-81d4-52a6ed7d81cf)

Команда восстановления из третьего бэкапа:
```sql
-- Восстановление из дифференциального бэкапа №3
RESTORE DATABASE myTest_db
FROM DISK = '/var/opt/mssql/backups/myTest_db_compressed_Diff3.bak'
WITH REPLACE;

USE myTest_db;

SELECT FirstName FROM DimCustomer
WHERE CustomerKey = 11000;

SELECT Class FROM DimProduct
WHERE ProductKey BETWEEN 1 AND 5;

SELECT EnglishDescription FROM DimProduct
WHERE ProductKey = 1;
```

Результат третьего бэкапа

![image](https://github.com/user-attachments/assets/ad65a8d8-3433-4d41-b5a8-90ea28216e09)
  
## 🧠 Self-Check Questionnaire

### 🔍 Question 1:
What ports do SQL server services use? What services are available and why?

### 🔍 Question 2:
What databases are needed to run SQL Server? Their functions.

### 🔍 Question 3:
What protocols are used to connect to SQL Server? How they work, how to connect from GUI/console for each protocol? How to define the connection protocol?

### 🔍 Question 4:
How SQL server can be installed? Types of installations, types of instances. How to install more than one SQL instance?
 
### 🔍 Question 5:
What are the services that SQL server needs to run?

### 🔍 Question 6:
What files are used by SQL server?

### 🔍 Question 7:
Types of backups, types of recovery models.

### 🔍 Question 8:
How to switch recovery models? How to switch backup types?

### 🔍 Question 9:
What is the difference between backups? In what order to do backups from a performance optimisation point of view?

### 🔍 Question 10:
In what order to restore backups (in a spherical vacuum situation when they are all different files)?

### 🔍 Question 11:
What is a dataset?

### 🔍 Question 12:
How databases can be moved between servers? How SQL Server can pick up backups from the network?

### 🔍 Question 13:
What is the name of the tool for SQL server management (GUI, console)?

### 🔍 Question 14:
How to restore system databases?

### 🔍 Question 15:
How to provide SQL Server and its services access to resources via Windows AD/authorisation centre?
