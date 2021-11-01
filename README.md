# Pewlett-Hackard-Analysis

## Analysis Overview
There are multiple employees at Pewlett Hackard that are approaching retirement age. The task associated with this project is to pull employee data
from multiple tables within the database. The data retrieval will show employees approaching retirement age to create a mentorship program for the 
retirement aged employees to mentor the new generation of employees.

## Results
Pewlett Hackard is a large corporation with many employees. When tasked to review the data on retirement aged employees multiple observations can be seen.

### Observations

- There are over 90k unique employees with varying job titles

![image](https://user-images.githubusercontent.com/90691846/139424288-71bf3423-322b-46a1-9e6a-5ffd1e085420.png)

- Approximately 300k employees with almost one third being eligible for retirment
- Many of the employees had multiple job titles throughout their career which led for the need to create a unique job title dataset
- A logical assumpion can be made that there is little turn over due to the large amount of staff still being employeed and near retirement age
- Out of these job titles there appears to be ample employees to assist in the mentorship program except for the manager job title group

## Summary
Due to one third of the total staff being close to retirement age, this event has been dubbed the "silver tsunami". Depending on when people retire, 90,398 roles will need to be filled.
There are 1549 employees who are eligible for the mentorship program. Out of those titles, 29,414 are for Senior Engineer and 28,254 are for Senior Staff, which is the highest need (see below).

![image](https://user-images.githubusercontent.com/90691846/139659896-674da3d7-33c7-4a64-a3d4-28dbd405372a.png)

To determine if this is an ample amount of employees for the mentorship, the below query was created to determine how many total employees currently have these unique job titles.

```
SELECT COUNT(e.emp_no), t.title
FROM employees AS e
INNER JOIN titles AS t
ON t.emp_no = e.emp_no
GROUP BY t.title
ORDER BY COUNT(e.emp_no)
```

This produced the following results:

![image](https://user-images.githubusercontent.com/90691846/139661019-21f255f9-18a1-47be-a544-f665397a3cb0.png)

When we run the following query we get the amount of employees for each title that are eligible for the mentorship program.

```
SELECT COUNT(DISTINCT(e.emp_no)), t.title
FROM employees AS e
INNER JOIN dept_emp AS de 
ON de.emp_no = e.emp_no
INNER JOIN titles AS t
ON t.emp_no = e.emp_no
WHERE (de.to_date = '9999-01-01')
AND (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
GROUP BY t.title;
```

Which has the following results:

![image](https://user-images.githubusercontent.com/90691846/139667217-26637d7a-e81b-4023-8c36-a7362937ef9c.png)


When we compare the retiring employees available to participate in the mentorship program to the amount of employees staffed in each area, then we can see there is enough employees to mentor the next generation.



