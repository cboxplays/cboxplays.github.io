---
title: IMDB Movies
date: 2022-12-05 10:30:00 -500
categories: [Projects, Data Analysis]
tags: [advance excel]     # TAG names should always be lowercase
---

## Project Description
We have an extensive dataset about the IMDB ratings of the movies. Using that data we are supposed to find the answers to the questions of stakeholders. We should use statistical and analytical skills to get to the result.

## Approach
While starting with the project I looked into the data and how the columns in the dataset are structured. After I checked if the database had the required data to find the solutions for the asked questions.

Second step was to clean the data and make it usable to get accurate results.

## Tech-Stack Used
* Google sheets - For presenting tables and visualization
* Google Docs - For report

## Insights

### Cleaning the data

As a part of data cleaning, I removed the records with the ‘Blank’ cells. I thought this approach is better because the sample size is large enough and there were few blank records.

Alternative could be to try to find missing values and make data more accurate but that seems inefficient.

Note : Following file has all the sheets that have been used in the analysis including different sheets for cleaned data.

https://docs.google.com/spreadsheets/d/1c7OmIH1L_94LeeneXl9c9NWyEoQ_0cOltpTbOuuH4NQ/edit?usp=sharing


### Movies with highest profit

The task was to visualize the graph of Budget vs Profit and we observed some **outliers** in that visualization. In the first chart I have highlighted the outliers in blue and the other chart is after removing the outliers to get a good perspective over data.

<iframe width="686" height="393" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTHfA9itXHFxFYK4EUTIyRYHsTrt3fv3sk3VhoPMKUYZi3HC-zVKWUosRtxGvERUBLhHSPJxyspU9dp/pubchart?oid=926940593&amp;format=interactive"></iframe>

**After removing outliers :**

<iframe width="686" height="393" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTHfA9itXHFxFYK4EUTIyRYHsTrt3fv3sk3VhoPMKUYZi3HC-zVKWUosRtxGvERUBLhHSPJxyspU9dp/pubchart?oid=363679035&amp;format=interactive"></iframe>

After removing the outliers we can observe that the **average movie bears the losses**, we can go into a deeper layer to analyze why it is so.

### Top 250

#### top 10 movies from top 250 of all time

| Rank | movie_title                                   | num_voted_users | language | imdb_score |
| ---- | --------------------------------------------- | --------------- | -------- | ---------- |
| 1    | The Shawshank Redemption                      | 1689764         | English  | 9.3        |
| 2    | The Godfather                                 | 1155770         | English  | 9.2        |
| 3    | The Dark Knight                               | 1676169         | English  | 9          |
| 4    | The Godfather: Part II                        | 790926          | English  | 9          |
| 5    | Pulp Fiction                                  | 1324680         | English  | 8.9        |
| 6    | Schindler's List                              | 865020          | English  | 8.9        |
| 7    | The Good, the Bad and the Ugly                | 503509          | Italian  | 8.9        |
| 8    | The Lord of the Rings: The Return of the King | 1215718         | English  | 8.9        |
| 9    | Fight Club                                    | 1347461         | English  | 8.8        |
| 10   | Forrest Gump                                  | 1251222         | English  | 8.8        |

#### Top 10 Foreign language Films

| Rank | movie_title                    | num_voted_users | language   | imdb_score |
| ---- | ------------------------------ | --------------- | ---------- | ---------- |
| 1    | The Good, the Bad and the Ugly | 503509          | Italian    | 8.9        |
| 2    | City of God                    | 533200          | Portuguese | 8.7        |
| 3    | Seven Samurai                  | 229012          | Japanese   | 8.7        |
| 4    | Spirited Away                  | 417971          | Japanese   | 8.6        |
| 5    | The Lives of Others            | 259379          | German     | 8.5        |
| 6    | Children of Heaven             | 27882           | Persian    | 8.5        |
| 7    | Amélie                         | 534262          | French     | 8.4        |
| 8    | Baahubali: The Beginning       | 62756           | Telugu     | 8.4        |
| 9    | Princess Mononoke              | 221552          | Japanese   | 8.4        |
| 10   | Das Boot                       | 168203          | German     | 8.4        |

### Best Directors

Following are the **top 10 directors with respect to average IMDB ratings**.

| Rank | Director              | Average IMDB rating |
| ---- | --------------------- | ------------------- |
| 1    | Charles Chaplin       | 8.6                 |
| 2    | Tony Kaye             | 8.6                 |
| 3    | Alfred Hitchcock      | 8.5                 |
| 4    | Damien Chazelle       | 8.5                 |
| 5    | Majid Majidi          | 8.5                 |
| 6    | Ron Fricke            | 8.5                 |
| 7    | Sergio Leone          | 8.43                |
| 8    | Christopher Nolan     | 8.42                |
| 9    | Asghar Farhadi        | 8.4                 |
| 10   | Marius A. Markevicius | 8.4                 |

### Popular Genres

#### Following are the popular genres with respect to average IMDB rating.

| Rank | Genre       | Average IMDB rating |
| ---- | ----------- | ------------------- |
| 1    | Biography   | 7.15                |
| 2    | Crime       | 6.94                |
| 3    | Documentary | 6.92                |
| 4    | Drama       | 6.82                |
| 5    | Western     | 6.77                |

#### Following are the popular genres with respect to number of movies in percent.

| Rank | Genre     | Number of movies in percent |
| ---- | --------- | --------------------------- |
| 1    | Comedy    | 26.69%                      |
| 2    | Action    | 24.99%                      |
| 3    | Drama     | 17.99%                      |
| 4    | Adventure | 9.74%                       |
| 5    | Crime     | 6.67%                       |

### Charts

Our task was to check the critic reviews and user reviews and find the **‘Mean’** of them. The mean represents which actor is critically acclaimed as well as approved by the masses.

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vTHfA9itXHFxFYK4EUTIyRYHsTrt3fv3sk3VhoPMKUYZi3HC-zVKWUosRtxGvERUBLhHSPJxyspU9dp/pubchart?oid=1138073479&amp;format=interactive"></iframe>

According to the results we can safely say that **Leonardo DiCaprio is the highest rated** amongst Leonardo DiCaprio, Brad Pitt and Meryl Streep.

## Results
I was able to find the data driven solutions for all the questions that were asked by the stakeholders. Also this project has helped me to revise and polish the knowledge of Advance Excel/ google sheets.

I have used techniques like **Advance formulas, filtering, sorting, vlookup, pivot table, charts etc.**

Also used **statistical tools such as Mean, mode, etc.**
