# Pewlett-Hackard-Analysis

## Overview of Analysis

Six separate databases containing employee and organizational data from Pewlett-Hackard were XXXXX to determine the number of employees that qualify for retirement. An ERD was put together to facilitate identification of commonalities within the databases in order to retrieve employee number, names, birthdates, hiring dates, titles and department information.  

[Database Diagram](EmployeeDB.png)

![ EmployeeDB.png](https://github.com/coralrofa/Pewlett-Hackard-Analysis/blob/main/Pewlett-Hackard-Analysis/Visual%20aids/EmployeeDB.png)

Data was filtered for employees born between January 1, 1965 and December 31, 1965 and titles to  determine the number of prospective retirees per function and establish possible retention strategies to facilitate transition of new employees.  

```
Query to create a Mentorship Eligibility table

SELECT DISTINCT ON (e.emp_no) e.emp_no, 
	   e.first_name,
	   e.last_name,
	   e.birth_date, 
	   de.from_date,
	   de.to_date,
	   tl.title
INTO mentorship_eligibilty
FROM employees as e
INNER JOIN dept_emp as de
ON (e.emp_no = de.emp_no)
INNER JOIN titles as tl
ON (e.emp_no = tl.emp_no)
WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
AND (de.to_date = '9999-01-01')
ORDER BY emp_no;
```
## Results
*	Total of possible retirees: 72458
* Highest number of retirees: 24926 Senior Staff members and 25916 Senior Engineer
*	Lowest number of retirees: 2 Managers
*	Mentorship Program candidates: 1549

[Retirees per Job Title](retiring_titles.PNG)

![retiring_titles.PNG](https://github.com/coralrofa/Pewlett-Hackard-Analysis/blob/main/Pewlett-Hackard-Analysis/Visual%20aids/retiring_titles.PNG)
![ retiring_titles_graph_visualiser-1664499598484](https://github.com/coralrofa/Pewlett-Hackard-Analysis/blob/main/Pewlett-Hackard-Analysis/Visual%20aids/retiring_titles_graph_visualiser-1664499598484.png)

[Eligibility for Mentorship Program](mentorship_elegibility.png)

![ mentorship_elegibility.png ](https://github.com/coralrofa/Pewlett-Hackard-Analysis/blob/main/Pewlett-Hackard-Analysis/Visual%20aids/mentorship_elegibility.png)

## Summary
How many roles will need to be filled as the "silver tsunami" begins to make an impact?

*	There is a total of 72458 possible retirees.

    Query for total number or retirees
    ```
    SELECT SUM ( rt.count) AS total
    FROM retiring_titles AS rt
    ```

Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?
Senior Staff and Engineer level employees make up the bulk of the retirement candidates eligible for the mentorship program. 

* There are potentially enought qualified resources at multiple carrer levels for training if the mentorship program is successfull. 

[Eligibility for Mentorship Program per Title]( elegibility_per_title.png)

![ elegibility_per_title.png](https://github.com/coralrofa/Pewlett-Hackard-Analysis/blob/main/Pewlett-Hackard-Analysis/Visual%20aids/elegibility_per_title.png)

```
Query for mentorship eligible total per title

SELECT COUNT (me.emp_no), me.title
INTO elegibility_per_title
FROM mentorship_eligibility as me
GROUP BY me.title
ORDER BY me.title DESC;
```
