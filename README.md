# Limelight Studios Movie Industry Analysis
#### Elina Rankova and Bekah McLaughlin

<div style="width: 100%; text-align: center;">
  <img src="https://www.citylit.ac.uk/media/amasty/blog/film_v1-min.jpg" width="720" height="450" style="margin: 0 auto;"/>
</div>

<u>image source</u>: <a href="https://www.citylit.ac.uk/blog/whats-the-point-of-studying-film">Why Study Film Blog Post</a>

## Business Problem and Understanding

**Stakeholders:** C-Suite leaders; Founder, CEO, CFO, COO.

As a respected member of the entertainment industry, our founder and sole investor is eager to make themselves a name in the Movie industry as a producer of valuable stories while maintaining a profit. Since reputation is important, we not only want to focus on gross, but popularity as well since we want our movies to be memorable. We are excited to work with established creators and provide them a platform to thrive both within their primary genre and branch out to diversify their portfolio and talents.

To reiterate, since we want the opportunity to continue to create in the future, we will focus on gross profit and evaluate how it correlates to other factors such as popularity.

There is a focus on a wide range of audiences and world wide reach so for the first phase of this initative, we will be evaluating world-wide grossing data as well as including all languages and regions in our analysis. In future expansion, we will want to evaluate such specifics however

Lastly, we will narrow down our search to years post the millenium as that is the start of the most recent era within movie history. In addition, our data limits our timeline not to 2023 but to 2019. This is another consideration for future endevours.

**Source:** <a href = "http://www.historyoffilm.net/movie-eras/history-of-cinema/#:~:text=With%20over%20100%20years%20of,every%20decade%20of%20its%20history.">Movie Eras - History of Cinema and the First Film</a>

**Preliminary Questions include:**

- *What genres make sense to invest based on profit and popularity among viewers?*
- *Which measure of central tendency makes sense as a reference for starting production budget for each identified genre?*
- *With which creators do we want to initate relationships within identified genres?*

Databases used and explored: 
- <a href = "https://www.boxofficemojo.com/">Box Office Mojo</a>
- <a href = "https://www.imdb.com/">IMDb</a>
- <a href = "https://www.rottentomatoes.com/">Rotten Tomatoes</a>
- <a href = "https://www.themoviedb.org/">TheMovieDB</a>
- <a href = "https://www.the-numbers.com/">TheNumbers</a>

**The goal:** Identify genres, production budget per genre, and creators in which to invest in phase 1. We want to both focus on profit and viewability based on popularity among viewers. As well as analyze which creators with whom to form relationships as we launch our first productions.

## The Datasets
We began with five original datasets, each containing substantial amounts of data. 
- One of these datasets originated from the website Rotten Tomatoes. Although we were keen on utilizing the review data within this dataset, it presented a challenge as 80% of the box-office data   was missing – a critical aspect considering profit is one of Limelight Studio's primary concerns. Furthermore, it lacked movie title data, whcih hindered our ability to merge it with other movie-grossing dataframes.
- Another significant dataset was a comprehensive IMDB SQL database, with tables detailing movie directors, writers, other industry professionals, movie particulars, and reviews. Despite lacking profit information, we successfully extracted data on movie creators, enabling us to make recommendations to Limelight Studios.
- Additionally, we used a dataset from themoviedb.org (TMDB) featuring movie reviews, popularity metrics, genres, release dates, and other relevant details.
- In our analysis, we extensively utilized data from www.the-numbers.com, particularly for comparing worldwide gross figures across movies.
- However, the dataset sourced from www.boxofficemojo.com was not useful to us due to its significant gaps in foreign gross data, which we need given Limelight Studios' emphasis on global reach.

**Ultimately, our analysis relied on data from TMDB, IMDB's directors, writers, and movie review tables, and budget/grossing information sourced from www.the-numbers.com.**

All mentioned datasets can additionally be found in the `Data` folder. 

## Data Cleaning and Preparation
Despite narrowing down our datasets, we still had a large volume of data sourced from three different sources. Since we knew we needed to merge data from the different sources, we thoroughly cleaned and processed the data for consistency and to seamlessly join. The following outlines the main steps in our data preparation process:

1. **TMDB dataframe** - In this dataframe, the column `genre_ids` contained only numerical values. We replaced these numerical representations with their corresponding genre labels. Subsequently, we cleaned the genre strings and made a new column named `primary_genre` to accommodate movies with multiple genres. Next, we addressed NaNs (missing values) and hidden NaNs by dropping rows where these occurred, as they were in columns critical for our analysis.
2. **Budget data** - Although there were no missing values in this dataframe, we did need to clean the format of several columns, including `worldwide_gross`, `domestic_gross`, `production_budget`, and `release_date`. Additionally, we created a `release_year` column to facilitate convenient filtering.
3. **IMDB tables** - In the directors and writers IMDB dataframes, we extracted pertinent columns from the persons and movies tables, such as `birth_year` and `death_year`. Initially, we removed rows with a `death_year` value to retain only individuals who are still alive. Subsequently, we eliminated the `birth_year` and `death_year` columns. We then proceeded to drop irrelevant columns and NaNs.
4. **Merging TMDB and Budget** - We merged the TMDB and budget dataframes to compare grossing information with `popularity`, `vote_average`, and `primary_genre`. To facilitate the merge, we aimed to merge on the movie title. Thus, we adjusted the column names accordingly for ease of reference and created a unique identifier column by combining `movie_title` and `release_date`. Subsequently, we cleaned the data and removed any duplicate values.

## Analysis and Findings

We first analyzed our dataframe containing TMDB and budget information. We wanted to test the correlation of several different variables, including `popularity`, `vote_average`, and `production_budget` to `worldwide_gross`. These are our results: 

#### Correlation Tests
- `worldwide_gross` vs `popularity`: With a correlation coefficient (r) of ~.64, we can confirm that the more popular the movie, the higher the gross profit with a 'moderate' positive correlation.

- `worldwide_gross` vs `vote_average`: With a r at ~.29, there is a negligible correlation, we can confirm that the `vote_average` is not a good signifier of `worldwide_gross` profits and should not be considered.

- `worldwide_gross` vs `production_budget`: There is a high positive correlation with r at ~.8, we can confirm that a higher `production_budget` is a good predicter of higher `worldwide_gross` profits.

<p align="center">
  <img src = ./Images/correlations.png>
</p> 

#### Genre Analysis
For our genre analysis, we conducted an ANOVA test to assess whether `worldwide_gross` varies based on genre. It's important to note that this test isn't perfect, as the sample sizes for the different genres vary. However, it provides an initial insight into whether further investigation into this relationship is warranted. Our results indicate that there *is* a statistical difference in gross between genres. 

We also looked at movie count by genre, popularity by genre and production budget by genre.

<p align="center">
  <img src = ./Images/Genre General Analysis.png>
</p> 

<p align="center">
  <img src = ./Images/genreanalysis.png>
</p> 

We computed the central tendencies of production_budget for each of our genres of interest. This analysis aimed to provide Limelight Studios with budget recommendations.

</p> 
  <p align="center">
  <img src = ./Images/productionbudgetplot.png>
</p> 

</p> 
  <p align="center">
  <img src = ./Images/image.png>
</p> 

Lastly, we scrutinized the ratings assigned to films by various writers and directors, with the goal of providing Limelight Studios with evidence-based collaboration recommendations.

## Recommendations and Looking Ahead

<u>*Genres:*</u><br>
For phase 1 we are investing in the following genres: **action, adventure, animation, family, fantasy, and science fiction**. We looked at a variety of factors, primarily `worldwide_gross` and `popularity`. We chose highly grossing genres as well as popular untapped markets such as Science Fiction. 


<u>*Starting Production Budget by Genre:*</u><br>
After viewing the distribution of values in our boxplot, we decided to focus on the median `production_budget` for each genre rather than the mean since the data was skewed towards the median and the mean was not a good representation. As these are starting budgets, there is room for flexibility based on specific projects, which will be determined by those working on the specific project when the time comes. This aligns with our findings stating that a higher `production_budget` is positively correlated with `popularity` as well as `worldwide_gross`.
- *Action:* 60,000,000 <br>
- *Adventure:* 99,500,000 <br>
- *Animation:* 80,000,000 <br>
- *Family:* 36,000,000 <br>
- *Fantasy:* 58,100,000 <br>
- *Science Fiction:* 52,600,000 <br>


<u>*Creators by Genre:*</u><br>
After identifying which genres we were starting with in phase 1, we took to other IMDb data on creators to find talents relevant for each genre. Of course, as we grow we want to give these individuals the chance to branch out as well, this is something we will consider on a per project basis.

*Directors:*
- *Animation:* Sumnash Sri Kaljai, Brent Triplett, and Hiroshi Nagahama <br>
- *Action:* Himesh Bhargo, Alper Caglar, and Christopher Nolan <br>
- *Science Fiction:* Erkut Altindag, M. Fahad Khan, and Eren Ozkural <br>
- *Adventure:* Karzan Kardozi, Zolbayar, Drj, Zack Bennett <br>
- *Family:* Elizabeth Blake-Thomas, Torfinn Iversen, and Ravi Jadhav <br>
- *Fantasy:* Matt Lang, Jennifer phillips, and Sung-hee Jo <br>

*Writers:*
- *Animation:* Usha Kaljai, Tony Schnur, and Yuki Urushibara <br>
- *Action:* Navdeep Maju, Alper Caglar, and Christopher Nolan<br>
- *Science Fiction:* Erkut Altindag, M Fahad Kahan, and Eren Ozkural  <br>
- *Adventure:* Karzan Kardozi, Zolbayar Dorj, and Zack Bennet <br>
- *Family:* Jonathan Brayley, Torfin Iversen, and Ravi Jadhav <br>
- *Fantasy:* Joe Walker, Jennifer Phillips, Sung-hee Jo <br>



**Conclusion** <br>

<u>*Phase 1:*</u><br>
For phase 1 of this business initiative we are focusing on making a name for ourselves as we are already well known in the industry but have not ventured into creation of movies as of yet. We are excited to make our mark and to do so, we must prioritize profit to ensure we can successfully move on with next step expansion and invest in worthy stories. <br>

While we did not include all genres of interst to our founder as their ideal portfolio is more dynamic than realistically accomplishable for phase 1, but we were able to include a diverse starter list that addresses profit as well as popularity.

We would love to work with a variety of creators and provide a platform that sets both, those we work with as well as our company up for success. While we have defined a starting budget per genre, this is just a guideline and there will be room for flexibility when a specific project launches.<br>

<u>*Looking Ahead:*</u><br>
As we continue to make our mark in the movie industry, we would want to take a deeper dive into both, what viewers prefer as well as what values we align with. The *date range* which we evaluated was limited by our data so we would be curious to evaluate data past 2020 as well. <br>

Language and region is not something we delf deep but we would like to look into how *language* and *region* plays a role in metrics we evaluated during our analysis for phase 1. <br>

As mentioned in *data limitations* we would love to take a closer look at critic reviews and box office information as this will direct us even better towards understanding how to define success within our projects. <br>

In addition, certain data had information about creators who participated in the movies we had access to, but it lacked *demographic information* we would want to take into account. We are interested in investing in stories from minorities and other less represented populations.<br>

We are also going to take a deeper dive into *ROI (return on investment)* metrics in relation to gross profit and production budget, as we do value being able to continue growing while investing in passion projects.

  ## Repository Structure

```
├── Data
├── Images
├── .gitignore
├── Limelight-Studios-Analysis-of-Movies.pdf
├── Limelight_Studios_Movie_Industry_Analysis.ipynb
└── README.md
```
