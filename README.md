# ECE-2112-Pyton-Exploratory-Data-Analysis💻👨🏻‍💻🐍
--- 

## Table Of Contents

 ### ●   [Introduction](#Introduction)
 ### ●   [File Utilized](#File-Utilized)
 ### ●   [Guide Questions](#Guide-Questions)
 ### ●   [Results / Answers](#Results--Answers)
 ### ●   [References](#References)
 ### ●   [Conclusion](#Conclusion)
 
## Introduction
* In this repository, we will be utilizing the Spotify-2023 data file to further deepen the understanding and enhance the programmer's skills on their python coding whilst utilizing various libraries. These libraries include Pandas and Matplotlib to provide the readers with visuals and provide an easier-to-read data. 

## File Utilized
* The file utilized in this repository is the

> [spotify-2023.csv](https://github.com/user-attachments/files/17621217/spotify-2023.csv)

---
# Guide Questions 
In this repository, we will be answering the following questions : 

### 1. Overview of Dataset
How many rows and columns does the dataset contain?

What are the data types of each column? Are there any missing values?

### 2. Basic Descriptive Statistics
 What are the mean, median, and standard deviation of the streams column?

What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

### 3. Top Performers
Which track has the highest number of streams? Display the top 5 most streamed tracks.

Who are the top 5 most frequent artists based on the number of tracks in the dataset?

### 4. Temporal Trends
Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.

Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?

### 5. Genre and Music Characteristics
Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?

Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

###  6. Platform Popularity
How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?

###  7. Advanced Analysis
Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?

Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.

---

---
# Results / Answers
In this section, it will provide the readers what the coder observed during his task and his answers to the guide questions. Take note, there are some parts that have additional tasks, these additional tasks are based on what the coder observed in the Data Frame that provided additional tasks. 

## Accessing the Data

Before we start with answering our data, we must first access our files and import the necessary libraries.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("spotify-2023.csv",encoding = 'latin-1')

```
> The Pandas library will be used for creating and manipulating data frames

> The Numpy library will be used for numerical functions

> matplotlib and seaborn libraries will be used for creating charts and graphs for visualization

## Output   

![image](https://github.com/user-attachments/assets/d33b8cf4-cb6b-45d2-884b-2203b7735443)

* You will encounter an error upon first loading the data, in my case it was :
**'utf-8' codec can't decode bytes in position 7250-7251: invalid continuation byte'** . [It is a common error that occurs when trying to read a file with Pandas that cntains non-UTF-8 characters](https://saturncloud.io/blog/how-to-fix-the-pandas-unicodedecodeerror-utf8-codec-cant-decode-bytes-in-position-01-invalid-continuation-byte-error/#:~:text=continuation%20byte%20error%3F-,The%20UnicodeDecodeError%3A%20'utf%2D8'%20codec%20can't,%2DUTF%2D8%20encoded%20characters.). To eliminate the problem, we specify an encoding format, in which case I used Latin-1. Now the table can be seen without problem. 

---
## 1. Overview of Dataset

### How many rows and columns does the dataset contain?

```
size = df.shape # gets the shape of the data frame
print("the size of the data is: ", size) #outputs the size
```

### Output   
![image](https://github.com/user-attachments/assets/ce04d33e-970e-4120-873a-02783a156d4b)

* The command .shape provides us with the size or the shape of the data frame in which it results to our data frame being 953 rows and 24 columns.
---

## What are the data types of each column? Are there any missing values?

* **First, we will determine what are the data types of each column.**

### Determining the data types

```
datas = df.dtypes #gets the data type of each column
print("The Data types of each columns are: " ) #outputs the data types
datas
```
## Output 

![image](https://github.com/user-attachments/assets/4dd4ffec-b4a9-4dc3-8af9-5c19a409c329)

## Observation 
* It can be observed that some data types in the data frame are not what they should be. Example, streams, in_shazam_charts., and in_deezer_playlists are 'objects'. Compared to their related data, these should be in int as these could cause problems in our cleaning of data. So, it will now be converted into a numeric data type

## Converting of Data  (Additional task based on observation)
* Since some data types are not what they should be, we shall first convert before proceeding to the next question

```
df['streams'] = pd.to_numeric(df['streams'], errors='coerce') #converting streams into int
df['in_deezer_playlists'] = pd.to_numeric(df['in_deezer_playlists'], errors='coerce') #converting in_deezer_playlists
df['in_shazam_charts'] = df['in_shazam_charts'].astype(str).str.replace(',', '').astype(float) #converting in_shazam_charts to float
```

> To convert a Dataframe column into an integer, we use the code [` pd.to_numeric `](https://pandas.pydata.org/docs/reference/api/pandas.to_numeric.html)

> the [.astype()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html) function converts the data frame into desired data type.

> the [str.replace()](https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace.html) replaces the string into another character or whitespace the coder wants

* this codeblock converts the streams, and in_shazam_charts and in_deezer_playlists into a numeric data type meaning there should't be anymore problem in answering the remaining questions

---

##  Continuation : Are there any missing values?
* Second, we will check for any missing values in the Data Frame
```

No_value = df.isnull().sum() # to see which rows has how many missing values
print("These are the columns that have how many NaN values")
print(No_value[No_value>0]) # sets a parameter so that it only shows that has columns who has no values greater than 0

```
## Output

![image](https://github.com/user-attachments/assets/ec7f56a2-79bf-4839-964f-958a91bdf594)

> The .isnull() function is a boolean function that returns true when the data has no value.

* This code checks each columns how many NaN values they have. It can be seen that there is 1 in streams, 79  in in_deezer_playlists, 50 in in_shazam_charts and 95 in key

## Observation 
* It can be observed that in this code, it only checks for those that are null. But what if there are duplicates? The coder proceeded to find the duplicated data and remove it along with the Null values


## Finding Duplicated Datas (Additional task based on Observation)
  
```
# Finding duplicates of tracknames or artists
duplicate_value = df[df.duplicated(subset=['artist(s)_name','track_name'])] # checks for duplicates 
print("These are the rows that are duplicated")
duplicate_value # prints the rows that are duplicates
```
## Output

![image](https://github.com/user-attachments/assets/539a12e4-f05e-47e9-8fdb-7752ccfa704c)
> the [.duplicated()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html) function returns the duplicated rows

* This code checks the columns of artist(s)_name and track_name to see if there are any duplicated datas. It can be seen that the artists  ThxSoMch, The Weeknd, Lizzo, and Rosa Linn are the artists who duplicated.

### Removing the Duplicated and missing datas (Additional Task based on Observation)

*  Since we have identified the missing values and the duplicates , we will remove all the Duplicates and Missing Values in the Data frame

```
df_NaNValue = df.dropna(subset = ['track_name','in_shazam_charts','key','streams']) #drops the rows that have Null Values 

final_df = df_NaNValue.drop_duplicates(subset = ['track_name','artist(s)_name']) #removes duplicated rows

# sorts the values in a descending order so that the highest streams is first
final_df
sorted_final_df = final_df.sort_values(by = 'streams', ascending=False).reset_index(drop = True) 
final_df

```
> the [.dropna()](https://stackoverflow.com/questions/44548721/remove-row-with-null-value-from-pandas-data-frame) function removes the NaN values in the dataframe

> the [.drop_duplicates()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html) function removes the duplicates in the data frame

> the [.sort_values()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html) function sorts the values either in an ascending or descending order

 * in this block, it remove the null values in the track_name, in_shazam_charts, key, and streams. Furthermore, it also removed the duplicates in the data frame so that it can achieve a clean data frame which will be used for the questions to come. 


## 2. Basic Descriptive Statistics
### What are the mean, median, and standard deviation of the streams column?
```
average = final_df['streams'].mean()
median = final_df['streams'].median()
std = final_df['streams'].std()

print("The mean is: ", average)
print("The median is: ", median)
print("The standard deviation is: ", std)
```
* in this code block, we calculate for the mean, median and the standard deviation of the streams in the clean dataframe. 

## Output

![image](https://github.com/user-attachments/assets/9f4f4471-0040-443a-ab68-007975dd8ac5)

## Observation
* From the output it can be seen that our mean, median and standard deviation are 468922407.2521525, 263453310.0, and 523981505.32150424, respectively.

### What is the distribution of released_year and artist_count? 
```
# Histogram for artist_count
plt.figure(figsize=(10, 6)) #set graph size
sns.displot(final_df, x = 'artist_count', kde = True, discrete = True,aspect = 2) #inputting data for the histogram plot for released_years
plt.title("Distribution of Artist Count")  #setting a title
plt.xlabel("Artist count") #setting x label
plt.ylabel("Count") #setting y label
plt.show() #adding a grid to the plot

# histogram for released_year
years = final_df[final_df['released_year'] >= 2000]['released_year'] #setting a limit of released_year only greater than 2000
plt.figure(figsize=(10, 6)) # setting graph size
sns.displot(final_df, x = years, kde = True, discrete = True, aspect = 2) #inputting data for the histogram plot for released_years
plt.title('Distribution of Released Years') #setting a title
plt.xlabel("Released years") #setting x label
plt.ylabel("Count") #setting y label
plt.grid() #adding a grid to the plot
plt.show()
```
> the [sns.displot()](https://seaborn.pydata.org/generated/seaborn.displot.html) allows us to create a histogram graph
* To know the distribution of the released_year and artist_count, the coder utilized a displot or a histogram.
  
## Output

![image](https://github.com/user-attachments/assets/6e530908-df26-4d80-9258-73eb45d5c713)

![image](https://github.com/user-attachments/assets/b86b2088-e247-4a3d-860b-03fe756e5e85)

## Observation
* For the histogram on the Artist Count, it can be seen that the most popular ones are the ones whose tracks only have 1 artits. Whilst for the histogram for the released_year, it can be seen that most of the tracks that were released on the years 2020 to 2023

### Are there any noticeable trends or outliers?

```
def outlierfinder(final_df): #setting a user defined function to find outliers
    q1 = final_df.quantile(0.25) #setting 1st quartile
    q3 = final_df.quantile(0.75) #setting third quartile
    IQR = q3-q1 #formula for IQR
    outliers = final_df[((final_df<(q1-1.5*IQR)) | (final_df>(q3+1.5*IQR)))] #formula to find outliers in the data frame
    return outliers # returns the outlier

artistcount_outlier =  outlierfinder(final_df['artist_count']).shape[0] #finding outlier in the artist_count
print("Number of outliers in artist count is: ", artistcount_outlier) #outputs the number of outliers

yearoutlier = outlierfinder(final_df['released_year']).shape[0] #finding outlier in released_year
print("Number of outliers in released year is: ", yearoutlier) #outputs the number of outliers

```
> There are multiple ways to find outliers in a data, but in this codeblock, the coder utilized the [IQR method](https://www.analyticsvidhya.com/blog/2022/09/dealing-with-outliers-using-the-iqr-method/)

## Output

![image](https://github.com/user-attachments/assets/bcd34748-819a-4eff-a5ed-3aafc128f267)

## Observation
* The number of outliers in artist_count and released_year are 24 and 180 respectively. As seen in the histogram,  there are far greater counts in the released_year resulting from 2021 to 2023 which means there were more songs released in that duration compared to the previous years. In the artist count, it reveals how many artists produced one song. it can be seen in the histogram that the count is greater when only one artist produces a song. This could mean that some of outliers are located when the song produced is created by only one artist


## Top Performers

### Which track has the highest number of streams? Display the top 5 most streamed tracks.

```
higheststreams = final_df.sort_values(by = 'streams', ascending=False).reset_index(drop = True) #sorts the values by descending and resets the indexes 
higheststreams.head() #Displays the first 5 indexes
```
> the function [.rest_index()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html) resets the index of the data frame

## Output
![image](https://github.com/user-attachments/assets/0ba5563b-9667-4254-b600-b29ce3c3f272)

## Observation
* It can be seen that Ed Sheeran's song "Shape of You" has the highest streams followed by Sunflower by Post Malone, Swae Lee, One Dance by Drake, WizKid, Kyla	, Stay by  Justin Bieber, The Kid Laroi, and Believer by Imagine Dragons.

### Who are the top 5 most frequent artists based on the number of tracks in the dataset?
```
artist_split = final_df['artist(s)_name'].str.split(', ') # since theyre separated by a comma
artist_unique = artist_split.explode() #turns the list into an array
topartists = artist_unique.value_counts() # counts how many times the artist is seen
topartists.head()
```

> The function [.explode()](https://www.w3schools.com/php/func_string_explode.asp#:~:text=The%20explode()%20function%20breaks,cannot%20be%20an%20empty%20string.) converts the string into an array

> The function [.value_counts()](https://pandas.pydata.org/docs/reference/api/pandas.Series.value_counts.html) counts the unique values in the array.

## Output

![image](https://github.com/user-attachments/assets/547ce664-82e5-42ef-bee9-d148fdaed4ed)

## Observation
* As seen in the results, the artist that frequently appears the most is Bad Bunny followed by Tayor Swift, The Weeknd, Kendtrick Lamar, and Feid.


## Temporal Trends
Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.

```
tracksperyear = final_df.groupby('released_year').size().reset_index(name = 'track_count')

plt.figure(figsize=(10, 6))
sns.lineplot(data = tracksperyear, x = 'released_year', y = 'track_count')
plt.grid()
plt.xlabel("Year Released")
plt.ylabel("Tracks released")
plt.title("Tracks released per year")
plt.show()

trackspermonth = final_df.groupby('released_month').size().reset_index(name = 'track_count', )
plt.figure(figsize=(10, 6))
sns.barplot(data = trackspermonth,x = 'released_month',y = 'track_count',width = .8,color = 'green')
plt.grid()
plt.title("tracks released per month")
plt.xlabel("Month Released")
plt.ylabel("Number of tracks")
plt.show()
```

> The [DataFrame.groupby()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) function groups the dataframe into a series of columns.


## Output
![image](https://github.com/user-attachments/assets/b45f4d44-27c2-4a1a-bc77-43c5a9b8ad45)

![image](https://github.com/user-attachments/assets/6047f002-ab02-4441-9d45-ba9ab1267000)


## Observation
* It can be seen in the graph that in the year 2020 and above has more tracks released. On the bar graph for tracks per month, it can be seen that most of the songs were released on January or on May.


## Genre and Music Characteristics

### Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?

```
dataneeded = final_df[['streams','bpm','danceability_%', 'valence_%', 'energy_%', 'acousticness_%', 'instrumentalness_%','liveness_%','speechiness_%'  ]] 
correlation_matrix = dataneeded.corr() # https://www.geeksforgeeks.org/python-pandas-dataframe-corr/ # computes for the correlation
plt.figure(figsize=(12, 6))
sns.heatmap(correlation_matrix, annot=True, linewidths=.8, cmap = 'Oranges')
plt.title("Correlation using Heatmap")
plt.show()

```
> The [.corr()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html) function computes for the correlation of the dataframe

## Output 

![image](https://github.com/user-attachments/assets/91cae5b0-fb09-41f5-87c1-9539ade5d06d)

## Observation
* It can be seen that is a correlation in the valence and danceability and valence and energy. This could mean that alot of listeners prefer their songs on which has a good energy, can make choreographies, and a positive type of song.


 ### Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

 ## Observation
 *  based on the heatmap, For the correlation between danceability_% and energy_%? there is a low positive correlation whilst for valence_% and acousticness_%? there is a low negative correlation.


---

## Platform Popularity

### How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?

```
playlists = [
    final_df['in_spotify_playlists'].sum(), 
    final_df['in_apple_playlists'].sum(), 
    final_df['in_deezer_playlists'].sum()
] #creating a list for the sum of all tracks in each playlist
print("The number of tracks in Spotify, Apple, and Deezer are: " ,playlists, "respectively") #outputs the number
platform = ['Spotify Playlist', 'Apple Playlist', 'Deezer Playlist'] #creates a list for the x axis
plt.figure(figsize=(15, 6)) #sets the plot size
sns.barplot(x = platform, y = playlists, color = 'green') #creates a bar plot
plt.grid() #sets a grid
plt.title("Platform Popularity") #sets title
plt.show() #shows plot


```
## Output

![image](https://github.com/user-attachments/assets/8f656b05-e420-4323-8c0d-cdaeb85facc6)

## Observation
* From the plot, it can be seen that there are more tracks in spotify. Followed by deezer then apple. Furthermore, the number of tracks in each playlist are 3943504, 48719, 69618 respectively.


## Advanced Analysis

### Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?

```
keystreams = final_df.groupby(['key'])['streams'].sum().reset_index() #groups the sum of streams by their keys.
keystreams = keystreams.sort_values(by = 'streams', ascending = False) #sorts the value from greatest to least
plt.figure(figsize=(15, 6)) # sets the size of the plot
plt.bar(keystreams['key'], keystreams['streams'], color = 'green') # sets a bargraph
plt.grid() #sets a grid
plt.xlabel("Keys") #labels the x axis
plt.ylabel("average streams") #labels the y axis
plt.title(" Number of streams per key (major and minor)") #sets a title
plt.show() #shows the graph
```
* In this codeblock, it sets up a bar graph to identify how many streams are in each key, the modes, major and minor, are added together in their respective keys.

## Output

![image](https://github.com/user-attachments/assets/75abe281-bc78-4ad1-992b-38e2878452db)

## Observation
* in the bar graph, It can be seen that most of the songs are in C#. Take note, both modes are in the same key. The highest is followed by D, F, G, G#, B, E F#, A#, A, and D#.


### Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.

```
#splits the string of each column whose parameter is ', ' 
artist_split = final_df['artist(s)_name'].str.split(', ') 

exploded_artists = artist_split.explode().reset_index(drop=True) #converts the string into an array

artist_unique = final_df[['in_apple_playlists', 'in_spotify_playlists', 'in_deezer_playlists']].copy()  # Include playlist columns
artist_unique['Artists'] = exploded_artists # creates a new column Artists
artist_unique['Artists'] = artist_unique['Artists'].str.strip() # removes any spaces

# groups the individual artist by their respective playlist
artists_playlist = artist_unique.groupby('Artists')[['in_apple_playlists', 'in_spotify_playlists', 'in_deezer_playlists']].sum()


artists_playlist = artists_playlist.reset_index() # Resets the index

#computes for the total playlist count of the 3 playlist and adds to a new column
artists_playlist['Total Playlists'] = artists_playlist[['in_apple_playlists', 'in_spotify_playlists', 'in_deezer_playlists']].sum(axis=1)

#sorts by ascending o=rder
artists_playlist_sorted = artists_playlist.sort_values(by='Total Playlists', ascending=False) #sorts be descending
artisttop10_playlist = artists_playlist_sorted.head(10) # Displays the first 10 indexes



#plotting the artists in the top 10 of the playlist summary
plt.figure(figsize=(15, 6)) #sets the plot size
plt.grid() #adds a grid
plt.bar(artisttop10_playlist['Artists'], artisttop10_playlist['Total Playlists'], color='green') #creates a bar graph
plt.xlabel("Top 10 Artists") # labels the x axis
plt.ylabel("Playlist count") #labels the y axis
plt.title("Total Playlist Count of Artists") #sets the title
plt.show() #shows the graph

```
> The [.str.strip()](https://www.w3schools.com/python/ref_string_strip.asp) function removes all spaces in the string.
> The [.copy()](https://www.w3schools.com/python/ref_list_copy.asp) function copies the list

* This code outputs a bargraph of the total playlist of the individual artist in the clean data frame.

```
#splitting the artists which are grouped
artist_split = final_df['artist(s)_name'].str.split(', ')

#breaking the string into an array
exploded_artists = artist_split.explode().reset_index(drop=True)

#copying the dataframe from the clean dataframe 
artist_unique = final_df[['in_apple_charts', 'in_spotify_charts', 'in_deezer_charts','in_shazam_charts']].copy()  # Include playlist columns

#Assigning the arrayed artists into a column
artist_unique['Artists'] = exploded_artists
#removing white spaces from the columns
artist_unique['Artists'] = artist_unique['Artists'].str.strip()

#grouping the aritst by their respective charts
artists_charts = artist_unique.groupby('Artists')[['in_apple_charts', 'in_spotify_charts', 'in_deezer_charts','in_shazam_charts']].sum()
#reseting the index of the charts as it outputs "['Artists'] not in index"
artists_charts = artists_charts.reset_index()
#computing the sum of the 3 charts of each artist into a new column[total charts]
artists_charts['Total Charts'] = artists_charts[['in_apple_charts', 'in_spotify_charts', 'in_deezer_charts','in_shazam_charts']].sum(axis=1)

#creating a data frame for the artist and their total charts
artistscharts = artists_charts[['Artists', 'Total Charts']]
#sorting the charts by descending to analyze who has the most. Reseting the index so i
artistscharts_sorted = artistscharts.sort_values(by=['Total Charts'], ascending=False).reset_index(drop=True)
artisttop10_charts= artistscharts_sorted.head(10)

#plotting the artists in the top 10 of the charts
plt.figure(figsize=(15, 6))
plt.grid()
plt.bar(artisttop10_charts['Artists'], artisttop10_charts['Total Charts'], color='green')
plt.xlabel("Top 10 Artists")
plt.ylabel("Charts count")
plt.title("Total Charts Count of Artists")
plt.show()
```
* This code outputs a bargraph of the total chart count of the individual artist in the clean data frame.

## Output

![image](https://github.com/user-attachments/assets/e86f93d0-32b3-42a8-8fd7-fa3329a03cab)

![image](https://github.com/user-attachments/assets/e804807d-6d6e-4d1c-bf9c-1c9df55cb28c)

### Observation
* In the first bar graph, the graph for the total playlist of each individual artist, it can be seen that The Weeknd has the most playlist count of all artists, followed by Taylor Swift, SZA, Bad Bunny, Grupo frontera, Eminem, Travis Scott, Metro boomin, and Junior H. While for the second Bar graph, the bargraph for the total charts of individual artists, Taylor Swift has the most charts followed by The Weeknd, Peso Pluma, Feid, Bad Bunny, Junior H, Yng Lvcas, Bizarrap, Sza, and Quevedo.

 ## Conclusion
 * To conclude this repository, the coder provided Insights and Suggestions for fellow peers planning to try this data frame for themselves.

### Insights
* During my coding process, I've encountered many problems such as null values in the data frame and the duplicates. I removed them as they could deter me from the results I want to achieve. Additionally, during my time here, I've noticed that there are so many functions that I've barely known before but now understand. I encourage the fellow readers to try this data frame and try to answer the guide questions as they have helped me significantly in deepening my understanding with python and helped me learn more functions.
  
### Suggestion
1.)  When creating a clean data frame, check each columns if there are any null values as these could make your code not work
2.) Check the data types as you could run into erros when computing for integers as object data types cannot be used to compute.
3.) For a more cleaner code, the other coders may opt to use a separate notebook for the clean dataframe. There, they could start their coding without confusion or messy codes. 
4.) Always add comments, especially when the code being done is a long process as these could help you recall what to do when you return again.




## Update Log
In this section, the coder provided Updates about the coding process and Versions of the ReadMe file to provide transparency to the readers of the Repository

#### Update 1.0 (10/31/2024)
* Cleaning of the dataframe in Jupyter, removing duplicates, null values, and changing of data types.
* Upon cleaning the data sheet, coder observes NaN values in the data.
* Some datatypes, such as stream, are 'object' which needs to be an integer or a float. This can be a problem when solving other questions such as mean as 'object' cannot be used to compute. 

#### Version 1.0 (10/31/2024)
 * Initial input in Github ReadMe (Guide questions and some drafts)

#### Update 1.1 (11/1/2024)
* Further adjustments and addition in the Jupyter Notebook Codes 

#### Version 1.1 (11/1/2024)
* Minor Adjustments and additions in ReadMe file

####  Update 1.2 (11/5/2024)
* Completion of coding, can still be changed if needed
  
####  Version 1.2 (11/5/2024)
* Input of results from the Jupyter Notebook codes
* Adjustment and additions to the ReadMe File

####  Version 1.3 (11/5/2024)
* Addition to the readme file

#### Update 1.4 (11/6/2024)
* Completion of the coding process

####  Version 1.4 (11/6/2024)
* Completion of the documentation and ReadMe file

## References
1. https://saturncloud.io/blog/how-to-fix-the-pandas-unicodedecodeerror-utf8-codec-cant-decode-bytes-in-position-01-invalid-continuation-byte-error/#:~:text=continuation%20byte%20error%3F-,The%20UnicodeDecodeError%3A%20'utf%2D8'%20codec%20can't,%2DUTF%2D8%20encoded%20characters.
2. https://stackoverflow.com/questions/22216076/unicodedecodeerror-utf8-codec-cant-decode-byte-0xa5-in-position-0-invalid-s
3. https://pandas.pydata.org/docs/reference/api/pandas.to_numeric.html
4. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.astype.html
5. https://pandas.pydata.org/docs/reference/api/pandas.Series.str.replace.html
6. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html
7. https://stackoverflow.com/questions/44548721/remove-row-with-null-value-from-pandas-data-frame
8. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html
9. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html
10. https://www.analyticsvidhya.com/blog/2022/09/dealing-with-outliers-using-the-iqr-method/
11. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html
12. https://www.w3schools.com/php/func_string_explode.asp#:~:text=The%20explode()%20function%20breaks,cannot%20be%20an%20empty%20string.
13. https://pandas.pydata.org/docs/reference/api/pandas.Series.value_counts.html
14. https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html
15. https://www.w3schools.com/python/ref_string_strip.asp
16. https://www.w3schools.com/python/ref_list_copy.asp




