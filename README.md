Apache Beam Project Report
Changes I made in this lab assignment

I added several improvements to make this pipeline richer and more meaningful.
Here is what I changed and expanded:

I used the MovieLens ratings dataset and processed two CSV files together

I calculated the average rating and rating count for every movie

I kept only movies that have at least fifty ratings so the results reflect popular movies

I added a new field called rating band that groups movies into high, medium, and low based on their average rating

I created genre-level statistics by computing the average rating and number of rated movies for each genre

I generated a third output file that shows the top ten genres with the highest average ratings

I produced three separate output files for movie summaries, genre summaries, and the top ten genres

I used Apache Beam's Mean and Count combiners for the calculations

I expanded the pipeline to handle list-based fields like movie genres by exploding and recombining them

These changes make the pipeline more complete, realistic, and easier to analyze.

Overview

This project uses Apache Beam to build a small data pipeline that processes the MovieLens small dataset.
The goal is to compute rating summaries for movies and genres and to enrich the data with some additional insights.

The dataset contains two CSV files:

movies.csv containing movie details and genre information

ratings.csv containing user ratings for each movie

The pipeline reads both files, cleans the data, computes statistics, and writes the results into an output folder.

What the pipeline does
Reading and parsing

The pipeline reads the movies and ratings CSV files

Each line is parsed into a structured dictionary

Movies contain a movie ID, title, and a list of genres

Ratings contain a user ID, movie ID, rating value, and timestamp

Computing movie statistics

The pipeline computes the average rating for each movie

It counts how many ratings each movie received

These values are joined with the movie metadata so each movie has full information

Filtering and adding rating band

Only movies with at least fifty ratings are kept

This avoids movies with unreliable averages

A new field called rating band is added

high for movies with a rating of 4.0 or higher

medium for movies with ratings between 3.0 and 3.99

low for movies with a rating below 3.0

Computing genre statistics

Each movie can have multiple genres

The pipeline expands the list of genres into separate records

It then computes:

the average rating for each genre

the number of popular movies that contributed to that genre

Top ten genres

The pipeline identifies the top ten genres with the highest average rating

This is done using Apache Beam’s Top combiner

Output files

The pipeline generates three output files inside the output folder:

movie_rating_summary.txt
Contains movie title, genres, average rating, rating count, and rating band

genre_rating_summary.txt
Contains the average rating and number of rated movies for each genre

top10_genres_by_rating.txt
Contains the ten genres with the highest average rating

Each line in these files is a small dictionary showing the computed values.
