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

**Step 3: choose the dataset CSV file and click "Open", in the next 2 images click "Next". When "Proceed" button become active, click it and wait while importing will finish. In the last image, we're done, a new table "club_member_info" is created in the database.**

<img src="https://github.com/user-attachments/assets/1b8bd484-8254-4639-8591-ae653ad5d8b0" width=350 height=400>
<img src="https://github.com/user-attachments/assets/d4019cec-a5ed-4b11-9387-92552a74ec20" width=350 height=400>
<img src="https://github.com/user-attachments/assets/6ff3fee1-8237-47f6-841c-fac4c26f6f9e" width=350 height=400>
<img src="https://github.com/user-attachments/assets/ef70e049-b7c3-4a37-8c53-e7a029174d95" width=350 height=400>
<img src="https://github.com/user-attachments/assets/a210ece0-d482-4e2d-bcda-67393830c6f3" width=705 height=400>

### An overview of the dataset

**Step 1: once you have finished importing the data, switch to the data tab by clicking on it on the tab bar.**

<img src="https://github.com/user-attachments/assets/ce8a1bfa-cff8-4918-8e0d-d80659c63669">

**Step 2: ctrl+left click on the green highlighted table name to open the SQL console (next to the ![image](https://github.com/user-attachments/assets/2a9ccac1-1191-4474-b7e4-bd41e94eee62) icon).**

<img src="https://github.com/user-attachments/assets/97ebf473-4667-4a7b-ac84-b44fb6ee1352" width=350 height=400>

**Step 3: enter the sql statement as in the image and click the button ![image](https://github.com/user-attachments/assets/a88c21d6-3f67-4426-9e71-e0a82690177d)
to see a quick look at the first 10 records of the "club_member_info" table.**

<img src="https://github.com/user-attachments/assets/832c24dd-1270-4de9-94ff-d8f96b14593a" width=350 height=400>
<img src="https://github.com/user-attachments/assets/460dbcbd-a21b-4e08-9033-ac225cd4a296" width=350 height=400>

**SQL statement used in the above step:**

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

**Step 1: right click on the database name in the "Database Navigator" pane, select "SQL Editor → Open SQL console".**

<img src="https://github.com/user-attachments/assets/3fc025dc-da86-4109-adaa-bb900e84f004" height=400 width=350>

**Step 2: enter the SQL statement as shown in the image and click the "Run" button.**

<img src="https://github.com/user-attachments/assets/f56699da-46d0-4cd3-b130-431a33089ab3" height=400 width=350>

**Step 3: right click on the database name and click "Refresh" as shown below. A new table "club_member_info_cleaned" will be created.**

<img src="https://github.com/user-attachments/assets/2b0d0c15-0557-4a09-8613-70f4433fee98" height=400 width=350>
<img src="https://github.com/user-attachments/assets/f4b83888-dff3-4d0a-9793-e2c6a6109e0d">

**Step 4: double-click on the newly created table to go to the information page of that table, point to the Data tab, do as steps 1 and 2 of "An overview of the dataset" to open the SQL console. Enter the SQL as shown in the image and press the "Run" button. Then refresh the "club_member_info_cleaned" table. In the data tab of the table, you can see the data has been inserted from the "club_member_info" table.**

<img src="https://github.com/user-attachments/assets/a962dba0-f9cf-4a68-98af-fa79d9a60772">
<img src="https://github.com/user-attachments/assets/1f1a98d0-cb4f-415e-ae1e-33752b4d0a45" height=400 width=350>
<img src="https://github.com/user-attachments/assets/d97f53f0-fb80-4aee-bea8-e88d9eab8d55" height=400 width=350>

**SQL statements used:**

```sql
-- Create table "club_member_info_cleaned"

CREATE TABLE club_member_info_cleaned (
    id_member INTEGER PRIMARY KEY AUTOINCREMENT,
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

```sql

-- Copy all values from original table

INSERT INTO club_member_info_cleaned (full_name, age, martial_status, email, phone, full_address, job_title, membership_date)  SELECT * FROM club_member_info
```

### Data cleaning

To clean the data in the "club_member_info_cleaned" table, execute the following SQL statements in the database SQL console.

#### Adjust age greater than 100 to average age

```sql
UPDATE club_member_info_cleaned SET age = 42 WHERE age > 100
```

#### Remove spaces at the beginning and end of each member's full name

```sql
UPDATE club_member_info_cleaned SET full_name = TRIM(full_name)
```

#### Normalize names in the fullname column (first character of first name and last name is capitalized, remaining characters are lowercase).

```sql
-- Create initcap() function

CREATE TEMPORARY FUNCTION initcap(str) RETURNS STRING AS
BEGIN
  SELECT group_concat(upper(substr(word, 1, 1)) || substr(word, 2))
  FROM (
    SELECT trim(substr(str, instr(str, ' '), instr(str, ' ', instr(str, ' ')+1)-instr(str, ' '))) AS word
    FROM (
      SELECT ' ' || str || ' ' AS str
    )
  )
  WHERE word != '';
END;
```

After completing the above sql statement, continue with the sql statement below.

```sql
UPDATE club_member_info_cleaned SET full_name = initcap(full_name);
```
