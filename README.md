# SQL data cleaning
This is an educational project on data cleaning and preparation using SQL by Duy Phi. The original database in CSV format is located in the file club_member_info.csv. This project will use SQLite database and will be implemented in DBeaver. Here, we will explore the steps that need to be applied to obtain a cleansed version of the dataset.

## Prepare a SQLite database to work

### Create a new database connection

**Step 1: in DBeaver, to create a connection to a new database, right-click in the "Database Navigator" pane, select "Create → Connection".**

<img src="https://github.com/user-attachments/assets/f714e78f-5364-4119-ac8a-6c460e12d862" width="350" height="400">

**Step 2: select SQLite database as image below and click "Next".**

<img src="https://github.com/user-attachments/assets/daaead2f-d60d-4123-ae79-b96ee5f86d14" width="350" height="400">

**Step 3: click on "Create" button, the dialog box in the next image appears, select where to save the database file and name this new database "club_members.db" and click the "Save" button. In the next image, click the "Finish" button. Finally, a new database appears in the "Database Nagivator" pane.**

<img src="https://github.com/user-attachments/assets/0b71d80f-bf4a-47ce-b6cd-1bffb40ab2d1" width="350" height="400">
<img src="https://github.com/user-attachments/assets/5e22cdf0-295a-4d4f-bb41-c25e1771d97a" width=350 height=400>
<img src="https://github.com/user-attachments/assets/b97d1cb9-fc62-4e35-9545-9dc818efa7bb" width=350 height=400>
<img src="https://github.com/user-attachments/assets/53550b39-56b4-40a8-81f5-f6e957f880e2" width=350 height=400>

### Import the CSV dataset into database

**Step 1: expand the newly created database by double-clicking on its name, right-click on "Tables", select the "Import Data" option.**

<img src="https://github.com/user-attachments/assets/65015155-8a89-4939-a0ab-1f57abb7ea3b" width=350 height=400>

**Step 2: check that CSV option is chosen and click "Next".**

<img src="https://github.com/user-attachments/assets/f1eed528-aed6-4c65-bd14-bb2b4d4dcad1" width=350 height=400>

**Step 3: choose the dataset CSV file and click "Open", in the next 2 images click "Next". When "Proceed" button become active, click it and wait while importing will finish. In the last image, you have completed importing data from the CSV file into the database.**

<img src="https://github.com/user-attachments/assets/1b8bd484-8254-4639-8591-ae653ad5d8b0" width=350 height=400>
<img src="https://github.com/user-attachments/assets/d4019cec-a5ed-4b11-9387-92552a74ec20" width=350 height=400>
<img src="https://github.com/user-attachments/assets/6ff3fee1-8237-47f6-841c-fac4c26f6f9e" width=350 height=400>
<img src="https://github.com/user-attachments/assets/ef70e049-b7c3-4a37-8c53-e7a029174d95" width=350 height=400>
<img src="https://github.com/user-attachments/assets/a210ece0-d482-4e2d-bcda-67393830c6f3" width=705 height=400>

### An overview of the dataset
First we need to display the first 10 records to get a quick look at the dataset by using following sql statement.
```sql
SELECT * FROM club_member_info LIMIT 10
```
**Results table:**

|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

## Cleaning and documenting 
### Make a copy of table

```sql
CREATE TABLE club_member_info_cleaned (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);
```
Copy all values from original table

```sql 
INSERT INTO club_member_info_cleaned SELECT * FROM club_member_info
```

### Data cleaning

#### Adjust age greater than 100 to average age

```sql
UPDATE club_member_info_cleaned SET age = 42 WHERE age > 100
```

#### Remove spaces at the beginning and end of each member's full name

```sql
UPDATE club_member_info_cleaned SET full_name = TRIM(full_name)
```

#### Capitalize all characters in the member's name

```sql
UPDATE club_member_info_cleaned SET full_name = UPPER(full_name)
```

#### Delete rows with duplicate emails

```sql
DELETE FROM club_member_info_cleaned WHERE rowid IN
(
SELECT cmic.rowid FROM club_member_info_cleaned cmic
JOIN
	(SELECT email, MIN(rowid) as min_id FROM club_member_info_cleaned 
	 GROUP BY email) as sub
ON cmic.email = sub.email
WHERE cmic.rowid > sub.min_id
)
```
