# Spotify Advanced SQL Project 
[Click Here to get Dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset)


## Overview
This project involves analyzing a Spotify dataset with various attributes about tracks, albums, and artists using **SQL**. It covers an end-to-end process of normalizing a denormalized dataset, performing SQL queries. The primary goal of the project is to practice advanced SQL skills and generate valuable insights from the dataset.

```sql
-- create table
DROP TABLE IF EXISTS spotify;
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);
```
## Project Steps

###  Data Exploration
Before diving into SQL, it’s important to understand the dataset thoroughly. The dataset contains attributes such as:
- `Artist`: The performer of the track.
- `Track`: The name of the song.
- `Album`: The album to which the track belongs.
- `Album_type`: The type of album (e.g., single or album).
- Various metrics such as `danceability`, `energy`, `loudness`, `tempo`, and more.

###  Querying the Data
After the data is inserted, various SQL queries can be written to explore and analyze the data. 
  ---

## 15 Practice Questions

1. Retrieve the names of all tracks that have more than 1 billion streams.
```sql
select 
track ,stream  
from spotify
where stream> 1000000000
order by stream;
```
 
2. List all albums along with their respective artists.
```sql
select 
distinct album,
artist 
from spotify
order by 1;
```
   
3. Get the total number of comments for tracks where `licensed = TRUE`.
```sql
select track,comments,licensed from spotify
where licensed ='True' ;

select sum(comments) as total_comments
from spotify 
where licensed = 'True';
```   
4. Find all tracks that belong to the album type `single`.
```sql
select
album_type,track
from spotify
where album_type = 'single';
```     
5. Count the total number of tracks by each artist.
```sql
select artist,
count(track) as no_of_tracks 
from spotify
group by artist;
```    
6. Calculate the average danceability of tracks in each album.
```sql
select track,
avg(danceability) as avg_danceability
from spotify
group by track;
```

7. Find the top 5 tracks with the highest energy values.
```sql
select 
track,max(energy)
from spotify
group by 1
order by 2 desc
limit 5;
```
8. List all tracks along with their views and likes where `official_video = TRUE`.
```sql
select 
track,
sum(views) as total_views,
sum(likes) as total_likes
from spotify
where official_video = 'True'
group by 1
order by 2 desc
limit 5;
```

9. For each album, calculate the total views of all associated tracks.
```sql
select album,track,
sum(views) as total_views
from spotify
group by 1,2
order by 3 desc
```

10. Retrieve the track names that have been streamed on Spotify more than YouTube.
```sql
select * from 
(select track,
--most_played_on,
COALESCE(SUM(CASE WHEN most_played_on = 'Spotify' THEN stream END),0) as most_played_spotify,
COALESCE(SUM(CASE WHEN most_played_on = 'Youtube' THEN stream END),0) as most_played_youtube
from spotify
GROUP BY 1
) as t1
where most_played_spotify > most_played_youtube
AND
most_played_youtube <> 0
```

11. Find the top 3 most-viewed tracks for each artist using window functions.
```sql
WITH CTE AS (
select artist,track,
sum(views) as total_views,
DENSE_RANK() OVER (PARTITION BY artist ORDER BY sum(views) desc) as RANK
from spotify
group by 1,2
order by 1,3 desc
)
select * from cte 
where rank <= 3;
```

12. Write a query to find tracks where the liveness score is above the average.
```sql
select track,
artist,
liveness 
from spotify 
where liveness > (select avg(liveness) from spotify)
```

13. calculate the difference between the highest and lowest energy values for tracks in each album.**
```sql
WITH CTE AS
(
select  album,
max(energy) as highest_energy,
min(energy) as lowest_energy
from spotify
group by 1
)
select album,
highest_energy - lowest_energy as energy_diff
from cte 
order by 2 desc
```
    
14. Find tracks where the energy-to-liveness ratio is greater than 1.2.
```sql
select track,energy_liveness
from spotify
where energy_liveness > 1.2
order by 2 desc
```

15. Calculate the cumulative sum of likes for tracks ordered by the number of views, using window functions.
```sql
select track,
sum(likes) as sum_of_likes,
views,
DENSE_RANK() OVER (PARTITION BY track ORDER BY views desc) as RANK
from spotify
group by 1,3
order by 2 desc
```

---

## Next Steps
- **Visualize the Data**: Use a data visualization tool like **Tableau** or **Power BI** to create dashboards based on the query results.
- **Expand Dataset**: Add more rows to the dataset for broader analysis and scalability testing.
---

