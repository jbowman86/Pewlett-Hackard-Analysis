# Pewlett-Hackard Analysis 

## Project Overview 

### Purpose

The purpose of this analysis is to prepare Pewlett-Hackard for the upcoming “silver tsunami”, in which a number of their employees will begin retiring at a rapid rate.  The company wants to prepare for this upcoming problem by understanding the required obligations for retirement packages with respect to those employees who are going to retire.  Additionally, Pewlett-Hackard would like to gain further insight into the future needs for filling open positions created by the “silver tsunami”. In order to ensure a smooth transition this analysis focuses on the following: 

1.	Develop an entity relationship diagram (ERD) that outlines the connections between multiple datasets containing employee information
2.	Identify the retiring employees by their title.
2.	Determine the sum of retiring employees grouped by title.
3.	Identify the employees eligible for participation in the mentorship program.
4.	Determine the number of roles-to-fill grouped by title and department.
5.	Determine the number of qualified, retirement-ready employees to mentor the next generation grouped by title and department.

### Background

The data was collected from six CSV files containing information on Pewlett-Hackard employees.  These datasets can be obtained via the links below:

  - Departments Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/departments.csv
  - Department Employees Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/dept_emp.csv
  - Department Manager Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/dept_manager.csv
  - Employees Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/employees.csv  
  - Salaries Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/salaries.csv  
  - Titles Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/titles.csv

After review of these datasets, an ERD was created to visualize and gain further understanding of the key elements of each group of employee data.  The completed ERD can be seen below:

![
](https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/ERD_Pewlett_Hackard.png)

Postgres and pgAdmin interfaces were used to analyse the employee data.  SQL queries were completed to create linkages amongst the data tables by joining primary keys from each data set together along with established foreign keys.  Additional SQL queries were written to compile a list of retiring employees by title as well as a list of employees eligible for mentorship.

## Results  

- A list of retiring employees was created by merging data from the employees and titles tables via an inner join.  The dataset was then filtered by birth date in order to determine which employees are approaching retirement age.  The completed list of retiring employees is included below:

Retirement Titles Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/retirement_titles.csv

The resulting list includes 133,776 entries; however, there appears to be some duplications with the new dataset.  Individuals who held multiple positions at Pewlett-Hackard may have multiple entries in the list.

- A table containing unique titles for each retiring employee was created in order to eliminate the duplicate entries for employees with multiple titles within the company.  This was completed by joining the employees and titles tables, filtering them by date of birth and date hired, removing duplicates, and ordering the data points by date hired.  It was found that there are an estimated 90,398 employees retiring as per the conditions outlined above.  The unique_titles table can be observed via the following link:

Unique Titles Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/unique_titles.csv

- A further breakdown of the potential retirees by position held within the company is: 29,414 Senior Engineers, 28,254 Senior Staff, 14,222 Engineers, 12,243 Staff, 4,502 Technique Leaders, 1,761 Assistant Engineers, and 2 Managers. 

Retiring Titles Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/retiring_titles.csv

- A mentorship_eligibility table was created by joining the employees, department employees, and titles tables. The criteria for the joining the tables were that employees were born in 1965 and that they were currently working at Pewlett-Hackard. There were 1,549 employees eligible for mentorship.

Mentorship Eligibility Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/mentorship_eligibility.csv

- Out of the mentorship eligible employees, there are 402 Engineers, 392 Senior Staff, 332 Staff, 290 Senior Engineers, 77 Technique Leaders, and 56 Assistant Engineers. 

## Summary

1.	As the “silver tsunami” approaches, Pewlett-Hackard should anticipate  that there will be 90,398 roles that will need to be filled across 7 different categories within the organization.  The majority of these positions will be senior roles within departments.  Included below is the list of potential retirees broken down by position held:

Retiring Titles Dataset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/retiring_titles.csv

2.	With 1,549 employees available for the mentorship program, it appears that there are not enough qualified employees ready for retirement in the departments to mentor the next generation of employees. Based on these findings, each mentor would need to train/advice approximately 58 individuals, a very difficult task for any individual who is not working full-time.  By breaking down the mentorship eligible employees by department in the query below, we can see that the employees are proportionally spread to the employees that are retiring. 
```
SELECT COUNT(title), title
FROM mentorship_eligibility
GROUP BY title
ORDER BY COUNT(title) DESC;
```
Mentor Count Datset: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/mentor_counts.csv

However if we extend the mentorship eligibility by 1 year to employees born in 1964 there are 19,905 eligible employees which is much more manageable.  The SQL query and output for these findings are included below:

```
WHERE (e.birth_date BETWEEN '1964-01-01' AND '1965-12-31')
```
Mentorship Eligibility Extended Counts: https://github.com/jbowman86/Pewlett-Hackard-Analysis/blob/main/Data/mentorship_eligibility_extended_count.csv

