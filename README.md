Apache Beam Project Report
Changes I made in this lab assignment

I added several improvements to make this pipeline richer and more meaningful.
Here is what I changed and expanded

I used the MovieLens ratings dataset and processed two CSV files together

I calculated the average rating and rating count for every movie

I kept only movies that have at least fifty ratings so the results reflect popular movies

I added a new field called rating band that groups movies into high medium and low based on their average rating

I created genre level statistics by computing the average rating and number of rated movies for each genre

I generated a final file that shows the top ten genres with the highest average ratings

I produced three separate output files for movie summaries genre summaries and the top ten genres

I used Apache Beam combiners Mean and Count for all calculations

I expanded the pipeline to handle list based fields like movie genres by exploding and recombining them

These changes make the pipeline more complete realistic and easier to analyze.

Overview

This project uses Apache Beam to build a small data pipeline that processes the MovieLens small dataset.
The goal is to compute rating summaries for movies and genres and to enrich the data with some additional insights.

The dataset contains two CSV files

movies.csv with movie details and genre information

ratings.csv with user ratings for each movie

The pipeline reads both files cleans the data computes statistics and writes the results into an output folder.

What the pipeline does
Reading and parsing

The pipeline reads the movies and ratings CSV files.
Each line is parsed into a structured dictionary.
Movies have a movie ID title and a list of genres.
Ratings have a user ID movie ID rating value and a timestamp.

Computing movie statistics

The pipeline computes the average rating for each movie.
It also counts how many ratings each movie received.
These two values are joined with the movie metadata so each movie has its full information.

Filtering and adding rating band

Only movies with at least fifty ratings are kept.
This avoids movies with unreliable averages.
A rating band is added to each movie

high if the rating is four point zero or higher

medium if the rating is between three and three point nine nine

low if the rating is below three

Computing genre statistics

Each movie can have multiple genres.
The pipeline breaks this into one record per genre.
It then computes the average rating for each genre and how many movies contributed to it.

Top ten genres

A small additional step identifies the top ten genres with the highest average rating.
This is done using Beam’s Top combiner.

Output files

The pipeline generates three output files inside the output folder

movie rating summary with movie title genres average rating rating count and rating band

genre rating summary with the average rating and number of rated movies for each genre

top ten genres by average rating

Each line in these files is a dictionary showing the computed values.