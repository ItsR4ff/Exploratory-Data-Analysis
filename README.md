# Exploratory-Data-Analysis
--- 

## Table Of Contents

 ### ●   [Introduction](#Introduction)
 ### ●   [File Utilized](#File-Utilized)
 ### ●   [Guide Questions](#Guide-Questions)
 ### ●   [Results / Answers](#Results--Answers)
 ### ●   [References](#References)

## Introduction
* In this repository, we will be utilizing the Spotify-2023 data file to further deepen the understanding and enhance the programmer's skills on their python coding whilst utilizing various libraries. These libraries include Pandas and Matplotlib to provide the readers with visuals and provide an easier-to-read data. 

## File Utilized
* The file utilized in this repository is the

> [spotify-2023.csv](https://github.com/user-attachments/files/17621217/spotify-2023.csv)

---
# Guide Questions 
In this repository, we will be answering the following questions : 

### 1. Overview of Dataset
1.1 How many rows and columns does the dataset contain?

1.2 What are the data types of each column? Are there any missing values?

### 2. Basic Descriptive Statistics
2.1 What are the mean, median, and standard deviation of the streams column?

2.2 What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

### 3. Top Performers
3.1 Which track has the highest number of streams? Display the top 5 most streamed tracks.
3.2 Who are the top 5 most frequent artists based on the number of tracks in the dataset?

### 4. Temporal Trends
4.1 Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
4.2 Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?

### 5. Genre and Music Characteristics
5.1 Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
5.2 Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

###  6. Platform Popularity
6.1 How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?

###  7. Advanced Analysis
**7.1** Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?

7.2 Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.

---

---
# Results / Answers
In this section, it will provide answers with in-depth explanations for our guide questions to further explain the observations in the problems. 

## Accessing the Data

Before we start with answering our data, we must first access our files and import the necessary libraries.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("spotify-2023.csv",encoding = 'latin-1')

```
## Output   

![image](https://github.com/user-attachments/assets/d33b8cf4-cb6b-45d2-884b-2203b7735443)

* You will encounter an error upon first loading the data, in my case it was :
**'utf-8' codec can't decode bytes in position 7250-7251: invalid continuation byte'** . [It is a common error that occurs when trying to read a file with Pandas that cntains non-UTF-8 characters](https://saturncloud.io/blog/how-to-fix-the-pandas-unicodedecodeerror-utf8-codec-cant-decode-bytes-in-position-01-invalid-continuation-byte-error/#:~:text=continuation%20byte%20error%3F-,The%20UnicodeDecodeError%3A%20'utf%2D8'%20codec%20can't,%2DUTF%2D8%20encoded%20characters.). To eliminate the problem, we specify an encoding format, in which case I used Latin-1. Now the table can be seen without problem. 

---
# 1.) Overview of Dataset
## 1.1.)How many rows and columns does the dataset contain?

```
size = df.shape
print("the size of the data is: ", size)
```

## Output   
![image](https://github.com/user-attachments/assets/ce04d33e-970e-4120-873a-02783a156d4b)

* The command .shape provides us with the size or the shape of the data frame in which it results to our data frame being 953 rows and 24 columns.
---

### What are the data types of each column? Are there any missing values?

First, we will determine what are the data types of each column.

## Determining the data types

```
datas = df.dtypes
print("The Data types of each columns are: " )
datas
```
## Output 

![image](https://github.com/user-attachments/assets/4dd4ffec-b4a9-4dc3-8af9-5c19a409c329)

* It can be observed that some data types in the data frame are not what they should be. Example, streams, in_shazam_charts., and in_deezer_playlists are 'objects'. Compared to their related data, these should be in int as these could cause problems in our cleaning of data.
  
---


---
## Cleaning of Data Set (Additional Task)

* To answer next guide questions, the coder cleaned his data to avoid problems in the data frame and avoid future issues whilst answering the remaining questions.

#### Converting the into numerical data
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

###  Are there any missing values?

#### Finding the total number of missing values
```
No_value = df.isnull().sum() # to see which rows has how many missing values
print("These are the columns that have how many NaN values")
print(No_value[No_value>0])
```
## OUTPUT 
![image](https://github.com/user-attachments/assets/ec7f56a2-79bf-4839-964f-958a91bdf594)

> The .isnull() function is a boolean function that returns true when the data has no value. 
* This code checks each columns how many NaN values they have. It can be seen that there is 1 in streams, 79  in in_deezer_playlists, 50 in in_shazam_charts and 95 in key

#### Finding Duplicated Datas

```
duplicate_value = df[df.duplicated(subset=['artist(s)_name','track_name'])] 
print("These are the rows that are duplicated")
duplicate_value 
```
![image](https://github.com/user-attachments/assets/539a12e4-f05e-47e9-8fdb-7752ccfa704c)
> the [.duplicated()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html) function returns the duplicated rows
* This code checks the columns of artist(s)_name and track_name to see if there are any duplicated datas. It can be seen that the artists  ThxSoMch, The Weeknd, Lizzo, and Rosa Linn are the artists who duplicated.

##### Removing the Duplicated and missing datas

```
df_NaNValue = df.dropna(subset = ['track_name','in_shazam_charts','key','streams'])  # source : https://stackoverflow.com/questions/44548721/remove-row-with-null-value-from-pandas-data-frame
# this code removes the rows that have NaN values
# Now lets remove duplicates, if there are any.
final_df = df_NaNValue.drop_duplicates(subset = ['track_name','artist(s)_name']) # https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html
sorted_final_df = final_df.sort_values(by = 'streams', ascending=False).reset_index(drop = True) # this also sorts the values in a descending order so that the highest streams is first
final_df
```
> the [.dropna()](https://stackoverflow.com/questions/44548721/remove-row-with-null-value-from-pandas-data-frame) function removes the NaN values in the dataframe

> the [.drop_duplicates()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html) function removes the duplicates in the data frame

> the [.sort_values()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html) function sorts the values either in an ascending or descending order

 * in this block, it remove the null values in the track_name, in_shazam_charts, key, and streams. Furthermore, it also removed the duplicates in the data frame so that it can achieve a clean data frame which will be used for the questions to come. 


## Basic Descriptive Statistics
### What are the mean, median, and standard deviation of the streams column?
```
average = final_df['streams'].mean()
median = final_df['streams'].median()
std = final_df['streams'].std()

print("The mean is: ", average)
print("The median is: ", median)
print("The standard deviation is: ", std)
```

* in this code block, we calculate for the mean, median and the standard deviation of the streams in the clean dataframe. our mean, median and standard deviation are 468922407.2521525, 263453310.0, and 523981505.32150424, respectively.

### What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?
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
  
## OUTPUT

![image](https://github.com/user-attachments/assets/6e530908-df26-4d80-9258-73eb45d5c713)

![image](https://github.com/user-attachments/assets/b86b2088-e247-4a3d-860b-03fe756e5e85)



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

![image](https://github.com/user-attachments/assets/bcd34748-819a-4eff-a5ed-3aafc128f267)


* The number of outliers in artist_count and released_year are 24 and 180 respectively. As seen in the histogram,  there are far greater counts in the released_year resulting from 2021 to 2023 which means there were more songs released in that duration compared to the previous years. In the artist count, it reveals how many artists produced one song. it can be seen in the histogram that the count is greater when only one artist produces a song. This could mean that some of outliers are located when the song produced is created by only one artist


## Top Performers

### Which track has the highest number of streams? Display the top 5 most streamed tracks.

```
higheststreams = final_df.sort_values(by = 'streams', ascending=False).reset_index(drop = True) #sorts the values by descending and resets the indexes 
higheststreams.head() #Displays the first 5 indexes
```
> the function [.rest_index()](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html) resets the index of the data frame

## OUTPUT
![image](https://github.com/user-attachments/assets/0ba5563b-9667-4254-b600-b29ce3c3f272)

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

## OUTPUT

![image](https://github.com/user-attachments/assets/547ce664-82e5-42ef-bee9-d148fdaed4ed)


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


## OUTPUT
![image](https://github.com/user-attachments/assets/b45f4d44-27c2-4a1a-bc77-43c5a9b8ad45)

![image](https://github.com/user-attachments/assets/6047f002-ab02-4441-9d45-ba9ab1267000)


* It can be seen in the graph that in the year 2020 and above has more tracks released. It can be seen between the year 2021 and 2022 has the highest number of tracks released. 

---

## Update Log
In this section, the coder provided updates about the coding process and versions of the ReadMe file to provide transparency to the readers of the Repository


#### Version 1.0 (10/31/2024)
 * Initial input in Github ReadMe (Guide questions and some drafts)

#### Update 1.0 (10/31/2024)
* Cleaning of the dataframe in Jupyter, removing duplicates, null values, and changing of data types.
* Upon cleaning the data sheet, coder observes NaN values in the data.
* Some datatypes, such as stream, are 'object' which needs to be an integer or a float. This can be a problem when solving other questions such as mean as 'object' cannot be used to compute. 

#### Version 1.1 (11/1/2024)
* Minor Adjustments and additions in ReadMe file

#### Update 1.1 (11/1/2024)
* Further adjustments and addition in the Jupyter Notebook Codes 

####  Version 1.2 (11/5/2024)
* Input of results from the Jupyter Notebook codes
* Adjustment and additions to the ReadMe File

####  Update 1.2 (11/5/2024)
* Completion of coding, can still be changed if needed

####  Version 1.3 (11/5/2024)
* Addition to the readme file


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


