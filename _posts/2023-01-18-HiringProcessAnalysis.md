---
title: Hiring Process Analytics
date: 2023-01-18 10:30:00 -500
categories: [Projects, Data Analysis]
tags: [advance excel]     # TAG names should always be lowercase
---

## Project Description
In this project, we have data collected from the recent hiring campaign of the company. Stakeholders want the insights from the data. They have questions that can be answered with the statistics. Our job is to extract the essence from the data and find the answers.

## Approach
While starting with the project I looked into the data and got familiar with the fields. After I checked if the data had any outliers, empty fields, etc. As there were minimum outliers I filtered them out while analyzing the part.

## Tech-Stack Used
* Google sheets - For analysis, presenting tables and visualization
* Google Docs - For report

## Insights
### Hiring
I used the COUNTIF function to gather information about hiring across genders.

*Eg. =COUNTIFS('Main Sheet'!C:C, "Hired", 'Main Sheet'!D:D, "Male")*

| Gender  | Hiring count |
| ------- | ------------ |
| Male    | 2563         |
| Female  | 1856         |
| Unknown | 278          |

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR95wv0frNxJhECfGEX4rzGkg8dXDiCv8UFQ8d6TP-YSyraoEzuMduXrbW_xXRZLA/pubchart?oid=987546673&amp;format=interactive"></iframe>

### Average Salary
I used the pivot table to gather information about average salary across departments.

 | Department                | Average  of Offered Salary |
| ------------------------- | -------------------------- |
| General Management        | 58722.09                   |
| Purchase Department       | 52564.77                   |
| Service Department        | 50629.88                   |
| Finance Department        | 49628.01                   |
| Production Department     | 49448.48                   |
| Sales Department          | 49310.38                   |
| Operations Department     | 49151.35                   |
| Human Resource Department | 49002.28                   |
| Marketing Department      | 48489.94                   |

<iframe width="653" height="404" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR95wv0frNxJhECfGEX4rzGkg8dXDiCv8UFQ8d6TP-YSyraoEzuMduXrbW_xXRZLA/pubchart?oid=849104288&amp;format=interactive"></iframe>

### Class Intervals
I took class intervals for 10000 to get the statistics across the range of the salaries.

*Eg. COUNTIFS('Main Sheet'!G:G, ">10000", 'Main Sheet'!G:G, "<20001")*

| Class Interval | Frequency |
| -------------- | --------- |
| 0 - 10000      | 678       |
| 10001 - 20000  | 732       |
| 20001 - 30000  | 711       |
| 30001 - 40000  | 732       |
| 40001 - 50000  | 781       |
| 50001 - 60000  | 750       |
| 60001 - 70000  | 698       |
| 70001 - 80000  | 734       |
| 80001 - 90000  | 711       |
| 90000 - 100000 | 659       |
| 100001+        | 3         |

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR95wv0frNxJhECfGEX4rzGkg8dXDiCv8UFQ8d6TP-YSyraoEzuMduXrbW_xXRZLA/pubchart?oid=1168336795&amp;format=interactive"></iframe>

### Charts and Plots
Using the pivot table I calculated the number of people working in each department.
And then applied a pie chart on that data to get the visual representation of the calculated data.

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR95wv0frNxJhECfGEX4rzGkg8dXDiCv8UFQ8d6TP-YSyraoEzuMduXrbW_xXRZLA/pubchart?oid=1633290183&amp;format=interactive"></iframe>

### Charts
Using the pivot table I calculated the number of people working in each post.
And then applied a bar chart on that data to get the visual representation of the calculated data.

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vR95wv0frNxJhECfGEX4rzGkg8dXDiCv8UFQ8d6TP-YSyraoEzuMduXrbW_xXRZLA/pubchart?oid=1673006482&amp;format=interactive"></iframe>

## Results
I was able to find the data driven solutions for all the questions that were asked by the stakeholders. Also this project has helped me to revise and polish the knowledge of Google Sheets/ Excel.

I have used advanced excel techniques like **formulas, pivot tables, charts, filters etc.**
