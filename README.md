# Movies and Series SQL Analysis

A hands-on SQL project that analyzes the Netflix Movies and TV Shows dataset (about 8,800 titles). I built it while learning SQL step by step: every new concept was used on real data to answer a real question.

## Dataset

- Source: "Netflix Movies and TV Shows" dataset from Kaggle (CSV)
- Main table: `netflix_titles`
- Columns: `show_id`, `type`, `title`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description`
- Extra tables I created: `rating_groups` (maps each rating to an audience group) and a numeric column `duration_values`

## Tools

- SQLite
- DB Browser for SQLite
- GitHub

## Project files

| File | What it covers |
|------|----------------|
| `01_explore.sql` | SELECT, WHERE, ORDER BY, LIMIT, LIKE |
| `02_summarize.sql` | COUNT, GROUP BY, HAVING, DISTINCT, NULL checks |
| `03_cleaning.sql` | UPDATE, COALESCE, fixing wrong values |
| `04_duration.sql` | ALTER TABLE, CAST, REPLACE, CASE |
| `05_joins.sql` | CREATE TABLE, INSERT, JOIN, LEFT JOIN |
| `06_subqueries_cte.sql` | Subqueries, CTEs (WITH) |

## Data cleaning notes

- **Shifted values:** 3 rows had the duration (for example "66 min") stored in the `rating` column. I moved them into `duration` and set the rating to NULL.
- **Missing ratings:** 7 titles have no rating. A plain JOIN drops them, a LEFT JOIN keeps them, so I used LEFT JOIN when the totals had to be complete.
- **Duration is text:** values like "90 min" and "2 Seasons" cannot be averaged. I created a numeric column `duration_values`.
- **Different units:** movies are measured in minutes and TV shows in seasons, so I never average them together. Length analysis uses `WHERE type = 'Movie'`.
- **Rating groups:** I created a lookup table `rating_groups` to group ratings into Kids, Family, Teens, Adults and Unrated.

## Key findings

- The dataset has 6,131 movies. By length: 1,841 short (under 90 min), 3,148 medium (90 to 120 min) and 1,142 long (over 120 min).
- The average movie length is about 99.6 minutes. 2,922 movies are longer than the average.
- TV-MA is the most common rating (3,207 titles). Adults is the largest audience group.
- Teens (PG-13 and TV-14) have the longest average movie length.
- Movies from 2003 have the longest average length of all years with at least 50 movies: 116.3 minutes (51 movies). 2004 follows with 114.3 minutes and 2005 with 113.9 minutes.
- Grey's Anatomy is the TV show with the most seasons.

## SQL skills used

SELECT, WHERE, ORDER BY, LIMIT, LIKE, DISTINCT, COUNT, AVG, ROUND, GROUP BY, HAVING, IS NULL, COALESCE, NULLIF, UPDATE, ALTER TABLE, CAST, REPLACE, CASE, CREATE TABLE, INSERT, PRIMARY KEY, JOIN, LEFT JOIN, subqueries, CTEs

## Next steps

- Window functions: ranking (ROW_NUMBER, RANK) and running totals
- Dates: analyze when titles were added (`date_added`)
- Split the multi-value columns (`listed_in`, `country`, `cast`) into separate tables
- Many-to-many joins: genres, countries and actors
- Views for the most useful queries
- Final summary of insights

## How to reproduce

1. Download the Netflix titles CSV from Kaggle.
2. Open DB Browser for SQLite, create a new database and import the CSV as the table `netflix_titles`.
3. Run the SQL files in order, from `01_explore.sql` to the latest file.
