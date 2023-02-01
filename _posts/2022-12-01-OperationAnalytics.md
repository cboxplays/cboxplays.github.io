---
title: Operation Analytics and Investigating Metric Spike
date: 2022-12-01 10:30:00 -500
categories: [Projects, Data Analysis]
tags: [sql, excel]     # TAG names should always be lowercase
---
# Case Study 1 (Job Data)

## Project Description
It has a data regarding jobs and we need to analyze the data and find the answers that were asked by the stakeholders.

## Approach
While starting with the project I looked into the data and how the tables in databases are related to each other. After I checked if the database had the required data to find the solutions for the asked questions.

## Tech-Stack Used
* MySQL Workbench 8.0 - For analysis
* Google Docs - For report
* Google sheets - For presenting tables and visualization

## Insights
### Number of jobs reviewed
**Job reviewed per hour : 0.056**

**Job reviewed per day : 1.333**

| per_day | per_hour |
| ------- | -------- |
| 1.333 | 0.056 |

```sql
select 
  round(sum(id_count)/count(ds), 3) as per_day,
  round((sum(id_count)/count(ds))/24, 3) as per_hour
from
  (select
    ds,
    count(job_id) as id_count
  from
    job_data
  group by
    ds) a;
```
### Throughput
We first checked the daily job processed for the week, then we calculated rolling average for the week.

**Average jobs processed in a week : 1.3333/day**

| date       | rolling_avg |
| ---------- | ----------- |
| 2020-11-25 | 1           |
| 2020-11-26 | 1           |
| 2020-11-27 | 1           |
| 2020-11-28 | 1.25        |
| 2020-11-29 | 1.2         |
| 2020-11-30 | 1.3333      |

```sql
select
  date(ds) as date,
  avg(job_count) over (order by date(ds) rows between unbounded preceding and 0 following) as rolling_avg
from
  (select
    ds,
    count(job_id) as job_count
  from
    job_data
  group by
    ds) a
group by
  ds;
```
### Percentage share of each language
First we calculated the total jobs, then we cross joined it with the job_data table.

From this table we calculated the percentage share of each language.

**Language with highest percentage share : Persian(37.50%)**

| language | percent |
| -------- | ------- |
| Persian  | 37.50%  |
| English  | 12.50%  |
| Arabic   | 12.50%  |
| Hindi    | 12.50%  |
| French   | 12.50%  |
| Italian  | 12.50%  |

```sql
select
  language,
  concat(round((count(job_id)*100)/total_jobs, 2), '%')  as percent
from
  job_data
cross join
(select
  count(job_id) as total_jobs
from
  job_data) a
group by
  language
order by
  2 desc;
```

### Duplicate rows
We counted job_id using GROUP BY clause. If the id count is more than 1, that id is duplicate.

**job_id 23 is repeated 3 times in the table.**

| job_id | duplicates |
| -------- | ------- |
| 23  | 3  |

```sql
select
  job_id, count(job_id) as duplicates
from
  job_data
group by
  job_id
having duplicates > 1;
```
# Case Study 2 (Investigating metric spike)

## Project Description
We have three tables that provide us with data about the engagement of the users. We need to find the insights from given data.

## Approach
While starting with the project I looked into the data and how the tables in databases are related to each other. After I checked if the database had the required data to find the solutions for the asked questions.

## Tech-Stack Used
* BigQuery - For loading the data and analysis
* Google Docs - For report
* Google sheets - For presenting tables and visualization

## Insights
### User Engagement
First we calculated the active users for every week.

Then we calculated the average active use per week.

**User engagement for the product is 177/week.**

| total_active_users | total_weeks | active_user_per_week |
| ------------------ | ----------- | -------------------- |
| 9381               | 53          | 177                  |

```sql
select
  sum(active_users) as total_active_users,
  count(weeks) as total_weeks,
  round(sum(active_users)/count(weeks), 2) as active_user_per_week
from
  (select
    extract(week FROM activated_at) as weeks,
    count(*) as active_users
  from
    `dataanalysiscapstone.Investigating_Metric_Spike.users`
  where
    activated_at is not null
  group by weeks
  order by weeks) a
```

### User Growth
First we calculated a new user count for every month.

From that data we calculated the user growth by using rolling sum.

Then we calculated the growth in percentage for every month.

| month   | user_growth | growth_percentage |
| ------- | ----------- | ----------------- |
| 1/2013  | 332         | -              |
| 2/2013  | 660         | 33.06%            |
| 3/2013  | 1043        | 22.49%            |
| 4/2013  | 1453        | 16.43%            |
| 5/2013  | 1939        | 14.33%            |
| 6/2013  | 2424        | 11.12%            |
| 7/2013  | 3032        | 11.14%            |
| 8/2013  | 3668        | 9.49%             |
| 9/2013  | 4367        | 8.70%             |
| 10/2013 | 5193        | 8.64%             |
| 11/2013 | 6009        | 7.28%             |
| 12/2013 | 6981        | 7.48%             |
| 1/2014  | 8064        | 7.20%             |
| 2/2014  | 9118        | 6.13%             |
| 3/2014  | 10349       | 6.32%             |
| 4/2014  | 11768       | 6.42%             |
| 5/2014  | 13365       | 6.35%             |
| 6/2014  | 15093       | 6.07%             |
| 7/2014  | 17076       | 6.16%             |
| 8/2014  | 19066       | 5.51%             |

```sql
select
  month, final_table.user_growth, if(user_growth_per=100, "-", concat(round(user_growth_per, 2), '%')) as growth_percentage
from
  (select
    month, user_growth,
    user_count*100/sum(user_growth) over(order by user_growth rows between 1 preceding and 0 following) as user_growth_per
  from
    (select
    concat(a.month, "/",a.year) as month,
    sum(user_count) over(rows between unbounded preceding and 0 following) as user_growth,
    user_count
    from
      (select
        extract(month FROM created_at) as month,
        extract(year FROM created_at) as year,
        count(*) as user_count
      from
        `dataanalysiscapstone.Investigating_Metric_Spike.users`
      group by
        year, month) a)
  order by user_growth) final_table
```

### Weekly retention
First we find out the latest activity for every user.

We right joined the users table to calculate if the difference between the latest activity of the user and user’s activation date is more than 7 days.

Then we calculated the user who stuck around more than 7 days in percent with respect to all active users as retention_percent.

**User retention of the product is 73.55%**

| retention_percent |
| ----------------- |
| 73.55% |

```sql
select
  concat(round((user_count*100)/total, 2), '%') as retention_percent
from
  (select
    *, sum(calc.user_count) over() as total
  from
    (select
      count(users.user_id) as user_count, if(date_diff(occurred_at, activated_at, day)<7, "less", "more") as flag
    from
      `dataanalysiscapstone.Investigating_Metric_Spike.users` as users
    right join
      (select
      user_id, occurred_at
    from
      (select
        rank() over(partition by user_id order by occurred_at desc) as event_rank, user_id, occurred_at
      from
        `dataanalysiscapstone.Investigating_Metric_Spike.events`) a
      where a.event_rank=1) events
  on events.user_id = users.user_id
  where users.state = 'active'
  group by flag) calc)
Where flag ='more'
```

### Weekly Engagement
First we calculated the number of users who used the device every week for every device.

From that data we calculated the Weekly user engagement for every device.

**Device with highest retention : macbook pro**

**Device with lowest retention : samsumg galaxy tablet**
*data in the table has spelling mistake*

| rank | device                 | weekly_retention |
| ---- | ---------------------- | ---------------- |
| 1    | macbook pro            | 3155.16          |
| 2    | lenovo thinkpad        | 2035.74          |
| 3    | macbook air            | 1479.16          |
| 4    | iphone 5               | 1428.11          |
| 5    | dell inspiron notebook | 1077.68          |
| 6    | samsung galaxy s4      | 1031.26          |
| 7    | nexus 5                | 907.84           |
| 8    | iphone 5s              | 879.21           |
| 9    | dell inspiron desktop  | 556.26           |
| 10   | iphone 4s              | 531.42           |
| 11   | asus chromebook        | 527.05           |
| 12   | ipad air               | 526              |
| 13   | acer aspire notebook   | 493.26           |
| 14   | hp pavilion desktop    | 488.42           |
| 15   | nexus 7                | 362.89           |
| 16   | ipad mini              | 310.26           |
| 17   | nokia lumia 635        | 309.47           |
| 18   | nexus 10               | 286.63           |
| 19   | acer aspire desktop    | 284.32           |
| 20   | mac mini               | 243.26           |
| 21   | htc one                | 236.05           |
| 22   | kindle fire            | 225.26           |
| 23   | windows surface        | 193.32           |
| 24   | samsung galaxy note    | 148.47           |
| 25   | amazon fire phone      | 120.95           |
| 26   | samsumg galaxy tablet  | 106.67           |

```sql
select
  ROW_NUMBER() over (order by round(b.total_users/ b.total_weeks, 2) desc) as rank_count,
  b.device,
  round(b.total_users/ b.total_weeks, 2) as weekly_retention
From
(select
  distinct device,
  sum(a.user_count) over (partition by device order by weeks, user_count rows between unbounded preceding and unbounded following) as total_users,
  count(weeks) over (partition by device order by weeks, user_count rows between unbounded preceding and unbounded following) as total_weeks
from
  (select
    device, extract(week from occurred_at) as weeks, count(user_id) as user_count
  from
    `dataanalysiscapstone.Investigating_Metric_Spike.events`
  group by
    device, weeks) a) b
order by 1
```

### Email Engagement
First we calculated the action count by actions for every user.

From that data we found the average action count by user for every action.

From this data we conclude that, if we send a weekly digest to 16 people, 6 people will open the mail and 3 people will click on the link in the mail.

| action             | avg_count |
| ------------------ | --------- |
| sent_weekly_digest | 16        |
| email_open         | 6         |
| email_clickthrough | 3         |

```sql
with user_data as(
  select
    count(*) as user_count
  from
    `dataanalysiscapstone.Investigating_Metric_Spike.users`
)
select
  action, ceiling(sum(action_count)/count(user_data.user_count)) as avg_count
from
  (select
    action, 
    count(*) over (partition by action, user_id order by action, user_id rows between unbounded preceding and unbounded following) as action_count
  from
    `dataanalysiscapstone.Investigating_Metric_Spike.email_events`) a, user_data
where action != 'sent_reengagement_email'
group by action
order by 2 desc
```
# Results
I was able to find the **data driven solutions** for all the questions that were asked by the stakeholders. Also this project has helped me to revise and polish the knowledge of **SQL**.

I have used **Advance SQL** techniques like **Join, Nested queries, Functions, etc**.