# Data Analysis & Statistical Hypothesis testing for Jawwy TV

> This work points & Analysis is the author opinions and doesn't speak for anybody.

## Overview of JawwyTV IPTV
Firstly who's JawwyTV ? It's a platform where STC host movies / TV shows on this platform.
Maybe 2 years prior JawwyTV shared a portion of the data they have about the users activity on the website in public. Even though those data doesn't violate any privacy for the users. The dataset in csv format with 3 Million records of different things like name of the movie / TV show or the duration each user have been watching certain series. Those records between the year 2017 to 2018. In the end JawwyTV now an old name, Rightnow they goes by "STC TV".

## plan of attack

We'll go with pure data analysis with pandas and manipulation if needed.
The steps will be:
- Check memory consumption(since DF is ~300MB)
- Inspect & clean for NaNs
- Parse dates 
- Optimization of DataFrame
- Inspect and Getting insights on unknown columns
- Manipulate data values such as: drop duplicates, change column names, get to know which quantiative & Qualitative.

Then after the data analysis we'll do some "Statistical Analysis":
- Standard deviation
- Confidence interval
- Compute T-test & Set a Hypothesis
- Compute Chi-square test

In the end we'll perform EDA(Exploratory Data Analysis):
- Percentage of HD Vs. SD resolution.
- Most popular Genres in (Movie & TV Show)
- Most Watched Movie & TV Show
- Does people tend to watch more on Weekends ?

## Data analysis

### Check memory allocation
- Memory usage are HUGE.
- No. Of Rows : 3.598.607
- Columns Data Types:
    - 1 of datetime obj
    - 6 int numbers
    - 5 objects (strings)

### Optimization of DataFrame approach
We need to optimze this as much as possible!

One way to drop columns that have no significant meaning or convert the dtype to something more efficient.
- like objects ==> category

Note: If you need to convert something to category THE MOST IMPORTANT THING to look out is to make the column doesn't contain ANY NaNs.

---
#### After Optimization
Nice! we can see here we optimized the Dataframe By = ~20%

From ~300MB to ~260MB. 

That's a good amount for a DataFrame of 3M rows!

### Unknown genres
After inspecting the DataFrame and trying to drive insights from it. Firstly, I need to get to know those attributes and what they mean in the 
Dataset like "SERIES_NOT_ADDED_UNDER_ANY_GENRE" & "NOT_DEFINED_IN_UMS"

After checking the values and compare it with each other here's the information I got to derive

Keypoints for "SERIES_NOT_ADDED_UNDER_ANY_GENRE" Genre:

- It seems for the genre — "SERIES_NOT_ADDED_UNDER_ANY_GENRE" due to some reason Jawwy TV interpret some Series/Episodes as "SERIES_NOT_ADDED_UNDER_ANY_GENRE".
- ONLY from the program_class of Series/Episodes.
- Sums up to 838 Series/Episodes only.
- Only 4% of the WHOLE Series/Episodes have the genre of "SERIES_NOT_ADDED_UNDER_ANY_GENRE"


Keypoints for "NOT_DEFINED_IN_UMS" Genre:
- Like the above Jawway TV interpreted the 2 movies which are[Dunkirk, Batman Unlimited: Animal Instincts] as this genre.
- ONLY from the program_class of "MOVIE" belong to this genre.
- Sums up to 11775 Movies.
- The Percentage of those movies belong to this genre to the whole are 77%.

So After inspecting these two columns I decided to merge it together into one value called "Others"


### Getting insights from Quantitaive columns

Keypoints for quantitaive [hd, season, episode, series_title, duration_seconds]:
- For hd:
    - hd feature only have 1 which indicates the movie / tv show have hd resolution otherwise 0 it doesn't have one.
    - hd for higher / lower resolution the percentages goes like: 36% / 63% respectively.
    - There's no indicators for 4k, FHD and so on ... maybe it's the old version of Jawwy tv. or that's how they're referenced in the dataset for 4k it gives it 1 other than 4k it goes by 0.


- For season:
    - Only applicaple for Movies, For TV Shows there's no season obviously but just wanna make sure. Because some sites call it "sequel" instead of season.
    - Nearly ~2 Million Movie that have more than one season.

- For episode:
    - The range of episodes between 0 — 282. whether it's a movie or one episode of a TV Show.
    - The Average episodes that the users had been watched is ~7 episodes. But that's not the case if there's an outlier.
    - The median for this feature is 1. that means there's an outlier it seems normal because not everyone watches only a single movie. Some people maybe binge watching some TV Shows out there. Another possibility is people who falls asleep during watch along parties and such a thing could be a disastrous for database records. Why is that ? because the feature of "auto play" to next episode or recommendation to another and the user is sleeping that will keep the system to auto record every single activity as long as the user are sleeping....ZzZ.
    - Most popular number for episode the user watches are 0. Which means he either watches a movie or one episode of a TV Show.

- For series_title:
     - for series_title = 1, Only TV Show have this value And for series_title = 0 have both TV Show & Movie. So i put a hypothesis maybe it's an indicator for "ONE" title and "TWO" title respectivly. But after inspecting more I was proved wrong because there's some rows in series_title of 0 have only ONE title. So the format that i imagined inside my head are like this (Original Movie/epsiode title + the episode name).

- For duration_seconds:
    - It seems like the number of seconds someone watching the episode of a movie or TV show.
    - What's interesting is the duration of seconds some users have like = 2053603 Seconds which equals to ~570 Hours🔴which are a lot of time for watching a movie. But it seems to have some feature for cumulative recording mechanism because there's no movie with 570 hours long.
    - For cumulative part I inspected some other movies of this user(30881) and i found that movie named "Emoji Movie" which have 2 reconds at the same day even though the time is unknown because Jawwy doesn't record in their. But that's interesting how they separate those records ? is it by some specific duration ? or by logging out / log in again ?.
    - Another possibility of those huge durations of time the same as "Auto play" for next episode but this like a loop for the same episode.

### Inspecting for duplicates
After inspecting the entire DataFrame i got this:

Number of Duplicates: 397.883

Percentage of duplicates to the whole DF: 11.06%


### Data Attributes information

After inspecting all columns and getting the information needed I made this part came in later part of the analysis part not like the usual which is First step for most of the data science project that I saw. Because I feel more comfortable when writing those information after thorough analysis.

Data Attributes Information:

Name — Data Type(Pandas) — Data Type(Statistic term) — Description
- date — datetime object — Quantitative — Values 2017-03-14 / 2018-04-30 indicates users activity in Jawwy TV database.
- user_id — integer object — Quantitative — contains of user_id not unique the user may get duplicated (E.g. user 1 may get 20 movie watching).
- program_name — pandas object — Qualitative — The movie or TV Show name episode.
- duration_seconds — integer object — Quantitative — Duration of a single user watching Movies/TV shows.
- program_type — pandas object — Quantitative — Whether a user watched a Movie or TV Show.
- season — integer object — Quantitative — indicates a user watched one season(0) indexed in DataFrame. Or 1 and more.
- episode — integer object — Quantitative — Indicates a user how many episodes he/she watched.
- program_desc — pandas object — Qualitative — A small description for a Movie/TV Show.
- program_genre — pandas category object — Qualitative — Types of genre of the Movie / TV Show. whether it's Drama, Sci-Fi, etc..
- series_title — integer object — Quantitative — A binary indicator of 0, 1. it's UNKNOWN for me untill now what those mean.
- hd — integer object — Quantitative — A binary indicator for resolution whether 1 HD or 0 SD resolution.
- original_name — pandas category —  Qualitative — Name of the Movie / TV Show. Unlike "program_name" which may contain the episode name and NOT the *original* series name.


*Ok that's enough of data analysis and manipulation for now!*


## Exploratory Data Analysis & Statistical Hypothesis Testing

We'll start with statistical analysis

### Standard deviation
Measures the variation or dispersion of a set of values.

In simple words, High values mean higher variability.

Bigger than the mean(average) ==> Higher variation.

Testing the column (duration_seconds)
Mean = 1177.635590382612
STD = 6231.966899676256

>We can see here that the values dispersed, Which means there are users who watches a lot of movies / TV Shows. (Probably Binge watching)


### Confidence interval

A range that gives a sense of how precisely a statistic estimates a parameter.

In simple words, It'll give you a notion of how much the parameter or coefficient vary. 


Lets test couple of columns:
- season.
- episodes.

#### Confidence interval on "Season"

```python
print(df[["season"]].mean())
st.norm.interval(alpha=0.95,
                 loc=df["season"].mean(),
                 scale=st.sem(df["season"]))
```
season    1.426785
dtype: float64
(1.4245705358900655, 1.4289997483893793)

Lower bound = 1.4245705358900655
Upper bound = 1.4289997483893793

>We can see that the lower bound + upper bound of season mean with a Confidence interval of 95%.

Lets visualize it with histogram

!["hist_of_ci"](asset/season_hist.png)

---
#### Confidence interval on "episodes"

```Python
# Confidence interval of the episode mean
print(df[["episode"]].mean())
st.norm.interval(alpha=0.95,
                 loc=df["episode"].mean(),
                 scale=st.sem(df["episode"]))
```

episode    7.028602
dtype: float64
(7.01470446475272, 7.042499892377691)

Lower bound = 7.01470446475272
Upper bound = 7.042499892377691

!["hist_of_ep"](asset/episode_hist.png)

---
### T-test

It helps us understand whether one group is "Statistically" different from the other.


Note: Common value for significance level is 5% or α=0.05.
And I'll be using it through out this entire section.

#### Hypothesis

There are two types of hypothesis:
- Null Hypothesis: Is a hypothesis which the researchers tries nullify or reject. OR in another definition, the two variables we use are "independent"
- Alternative Hypothesis: Is a hypothesis the researchers tries to prove. OR in another definition, the two variables we use are "dependent"


So we're gonna test:
- H0: Both Movie / TV Show watchers have same time duration of watching.
- H1: movie watcher and TV show watchers are NOT the same in time watching.

So to perform those tests we need a "P-Value" threshold

```Python
# Set the ALPHA value (p-value threshold)
ALPHA = 0.05
```

After Performing the T-test

The p-value for T-test: 1.0544447755583053e-169

Movie watcher and TV show watcher are NOT the same in time watching (Reject H0)

The Null Hypothesis we sucessfuly prove it wrong!.


### Chi-square test
Determine whether there's a statistically significant difference between the expected frequencies and the observed frequencies.

Lets make a hypothesis about Movie / TV Show preference in resolution:
- H0: there is no relationship between Movie/TV Show watchers and HD preference.
- H1: There is a Strong relationship between Movie/TV Show watchers and HD preference.

I performed this test on a portion of 4% of data

The p-value for Chi-square test: 6.431612333668485e-101

There is a Strong relationship between Movie/TV Show watchers and HD preference (Reject H0)

Enough of the statistical analysis for now.

---
## EDA (Exploratory Data Analysis)

### Percentage of HD Vs. SD

Lets see users on which resolution they pick is it the same or not ?

!["pr_HD_SD"](asset/HD_SD.png)


### Most popular Genres in movie & TV Show types


Lets inspect & visualize which type of users the majority ?

#### Movie type people

![""](asset/movie_type_people.png)


#### TV Show type people

![](asset/tvshow_type_people.png)


Keypoints:
- Both Movies & TV Shows people leaning towards "Animation" genre.
- For TV Shows people Favours drama in 2nd place. Unlike Movies which Action is the 2nd.
- The Ratio of SD Movies / TV Shows are more than HD resolution.

---
### Most watched Movie and TV Show

Lets see whats the top 10 movies & TV Shows the people in JawwyTV like to watch.

#### TOP 10 Movies 
![](asset/top10_movies.png)


#### TOP 10 TV Shows

![](asset/top10_tvshows.png)


Keypoints for users preference in media type:
- For movies: the most watched "The Boss Baby" which is an animation movie.
- For TV Shows: The most watched "PAW Patrol" which also an animation of 9 seasons untill this date.
    - In the 2nd place goes to "Friends". not far from the 1st one in popularity among Jawwy users. Unlike movies the 2nd one goes very far from 1st.

---
### Insights on Weekends & Business days users activity

#### Users activity in weekends
![](asset/users_act_weekend.png)


#### Users activity in business days
![](asset/user_act_bus.png)


Keypoints:
- People tend to use Jawwy TV to watch either movies or TV shows in the Saturday for the weekend.
- For business days, It seems like people prefer Tuesday the most as the day to watch movies or TV shows.
- Interesting thing is Wednesday is the 2nd famous day to watch movies/TV shows on even though from what I see the Thursday is more popular as It's nearly a weekend even though half of it but that's interesting indeed to be Wednesday the 2nd.

---

#### User preferences movie or TV Show to watch for each day

Lets visualize those data in more broad way.

![](asset/weekend_bus.png)

keypoints:
- All DAYS people tend to learn more on watching TV shows more than movies.
- In Friday & Saturday which is a weekend here in Saudi Arabia the movie watching increasing more than the other days.



## Improvements
Any improvements to the code or anything unclear please open discussion or send me a message on twitter: [@Joxdrink](https://twitter.com/Joxdrink)

## Dataset link
https://lab.stc.com.sa/dataset/en/