# Exploratory-Data-Analysis
--- 

## Table Of Contents
 * Introduction
 * Guide Questions
 * Results / Answers
 * References 





### Guide Questions
In this repository, we will be answering the following questions : 
#### Overview of Dataset
* How many rows and columns does the dataset contain?
* What are the data types of each column? Are there any missing values?

#### Basic Descriptive Statistics
* What are the mean, median, and standard deviation of the streams column?
* What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

#### Top Performers
* Which track has the highest number of streams? Display the top 5 most streamed tracks.
* Who are the top 5 most frequent artists based on the number of tracks in the dataset?

#### Temporal Trends
* Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
* Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?
#### Genre and Music Characteristics
* Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
* Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

####  Platform Popularity
* How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?
####  Advanced Analysis
* Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
* Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.

### Results / Answers
In this section, it will provide answers with in-depth explanations for our guide questions to further explain the observations in the problems. 


## Update Log
In this section, the coder provided updates about certain observations or changes during his process in cleaning and coding the dataframe. 

##### Observation during the cleaning process
* Upon cleaning the data sheet, it can be observed that there are multiple NaN values.
* Some datatypes, such as stream, are 'object' which needs to be an integer or a float. This can be a problem when solving other questions such as mean as 'object' cannot be used to compute. 

#### Version 1.0 (10/31/2024)
 * Initial input in Github ReadMe
 * Cleaning of the dataframe in Jupyter, removing duplicates and null values.

#### Version 1.1 (11/1/2024)
* Further adjustments and addition in the dataset file
* Minor Adjustments and additions in ReadMe file


## References
1. https://stackoverflow.com/questions/22216076/unicodedecodeerror-utf8-codec-cant-decode-byte-0xa5-in-position-0-invalid-s
2. https://www.geeksforgeeks.org/convert-a-dataframe-column-to-integer-in-pandas/
3. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html


