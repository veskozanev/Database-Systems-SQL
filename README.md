# Database-Systems-SQL

## Scenario

A haulage company manages its information using a relational database whose ER diagram is shown
at the end of this document. The database provided contains information from a typical six-month
period of operation. To fully understand the database structure, you will need to know some details
about the way the company operates, and some of the terminology used:
• A single trip may last between 2 and 10 days
• Trips are grouped by their start dates. A trip starting in May for example is therefore
deemed a “May trip” even if it ends in June.
• During a trip the driver visits a number of customer sites to pick up items of cargo, which are
then delivered to other customers
• Items may be picked up from a customer early in the trip, and other items delivered back to
the same customer later on
• Routing is complex and is handled separately. This means you do not need to consider the
relative location of customers on any given trip or the order in which they are visited
• Some items are fragile, and must therefore have their condition checked and signed off by
both pickup and delivery customers
• Some items are hazardous, and may only be transported by drivers with appropriate
qualifications
• Manifest is the term used for a list of the items of cargo in transit
• Each manifest item is identified by a barcode which is used for checking and billing
• The kerb weight of the vehicle is its unladen (empty) weight
• GVW stands for gross vehicle weight. This is the maximum allowable laden weight for the
vehicle
Section One - SELECT Statements (60 points)
The haulage database is available in MySQL format in Moodle as is the ER diagram in both
png and drawio format.
Choose any five questions to answer according to your ability. Questions 1 – 5 are worth 6
marks each, 6 – 10 are worth 9 marks, and 11 – 15 are worth 12 marks.
Each solution is a single SQL statement, which must be compatible with MySQL. Hard-coded
values should be avoided except when the value is included in the question. The target
answer has been provided for each question. The output from your SQL statement should
reproduce the results provided, including formatting and column order. Row ordering
should also be respected when asked for in the question.


## Solved queries
***Due to university regulations can not upload the code***
### 1. Trip 73450. How many items were transported during trip 73450?
+-------+  
| Items |  
+-------+  
| 6     |  
+-------+  
### 2. Dead-On Thirty. Find the trip in which exactly 30 items were transported?
+---------+  
| trip_id |  
+---------+  
| 73303   |  
+---------+  
### 3. Tristan Crumbie. Which two companies did Tristan Crumbie deliver to between the 21th and 22nd of May?
+------------------+  
| company_name     |  
+------------------+  
| Elephantine Ltd. |  
| Temerarious & Co |  
+------------------+  
### 4. What are they doing? Which driver was responsible for the shortest trip (shortest duration, not distance)? (A correct answer should avoid hardcoding the values shown below)
+------------+------------+------+  
| first_name | last_name  | days |  
+------------+------------+------+  
| Albert     | Phillimore | 0    |  
+------------+------------+------+  
### 5. The Low Five. Find the five (5) towns where we do the least business – i.e. the one where the fewest number of items are picked up and/or delivered. Order the result by number of items.
+------------+-------+  
| town       | Items |  
+------------+-------+  
| Canterbury | 40    |  
| Whitehaven | 45    |  
| Manchester | 49    |  
| Axbridge   | 52    |  
| Ely        | 53    |  
+------------+-------+  
### 6. Most Used. Find the five trucks that are most used during the six months covered by the data, which have a non-blank (non-null) value in the body column. Order by the number of trips on which they were used.
+--------+--------------+--------------+-------+  
| make   | body         | registration | trips |  
+--------+--------------+--------------+-------+  
| Scania | Chassis      | KN10WDG      | 26    |  
| Scania | Curtainsider | BD09FNE      | 25    |  
| MAN    | Box          | BR58BXG      | 24    |  
| MAN    | Box          | BR58BXC      | 23    |  
| MAN    | Box          | BR58BXE      | 23    |  
+--------+--------------+--------------+-------+  
### 7. Customer satisfaction. Each quarter the company emails the FIVE customers with the highest number of pickups (not manifest items) to check they are happy with the service. List the top FIVE customers for the first quarter (January, February, and March inclusive). Order by Pickups and then Reference number.
+-----------+----------------------+---------+  
| reference | company_name         | Pickups |  
+-----------+----------------------+---------+  
| 94        | Isostere Retail      | 19      |  
| 204       | Intrados Industrial  | 19      |  
| 12        | Afforest Group       | 18      |  
| 186       | Megathermic Inc.     | 18      |  
| 189       | Milquetoast Group    | 18      |  
+-----------+----------------------+---------+  
### 8. A, B, but not C. Which vehicles have never transported anything in category C? Only show vehicles whose registration plate begins with B.
+----------+--------------+  
| model    | registration |  
+----------+--------------+  
| P230 4x2 | BD10AYV      |  
| R270 6x2 | BD08AOC      |  
| TGM      | BR57BXF      |  
| TGM      | BR58BXE      |  
| TGM      | BR58BXV      |  
| TGM      | BR58BXM      |  
+----------+--------------+  
### 9. Travelling light. Usually, the sequence of pickups and deliveries has to be carefully managed so as not to exceed the vehicle’s capacity at any point. However, if the total weight of manifest items for the whole trip does not exceed the limit, these checks can be skipped. How many trips can proceed without checking in quarter 1 (see Q7)?
+----------+  
| COUNT(*) |  
+----------+  
| 183      |  
+----------+  
### 10. Average number of trips. What is the average number of trips per model of vehicle in
each month? To calculate this, you should divide the number of trips in each month by
the number of different (non-blank) values in the model field. You should not hardcode
the number of values in the model field. Order the results by month.
+------------+-------+  
| trip_month | trips |  
+------------+-------+  
| January    | 14.1  |  
| February   | 13.1  |  
| March      | 14.1  |  
| April      | 13.4  |  
| May        | 13.8  |  
| June       | 13.6  |  
| July       | 1.0   |  
+------------+-------+  
### 11. Dangerous driving. For all trips where hazardous good were transported, find the percentage of each category of item in the manifest. Sort in descending order of the percentage of hazardous items. (NB Outputis abbreviated – in your submission, all 48 rows should be included.)
+---------+------+------+------+  
| trip_id | A    | B    | C    |  
+---------+------+------+------+  
| 73832   | 44%  | 0%   | 56% |  
| 73404   | 60%  | 0%   | 40% |  
| 73773   | 63%  | 0%   | 38% |  
| 73551   | 64%  | 0%   | 36% |  
| 73013   | 67%  | 0%   | 33% |  
| …       | …    | …    | …   |  
| 74059   | 96%  | 0%   | 4%  |  
| 73049   | 96%  | 0%   | 4%  |  
+---------+------+------+------+  
### 12. Unused trucks. List the registration numbers of the trucks that were not in use between 1 and 5 May inclusive.
+--------------+  
| registration |  
+--------------+  
| SDU 567M |   
| PY56 BZU |  
| PY58 UHB |  
| PW09 EKX |  
| PY12 RSV |  
+--------------+  

## 2. ER Diagram

![er diagram](https://user-images.githubusercontent.com/57451986/129563939-b462e83a-36ab-4f87-9eb8-b6831e128899.png)

## 3. Normalisation 
![image](https://user-images.githubusercontent.com/57451986/129564246-cccd0177-fc59-4b88-bc1b-e5cfac95f02d.png)




