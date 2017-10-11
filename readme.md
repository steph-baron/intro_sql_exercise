# Intro to SQL Assignment - Apartment Lab

## Part 1

- Create a database called apartmentlab 
- Using this database, create two tables, one for owners and one for properties
- Keep this relationship in mind when designing your schema:
	+ **One owner can have many properties**

### Tables

- The owners table should consist of: 
	+ owner_id (this should be the primary key as well as a unique number that increments automatically)
	+ name
	+ age
- The properties table should consist of:
	+ property_id (this should be the primary key as well as a unique number that increments automatically)
	+ name
	+ number of units
	+ owner_id (this should have the constraint NOT NULL)
		+ There should be also be a foreign key that references the owners table

### Questions
Write down the following sql statements that are required to solve the following tasks.

1. Show all the tables (this is a psql command). 

2. Show all the users (this is a psql command).  

3. Show all the data about the owners table (this is a psql command).  

4. Show the names of all owners.

5. Show the ages of all of the owners in ascending order.

6. Show the name of any owner whose name is Donald.

7. Show the age of all owners who are older than 30.

8. Show the name of all owners whose name starts with an E.

9. Add an owner named John who is 33 years old to the owners table.

10. Add an owner named Jane who is 43 years old to the owners table.

11. Change Jane's age to 30.

12. Change Jane's name to Janet.

13. Add a property named Archstone that has 20 units, owned by Janet.

14. Delete the owner named Janet.

15. Show all of the properties in alphabetical order that are not named Archstone and do not have an id of 3 or 5.

16. Count the total number of rows in the properties table

17. Show the highest age

18. Show the names of the first three owners in your owners table.

#### Bonus (this might require you to look up documentation online)

1. Create a foreign key that references the owner_id in the owners table and forces the constraint ON DELETE CASCADE.

2. Create a constraint on the properties table called positive_num_units that ensures that you can only add a num_units value that is greater than or equal to zero (research CHECK to do this)
	
2. Show all of the information from the owners table and the properties table in one joined table.  

3. In the properties table change the name of the column "name" to "property_name". 

4. Count the total number of properties where the owner_id is between 1 and 3.

5. Add a column to the owners table called fav_color with a type of TEXT
	
6. Change the name column in the owners table to be a type of VARCHAR(200)
	
7. Delete the owners table - what happens? why?

## Part 2 - Operators and Aggregates 

### Intro

**Before you get started, make sure you run `psql < part2.sql`**

### Questions
Write down the following sql statements that are required to solve the following tasks.

1. Find all the properties where the owner id is 2,3 or 4. 


2. Find all the owners who do not have an age of 22,23 or 25


5. Find all the owners who name is equal to the string 'b' concatenated with the string 'ob'. 

6. Using a regular expression, find all owners whose name begins with a lower case j.

7. Find all owners where the name starts with the letter 'b' (this search should be case insensitive and does not have to use a regular expression)

8. Find the lowest age of all the owners. Give this search result a name of minimum_age

9. Find the highest age of all the owners. Give this search result a name of maximum_age

10. Find the sum of all of the ages of the owners, call this search result total

11. Find the average age of all the owners, call this search result average_age

12. Find the average age of all the owners rounded to two decimal places, call this search result average_age

13. Find the number of owners who have an age, call this search result total_age_given.

14. Find the count of each age for the owners and order it by the age ascending. Your output should look like this:

	```
	 age | count
	-----+-------
	  33 |     3
	  53 |     1
	  73 |     1
	     |     0
	(4 rows)
	```

14. Find the count of each age for the owners and order it by the age ascending only if the age is greater than zero . Your output should look like this:
	
	```
	 age | count
	-----+-------
	  33 |     3
	  53 |     1
	  73 |     1
	(3 rows)
	```

1. Create a prepared statement called addOwner that inserts an owner with a name and age.

2. Execute the addOwner statement with the values of 'test' and 25;

3. Using the CASE operator, select the name and num\_units from the properties table, and when the num\_units is greater than 3000 a column called "status" should display 'huge'. If it is between 100 and 1000, "status" should display 'large'. If it is between 30 and 99 "status" should display 'medium'. If it is between 5 and 25 "status" should display 'small'. Otherwise "status" should display 'tiny'. Finally, order the results by the status and then the name - your output should look something like this

	```	
	               name               | num_units | status
	----------------------------------+-----------+--------
	 briar patch                      |      3133 | huge
	 island road                      |      1133 | huge
	 1020 Sunset Blvd                 |       532 | large
	 Figueroa Mt Road                 |       133 | large
	 archstone                        |        33 | medium
	 galvanize austin                 |        33 | medium
	 galvanize denver platte          |        33 | medium
	 galvanize san francisco          |        33 | medium
	 galvanize seattle                |        33 | medium
	 grand plaza                      |        33 | medium
	 hotel california                 |        33 | medium
	 lovely place                     |        33 | medium
	 galvanize fort collins           |        13 | small
	 galvanize boulder                |         4 | tiny
	 galvanize denver golden triangle |         3 | tiny
	(15 rows)
	```

5. Select all of the names and ages for owners. If the owner does not have an age, use the COALESCE operator to give it a value of -1

10. Create a view that stores the SQL command from question 17 (the query involving CASE)

8. Using the EXPLAIN keyword, SELECT all information from the properties_size view

11. Rename your view to prop_size

12. Delete the view called prop_size

#### Bonus (this might require you to look up documentation online [here](http://www.postgresql.org/docs/9.4/static/functions-aggregate.html) and [here](http://www.postgresql.org/docs/9.1/static/sql-createfunction.html)

1. Find the number of properties for each owner as a column called number\_of\_properties and display their name. Your output should look like this:

	```
	   name   | number_of_properties
	----------+----------------------
	 jim      |                    9
	 chrisine |                    2
	 bob      |                    2
	 tom      |                    2
	(4 rows)
	```

2. Using the rank() function, rank the number of units from highest to lowest: your output should look like 

	```
	 num_units | rank
	-----------+------
	      3133 |    1
	      1133 |    2
	       532 |    3
	       133 |    4
	        33 |    5
	        33 |    5
	        33 |    5
	        33 |    5
	        33 |    5
	        33 |    5
	        33 |    5
	        33 |    5
	        13 |   13
	         4 |   14
	         3 |   15
	(15 rows)
	```

3. Find the most commonly occuring num_units in the properties table using the mode() function. 


1. Write a function called calculate_sales_tax which takes in an integer and returns that value multiplied by 12%. Remember you will not be returning an INTEGER so make sure you return the correct type. 

2. Write a function call calc_annual_tax which takes in an integer and returns the result of the previous calculate_sales_tax function multiplied by 12.
	
