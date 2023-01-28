---
title: Instagram User Analysis
date: 2022-11-07 10:30:00 -500
categories: [Project, DataAnalysis]
tags: [sql, excel]     # TAG names should always be lowercase
---
## Project Description
In this project, the product team of Instagram wants to have insights for the launch of a new marketing campaign, decide on features to build for an app, track the success of the app by measuring user engagement and improve the experience altogether while helping the business grow.

## Approach
While starting with the project I looked into the data and how the tables in databases are related to each other. After I checked if the database had the required data to find the solutions for the asked questions.

## Tech-Stack Used
* MySQL Workbench 8.0 - For analysis
* Google Docs - For report
* Google sheets - For presenting tables and visualization

## Insights
### Rewarding Most Loyal Users
We checked for the **oldest users**

| ranks | id | username         |
| ---- | -- | ---------------- |
| 1    | 80 | Darby_Herzog     |
| 2    | 67 | Emilio_Bernier52 |
| 3    | 63 | Elenor88         |
| 4    | 95 | Nicole71         |
| 5    | 38 | Jordyn.Jacobson2 |

```sql
select ROW_NUMBER() OVER(ORDER BY created_at) ranks, id, username
from users
order by created_at
limit 5;
```

### Remind Inactive Users to Start Posting
We checked users who haven’t posted a single photo.

Following IDs are **inactive**, we can **remind** them.

| id | username            |
| -- | ------------------- |
| 5  | Aniya_Hackett       |
| 7  | Kasandra_Homenick   |
| 14 | Jaclyn81            |
| 21 | Rocio33             |
| 24 | Maxwell.Halvorson   |
| 25 | Tierra.Trantow      |
| 34 | Pearl7              |
| 36 | Ollie_Ledner37      |
| 41 | Mckenna17           |
| 45 | David.Osinski47     |
| 49 | Morgan.Kassulke     |
| 53 | Linnea59            |
| 54 | Duane60             |
| 57 | Julien_Schmidt      |
| 66 | Mike.Auer39         |
| 68 | Franco_Keebler64    |
| 71 | Nia_Haag            |
| 74 | Hulda.Macejkovic    |
| 75 | Leslie67            |
| 76 | Janelle.Nikolaus81  |
| 80 | Darby_Herzog        |
| 81 | Esther.Zulauf61     |
| 83 | Bartholome.Bernhard |
| 89 | Jessyca_West        |
| 90 | Esmeralda.Mraz57    |
| 91 | Bethany20           |

```sql
select users.id, users.username
from users
left join photos
on users.id = photos.user_id
where photos.id is null
order by users.id;
```
### Declaring Contest Winner
We checked photos with the highest like count.

With **48 likes** on photo the winner is **Harley_Lind18**.

| user_id | username      | photo_id | image_url           | likes_count |
| ------- | ------------- | -------- | ------------------- | ----------- |
| 3       | Harley_Lind18 | 145      | https://jarret.name | 48          |

```sql
select likes.user_id, users.username, likes.photo_id, photos.image_url, count(photo_id) as likes_count
from likes 
inner join users
on users.id = likes.user_id
inner join photos
on photos.id = likes.photo_id
group by photo_id
order by likes_count desc
limit 1;
```
### Hashtag Researching
We checked for the most used hashtag.

Following are the **most used hashtags** ranked by the count.

| ranks | tag_name | tag_id | tag_count |
| ---- | -------- | ------ | --------- |
| 1    | smile    | 21     | 59        |
| 2    | beach    | 20     | 42        |
| 3    | party    | 17     | 39        |
| 4    | fun      | 13     | 38        |
| 5    | concert  | 18     | 24        |

```sql
select ROW_NUMBER() OVER(ORDER BY created_at) ranks, tags.tag_name, tag_id, count(tag_id) as tag_count
from photo_tags
inner join tags on tags.id = photo_tags.tag_id
group by tag_id
order by tag_count desc
limit 5;
```

### Launch AD Campaign
We checked on which day of the week Instagram is getting most registrations.

We can see that **Thursday and Sunday** have the **highest registration count**, so we can choose the date accordingly.

| ranks | day       | registration_count |
| ---- | --------- | ------------------ |
| 1    | Thursday  | 16                 |
| 2    | Sunday    | 16                 |
| 3    | Friday    | 15                 |
| 4    | Tuesday   | 14                 |
| 5    | Monday    | 14                 |
| 6    | Wednesday | 13                 |
| 7    | Saturday  | 12                 |

```sql
select ROW_NUMBER() OVER(ORDER BY created_at) ranks, dayname(created_at) as day, count(*) as registration_count
from users
group by day
order by registration_count desc
```

### User Engagement
We checked the average post count by the users.

According to analysis, the **average posts per user are Three**.

| total_photos | total_users | averge_posts_per_user |
| ------------ | ----------- | --------------------- |
| 283          | 100         | 3                     |

```sql
select count(*) as total_photos, count(distinct users.id) as total_users, ceil(count(*) /count(distinct users.id)) as averge_posts_per_user
from photos
right join users on photos.user_id = users.id;
```

### Bots & Fake Accounts
We checked users who have liked every photo on the application.

There are a **total 257 posts** on the application and the following **list of users** have **liked all of them**.

| username           | likes_count |
| ------------------ | ----------- |
| Aniya_Hackett      | 257         |
| Bethany20          | 257         |
| Duane60            | 257         |
| Jaclyn81           | 257         |
| Janelle.Nikolaus81 | 257         |
| Julien_Schmidt     | 257         |
| Leslie67           | 257         |
| Maxwell.Halvorson  | 257         |
| Mckenna17          | 257         |
| Mike.Auer39        | 257         |
| Nia_Haag           | 257         |
| Ollie_Ledner37     | 257         |
| Rocio33            | 257         |

```sql
select username, count(*) as likes_count
from users
inner join likes on users.id = likes.user_id
group by users.username
having likes_count = (select Count(*) from photos);
```
## Results
I was able to find the **data driven solutions** for all the questions that were asked by the stakeholders. Also this project has helped me to revise and polish the knowledge of **SQL**.

I have used **Advance SQL** techniques like **Join, Nested queries, Functions, etc**.