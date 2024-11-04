# Exploratory-Data-Analysis
--- 

## Table Of Contents
 ### ●  [Introduction](#Introduction)
 ### ●  [File Utilized](#File-Utilized)
 ### ●  [Guide Questions](#Guide-Questions)
 ### ●  [Answers](#Results--Answers)
 ### ●  [References](#References)

### Introduction
* In this repository, we will be utilizing the Spotify-2023 data file to further deepen the understanding and enhance the programmer's skills on their python coding whilst utilizing various libraries. These libraries include Pandas and Matplotlib to provide the readers with visuals and provide an easier-to-read data. 

### File Utilized
* The file utilized in this repository is the
[spotify-2023.csv](https://github.com/user-attachments/files/17621217/spotify-2023.csv)


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

#### Accessing the Data

Before we start with answering our data, we must first access our files.

```python
df = pd.read_csv("spotify-2023.csv",encoding = 'latin-1')

```
![image](https://github.com/user-attachments/assets/d33b8cf4-cb6b-45d2-884b-2203b7735443)
 
You will encounter an error upon first loading the data, in my case it was :
**'utf-8' codec can't decode bytes in position 7250-7251: invalid continuation byte'** . [It is a common error that occurs when trying to read a file with Pandas that cntains non-UTF-8 characters](https://saturncloud.io/blog/how-to-fix-the-pandas-unicodedecodeerror-utf8-codec-cant-decode-bytes-in-position-01-invalid-continuation-byte-error/#:~:text=continuation%20byte%20error%3F-,The%20UnicodeDecodeError%3A%20'utf%2D8'%20codec%20can't,%2DUTF%2D8%20encoded%20characters.). To counter eliminate the problem, we specify an encoding format, in which case I used Latin-1. Now the table can be seen without problem. 

## Update Log
In this section, the coder provided updates about certain observations or changes during his process in cleaning and coding the dataframe. 

##### Observation during the cleaning process
* Upon cleaning the data sheet, it can be observed that there are multiple NaN values.
* Some datatypes, such as stream, are 'object' which needs to be an integer or a float. This can be a problem when solving other questions such as mean as 'object' cannot be used to compute. 

#### Version 1.0 (10/31/2024)
 * Initial input in Github ReadMe
 * Cleaning of the dataframe in Jupyter, removing duplicates and null values.

#### Version 1.1 (11/1/2024)
* Further adjustments and addition in the Jupyter Notebook Codes 
* Minor Adjustments and additions in ReadMe file

#### Update 1.0 (11/2/2024)
* Further additions and adjustments to the Jupyter Notebook Codes

####  Version 1.2 (11/2/2024)


## References
1. https://saturncloud.io/blog/how-to-fix-the-pandas-unicodedecodeerror-utf8-codec-cant-decode-bytes-in-position-01-invalid-continuation-byte-error/#:~:text=continuation%20byte%20error%3F-,The%20UnicodeDecodeError%3A%20'utf%2D8'%20codec%20can't,%2DUTF%2D8%20encoded%20characters.
2. https://stackoverflow.com/questions/22216076/unicodedecodeerror-utf8-codec-cant-decode-byte-0xa5-in-position-0-invalid-s
3. https://www.geeksforgeeks.org/convert-a-dataframe-column-to-integer-in-pandas/
4. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html


