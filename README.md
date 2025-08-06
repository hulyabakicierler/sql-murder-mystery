SQL Murder Mystery

This project was completed using the "SQL Murder Mystery" database available on Kaggle. The goal is to identify both the murderer and the mastermind behind a crime committed on January 15, 2018 in SQL City, using only SQL queries.

This work was carried out after completing the SQL course by Halil Aydın on Miuul, as a way to reinforce what I learned in a more interactive and engaging scenario.

 Project Structure

sql-murder-mystery.db : SQLite database file

notebook.ipynb : Jupyter Notebook containing step-by-step SQL queries with explanations

README.md : Project overview and walkthrough (this file)

 Step-by-Step Solution Walkthrough

Explored database schema:

Used sqlite_master to list all tables

Located the murder case:

Found the incident that occurred on Jan 15, 2018 in SQL City from crime_scene_report

Extracted witness info from the description field

Identified witnesses:

Used the person table to locate Morty Schapiro & Annabel Miller by address

Retrieved their interviews:

Queried interview table to obtain witness statements

Clues pointed to a gold gym member with a bag labeled "48Z..." and a license plate containing "H42W"

Filtered gym members:

From get_fit_now_member, filtered gold members whose IDs started with "48Z"

get_fit_now_check_in showed Jeremy Bowers was at the gym on Jan 9, 2018

Confirmed vehicle match:

Queried drivers_license for license plates containing "H42W"

Matched Jeremy Bowers via person and license_id

Recorded first solution:

INSERT INTO solution (user, value) VALUES (1, 'Jeremy Bowers');

Final twist: checked Jeremy’s interview:

He confessed to being hired by a wealthy woman, 65–67 inches tall, with red hair, driving a Tesla Model S

She attended the SQL Symphony Concert 3 times in Dec 2017

Single-query suspect filtering:

SELECT p.name FROM person p
JOIN drivers_license dl ON p.license_id = dl.id
JOIN facebook_event_checkin fb ON p.id = fb.person_id
WHERE dl.gender = 'female' AND dl.hair_color = 'red'
  AND dl.height BETWEEN 65 AND 67
  AND dl.car_make = 'Tesla' AND dl.car_model = 'Model S'
  AND fb.event_name = 'SQL Symphony Concert'
  AND fb.date BETWEEN '20171201' AND '20171231'
GROUP BY p.id
HAVING COUNT(*) = 3;

Result: Miranda Priestly

Logged final solution:

INSERT INTO solution (user, value) VALUES (2, 'Miranda Priestly');

 Concepts Applied

SQL filtering: WHERE, LIKE, IN, BETWEEN

Table joins: JOIN

Aggregation: GROUP BY, HAVING

Logical deduction across tables

 References

Dataset: Kaggle - SQL Murder Mystery

Training: Miuul SQL Course

 Screenshots

Optional: add screenshots from your notebook to visualize steps.

 Try It Yourself

Open sql-murder-mystery.db in DB Browser or a Jupyter SQL extension

Follow notebook.ipynb step-by-step to solve the case

Explore your own deduction path!

 Feedback & Contact

If you're interested in interactive data analysis projects like this, feel free to connect! 

# sql-murder-mystery
An interactive SQL project where I investigated a murder case by querying a simulated database
