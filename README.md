# Vet Clinic Database Management System
![Database Management System for Vet Clinics and Visualization with Power BI](https://github.com/Coofone/Database-Management-System-for-Vet-Clinics-and-Visualization-with-Power-BI./assets/161744037/4143e1b0-e66d-411f-ad43-e34bfa5bb7db)


## 1.1 What is the  Happy and Healthy System?

Happy and Healthy is a Simple Database Management System designed specifically for veterinary clinics and animal healthcare facilities. 
It is built to track for customer behavior , Pet care Service. It can provide  systematic data storage mechanism for Customer Information, Clinical Service Records and Employee Related Data. 


## 1.2 Motivation about the database

Using a database management system in a pet clinic brings numerous benefits, including improved efficiency, better decision-making, better collaboration, and heightened data security. Embracing technology can transform the way pet clinics operate, leading to enhanced patient care and client satisfaction.


![Picture 1](https://github.com/Coofone/Database-Management-System-for-Vet-Clinics-and-Visualization-with-Power-BI./assets/161744037/76d96b6d-eded-4f3d-8c23-4ae1cbd30f04)

## ERD Diagram , SQL Statements and Query analysis 
<details>

  <summary> ERD Diagram </summary>  
![Picture2](https://github.com/Coofone/Database-Management-System-for-Vet-Clinics-and-Visualization-with-Power-BI./assets/161744037/52304124-1a8a-42e0-a9fa-72371aa35ea1)
</details>

<details>
<summary>SQL Statement for Database Tables</summary>  
## SQL Statement for Database tables

```sql
For System, total 9 tables are created as follow. 

CREATE TABLE tbl_location (
loc_id varchar(20),
loc_no_st VARCHAR2(200),
loc_qtr varchar(80),
loc_tsp varchar(80),
loc_district varchar(80),
loc_region varchar(80),
primary key (loc_id)
);

CREATE TABLE tbl_owner (
ow_id varchar(20),
ow_title varchar(10),
ow_name varchar(50),
ow_gender varchar(10),
ow_ph varchar(20),
ow_email varchar(50),
loc_id varchar(20),
primary key (ow_id) , 
Foreign key (loc_id) References tbl_location(loc_id)
);


CREATE TABLE tbl_breed(
br_id varchar(20),
br_type varchar(100),
br_breed varchar(100),
br_note varchar(255),
primary key (br_id)
);

CREATE TABLE tbl_pet (
pet_id varchar(20),
pet_name varchar(100),
pet_color varchar(100),
pet_size varchar(20),
pet_age INTEGER,
pet_gender varchar(20),
ow_id varchar(20),
br_id varchar(20),
primary key (pet_id),
Foreign key (ow_id) References tbl_owner(ow_id),
Foreign key (br_id) References tbl_breed(br_id)
);

CREATE TABLE tbl_service_price(
serv_id VARCHAR(20),
serv_type VARCHAR(100),
serv_description VARCHAR(100),
serv_Price INTEGER,
serv_Note VARCHAR(255),
primary key (serv_id)
);

CREATE TABLE tbl_department(
dept_id varchar(20),
dept_description varchar(100),
dept_note VARCHAR(255),
primary key (dept_id)
);

CREATE TABLE tbl_employee(
emp_id varchar(20),
emp_title varchar(10),
emp_name varchar(50),
emp_position varchar(50),
emp_phone varchar(20),
emp_email varchar(50),
emp_salary Integer,
emp_hiredate DATE, 
dept_id varchar(20) ,
emp_note varchar(255),
primary key (emp_id),
Foreign key (dept_id) References tbl_department(dept_id)
);

CREATE TABLE tbl_emp_service (
srp_id varchar(20),
emp_id varchar(20)  ,
serv_id varchar(20) ,
srp_note varchar(255),
primary key (srp_id),
Foreign key (emp_id) References tbl_employee(emp_id),
Foreign key (serv_id) References tbl_service_price(serv_id)
);

CREATE TABLE tbl_service_history (
case_id varchar(20),	
pet_id varchar(20),	
srp_id varchar(20) ,	
case_dlate Date,
case_note varchar(255),
primary key (case_id),
Foreign key (pet_id) References tbl_pet(pet_id),
Foreign key (srp_id) References tbl_emp_service(srp_id)
); 
```

## SQL Statements for Inserting Data
  You can use insert into or import from csv or excel files. 

```sql
1.	INSERT INTO location (loc_id, loc_no_st, loc_qtr, loc_tsp, loc_district, loc_region) VALUES ('loc_00001', ' No (47), ….. Street ', ' Yae Twin Kone Ward ', ' Mingalartaungnyunt ', ' Mingalartaungnyunt ', 'Yangon');

2.	INSERT INTO owner (ow_id, ow_title, ow_name, ow_gender, ow_ph, ow_email, loc_id) VALUES (‘ow_00001’,	‘Daw’,	‘,Zar Zar’, ’Female ’,	‘+95 09 773990067’,‘zarzar@email.com’, ‘loc_00001’);

3.	INSERT INTO breed (br_id, br_type, br_breed, br_note) VALUES ('br_00001', 'Dog', 'Labrador Retriever', 'Friendly and intelligent breed');

4.	INSERT INTO pet (pet_id, pet_name, pet_color, pet_size, pet_age, pet_gender, ow_id, br_id) VALUES ('pet_00001', 'Merlin', 'Black', 'Big', 9, 'Male', 'ow_00147', 'br_00001');

5.	INSERT INTO service_price (serv_id, serv_type, serv_description, serv_Price, serv_Note) VALUES ('serv_00001', 'Spay/Neuter Surgery ', 'Medical Service', 50000, ' ');

6.	INSERT INTO department (dept_id, dept_description, dept_note) VALUES ('dept_00001', 'Management ',’ ‘);

7.	INSERT INTO employee (emp_id, emp_title, emp_name, emp_position, emp_phone, emp_email, emp_salary, emp_hiredate, dept_id, emp_note) VALUES (''emp_00001' ,'Dr.' 'Mi Mi Soe' ,'General Manager', '+95 09 959706615', 'mimisoe@email.com', '1000000', '2015-07-09', 'dept_00001');

8.	INSERT INTO emp_service (srp_id, emp_id, serv_id, srp_note) VALUES ('srp_00001', 'emp_00001', 'serv_00001', ' ');

9.	INSERT INTO service_history (case_id, pet_id, srp_id, case_date, case_note)  ('case_00001', 'pet_00267', 'srp_0004', '2022-01-01',’ ‘);
```
</details>

<details>
<summary>Questions want to know </summary>  


+ SQL Statements for Answering Questions

For total number of pet owner based on location

```sql
SELECT loc_region, COUNT(*) AS total_customers
FROM tbl_location
WHERE loc_region IN ('Yangon', 'Mandalay', 'Nay Pyi Taw')
GROUP BY loc_region
ORDER BY total_customers DESC
```

for total number of pet owner based on specific location

```sql
SELECT loc_tsp, COUNT(*) AS customer_count
FROM tbl_location
WHERE loc_region = 'Yangon'
GROUP BY loc_district, loc_tsp
ORDER BY customer_count DESC
```

 What are the service available from the clinic?

```sql
//for total number of service 
SELECT serv_description, COUNT(DISTINCT serv_type) AS service_count
FROM tbl_service_price
GROUP BY serv_description;
```

 for detail service description

```sql
SELECT DISTINCT serv_description,serv_type
FROM tbl_service_price
ORDER BY serv_description DESC;
```
## Pet Related Quesitions 

What kinds of services are the most popular for pets?
//For Top 10 Popular Service
```sql
SELECT serv_type, COUNT(*) AS service_count
FROM tbl_service_history sh
JOIN emp_service es ON sh.srp_id = es.srp_id
JOIN service_price sp ON es.serv_id = sp.serv_id
GROUP BY serv_type
ORDER BY service_count DESC
FETCH FIRST 10 ROWS ONLY;
```

For Top 10 Popular Service for ‘dog’ and size ‘small’
```sql
SELECT sp.serv_type, COUNT(*) AS service_count
FROM tbl_service_history sh
JOIN emp_service es ON sh.srp_id = es.srp_id
JOIN service_price sp ON es.serv_id = sp.serv_id
JOIN pet p ON sh.pet_id = p.pet_id
JOIN breed b ON p.br_id = b.br_id
WHERE b.br_type = 'dog' and p.pet_size = 'big'
GROUP BY sp.serv_type
ORDER BY service_count DESC
FETCH FIRST 10 ROWS ONLY;
```

Which services are the most popular for young pets/old pets?
(Top 10 Popular Service for ‘dog’ and size ‘small’)
```sql
SELECT sp.serv_type, COUNT(*) AS service_count
FROM tbl_service_history sh
JOIN emp_service es ON sh.srp_id = es.srp_id
JOIN service_price sp ON es.serv_id = sp.serv_id
JOIN pet p ON sh.pet_id = p.pet_id
JOIN breed b ON p.br_id = b.br_id
WHERE b.br_type='dog' AND p.pet_age <3
GROUP BY sp.serv_type
ORDER BY service_count DESC
FETCH FIRST 10 ROWS ONLY;
```
## Department Related Questions 
Which department is the most popular department?
(the most Popular department) 
```sql
SELECT d.dept_description, COUNT(*) AS service_count
FROM service_history s
JOIN emp_service e ON s.srp_id =e.srp_id
JOIN employee em ON em.emp_id = e.emp_id
JOIN department d ON em.dept_id = d.dept_id
GROUP BY d.dept_description
ORDER BY service_count DESC;
```

3.	What is the average income of the clinic?
(average daily income)
```sql
SELECT ROUND(AVG(SUM(sp.serv_Price)),3) AS Average_Income_Per_day
FROM service_history sh
JOIN emp_service es ON sh.srp_id = es.srp_id
JOIN service_price sp ON es.serv_id = sp.serv_id
GROUP BY sh.case_date
```

average daily income via category
```sql
SELECT sp.serv_type As SERVICE_TYPE, ROUND(AVG(serv_Price),3) AS average_daily_income
FROM service_history s
join emp_service ems on s.srp_id = ems.srp_id
join service_price sp on ems.serv_id = sp.serv_id
Group BY sp.serv_type 
ORDER BY average_daily_income DESC
```


Find the average salary of the employee?

```sql
SELECT Round(AVG(emp_salary),3) AS average_salary
FROM employee
```

Find the total income according to the service?(....)

```
SELECT sp.serv_type, SUM(sp.serv_Price) AS total_income
FROM service_history sh
JOIN emp_service es ON sh.srp_id = es.srp_id
JOIN service_price sp ON es.serv_id = sp.serv_id
GROUP BY sp.serv_type
ORDER BY total_income DESC
```

What are the high demanded area?(For opening new branch)

```sql
SELECT l.loc_tsp, l.loc_district, l.loc_region, COUNT(*) AS customer_count
FROM location l
JOIN owner o ON l.loc_id = o.loc_id
where loc_tsp <> 'Thingangyun'
GROUP BY l.loc_tsp, l.loc_district, l.loc_region
```

To what kinds of pets is the clinic providing service?

```sql
SELECT br_type, COUNT(*) AS breed_count
FROM breed
WHERE br_type IN ('cat', 'dog')
GROUP BY br_type
ORDER BY br_type DESC
```

What is the most common pet's size?

```sql
SELECT "LOC_REGION", "PET_SIZE", "COUNT" FROM(
SELECT loc_region, pet_size, COUNT(*) AS count
FROM owner
JOIN pet ON owner.ow_id = pet.ow_id
JOIN location ON owner.loc_id = location.loc_id
GROUP BY loc_region, pet_size
ORDER BY loc_region DESC,count DESC
```

What are the highly demanded service by pets from Yangon?

```sql
SELECT loc_district, loc_tsp, COUNT(*) AS customer_count
FROM location
WHERE loc_region = 'Yangon'
GROUP BY loc_district, loc_tsp
ORDER BY customer count DESC
```
</details>

## 1.3 Power BI Dashboard
In earlier sections, we created and added data to our database. Now, let's build a Power BI dashboard to gain deeper business insights. This dashboard consists of three parts. 

#### Dashboard 
![Capture](https://github.com/Coofone/Database-Management-System-for-Vet-Clinics-and-Visualization-with-Power-BI./assets/161744037/7c4b8489-338b-40c6-bc52-94ac7ad2fff6)

[Happy and Health Vet Clinic Dashbaord.pdf](https://github.com/Coofone/Database-Management-System-for-Vet-Clinics-and-Visualization-with-Power-BI./files/15052200/Happy.and.Health.Vet.Clinic.Dashbaord.pdf)

### Questions Want to know 

#### Page 1: Pet-Related Information

<details>
<summary> Pet related information</summary>  
This page will focus on details about the pets themselves. The visuals on this page can help understand pet demographics, health, and services.

```
How are pets distributed by breed and type?
Visualize the breakdown of pets by breed using a pie chart or bar chart.

What is the average age of pets? How does this vary by breed?
Use a histogram or box plot to show age distribution by breed.

What are the common colors of pets per breed?
A stacked bar chart showing color distribution within each breed.

Which services are most commonly used for different pet sizes or ages?
A bubble chart or tree map to display service usage against pet size and age.

Trends in pet registration over time.
A line chart showing how pet registrations have trended over the years.

Health issues reported by breed or age group.
A table or list detailing the common health issues encountered by each breed or age group.
```
</details>

#### Page 2: Owner-Related Information
<details>

  <summary> Owner related information </summary>  

This page would provide insights into the pet owners, their demographics, and their relationship with the clinic.

```
What is the geographic distribution of pet owners?
A map visualization showing where most pet owners are located.

Analysis of owner demographics such as gender distribution.
A pie chart showing the gender breakdown of pet owners.

What are the common communication methods with owners (email, phone)?
A bar chart comparing the frequency of contact methods.

Relationship between owner location and types of pets owned.
A scatter plot or heat map showing types of pets by owner location.

Frequency of visits to the clinic by owner.
A histogram or line chart showing visit frequency.

Owner satisfaction with services received (if data available).
A gauge or scorecard displaying average satisfaction ratings.
```
</details>


#### Page 3: Clinic-Related Information

<details>
<summary> Clinic-Related Information  </summary>  
This page focuses on the operational aspects of the clinic, including services provided, employee performance, and financials.

```
What are the most popular services offered by the clinic?
A bar chart displaying the count of each type of service provided.

Employee performance based on the number of services rendered.
A leaderboard showing employees ranked by the number of services they have provided.

Financial analysis: Revenue from different services.
A line chart or area chart showing revenue trends by service type.

Clinic service demand by season or month.
A line chart showing service demand fluctuations throughout the year.

Efficiency of service delivery (time taken per service type).
A bar chart showing average duration of each type of service.

Departmental performance analysis.
Use a combination of bar charts and pie charts to show performance metrics by department.
```

Each page of your Power BI report will cater to different audiences, providing specific insights that are relevant to pets, their owners, and clinic operations. This structured approach will help stakeholders quickly find the information they need and make informed decisions.
</details>
