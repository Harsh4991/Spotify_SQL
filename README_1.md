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
   ``` sql
select 
  track ,
  stream  
  from spotify
  where stream> 1000000000
order by stream;
   ```
3. List all albums along with their respective artists.
4. Get the total number of comments for tracks where `licensed = TRUE`.
5. Find all tracks that belong to the album type `single`.
6. Count the total number of tracks by each artist.
7. Calculate the average danceability of tracks in each album.
8. Find the top 5 tracks with the highest energy values.
9. List all tracks along with their views and likes where `official_video = TRUE`.
10. For each album, calculate the total views of all associated tracks.
11. Retrieve the track names that have been streamed on Spotify more than YouTube.
12. Find the top 3 most-viewed tracks for each artist using window functions.
13. Write a query to find tracks where the liveness score is above the average.
14. calculate the difference between the highest and lowest energy values for tracks in each album.**
15. Find tracks where the energy-to-liveness ratio is greater than 1.2.
16. Calculate the cumulative sum of likes for tracks ordered by the number of views, using window functions.
---

## Next Steps
- **Visualize the Data**: Use a data visualization tool like **Tableau** or **Power BI** to create dashboards based on the query results.
- **Expand Dataset**: Add more rows to the dataset for broader analysis and scalability testing.
---

