---
title: Call Volume Trend Analysis
date: 2023-01-10 10:30:00 -500
categories: [Projects, Data Analysis]
tags: [excel, statistics]     # TAG names should always be lowercase
---

## Project Description
This project had a dataset containing the data about call volume trends in the call center. We are supposed to analyze the data and extract the insights out of it.

## Approach
1. Get familiar with the data and fields from dataset
2. Clean the data.
3. Perform analysis using Excel. 
4. Create a detailed report.

## Tech-Stack Used
* Google sheets - For Analysis and visualization
* Google Docs - For report

## Insights
### Calculate the average call time duration for all incoming calls received by agents (in each Time_Bucket).
1. Using the pivot table, Average duration in minutes and seconds is calculated.
![image1](/assets/img/CallVolume/Capture(0).JPG){: width="" height="360"}

### Show the total volume/ number of calls coming in via charts/ graphs [Number of calls v/s Time].
1. Using the pivot table, call volume for each time bucket is calculated.
2. After that, the percentage is calculated by using Excel formulas.![image1](/assets/img/CallVolume/Capture(1).JPG){: width="" height="360"}

### The current abandonment rate is approximately 30%. Propose a manpower plan required during each time bucket [between 9am to 9pm] to reduce the abandon rate to 10%.
1. Calculate the average call volume per day using pivot table.![image1](/assets/img/CallVolume/Capture(2).JPG){: width="" height="360"}
2. Assume, the agent works 6 days a week and takes 4 unplanned leaves in a month i.e. 30 days - 4 leaves - 5 sundays = 21 working days.
3. Agent attends call for 60% of his shift i.e. 60% of (9 hrs of shift - 1.5 hrs for lunch) = 4.5 hrs.
4. As to attend 70% calls call center takes 196.48 hrs, to attend 90% calls we need 252.4
5. So we need 252.4/4.5 = 56 agents to 90% attend calls.
6. Using the pivot table, percentage for every time bucket is calculated and 56 agents are distributed.

![image1](/assets/img/CallVolume/Capture(3).JPG){: width="" height="360"}

### Let’s say customers also call this ABC insurance company at night but don't get an answer as there are no agents to answer, this creates a bad customer experience for this Insurance company. Suppose every 100 calls that customer made during 9 Am to 9 Pm, customer also made 30 calls at night between interval [9 Pm to 9 Am] and distribution of those 30 calls are as follows.
1. 30% calls come at night (9pm - 9am) i.e. **30% of average daily calls(5130 calls) are 1539**.
2. With a 10% of abandonment rate we need to attend **1385 calls per night**.
3. We need **(1385*196.48) / 3600 = 75.71 man hours**.
4. That is we need **75.71 / 4.5 = 17 agents** at night **to attend 90% of calls**.
5. Total agents needed to attend 90% calls throughout the day are **56 at day and 17 at night** i.e. **73 agents**.


## Results
I was able to find the data driven solutions for all the questions that were asked by the stakeholders. Also this project has helped me to revise and polish the knowledge of Advance Excel/ google sheets.

I have used techniques like **Advance formulas, filtering, sorting, vlookup, pivot table, charts etc**.
