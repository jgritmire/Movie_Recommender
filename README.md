# Movie_Recommender


# Building a Movie Recommender

#### Required Data
in order to run the notebooks in this repository, data must be downloaded from the following links:
    https://www.imdb.com/interfaces/
    https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset

## Table of Contents

#### 1_compiling_MDB_data.ipynb
In this notebook, I take all of the information provided by IMDB and compile it into a single csv for further analysis

#### 2_cleaning_preprocessing
In this notebook, I take the compiled IMDB data and remove nulls, format the data in a usable way, and scrape some plot information

#### 3_wikipedia_synopsis_scraping
In this notebook, I scrape complete plot synopses from wikipedia. This notebook is separated out from the others because it takes several hours to run. 
    
#### 4_compiling_wikipedia
In this notebook, all of the information scraped from wikipedia is processed and cleaned into a usable format, with some NLP performed on it. I had larger aspirations for what I was going to do with the data scraped from wikipedia, but my dataset was rapidly becoming too large. 

#### 5_eda_feature_eng
In this notebook, I perform initial exploratory data analysis of my compiled datasets. 

#### 6_preparing_review_data
In this notebook, I collect review data from Movie Lens, and process it so that it can be referenced appropriately with my existing data.

#### 7_product_based_recommender
In this notebook, I build my product based recommender.

#### 8_review_based_recommender
In this notebook, I build my review based recommender.
    
#### 9_cleaned_recommender_scripts
This notebook contains the the two fully functioning recommenders and a hybrid recommender. 

## Data Description
The dataset I compiled from IMDB, Movielens, and Wikipedia contains details on 8,000 films including title, release year, cast and crew information, plot syopsis, genre, and more. Additionally, the review dataset contains movie reviews for over 150,000 unique users. 

## Modeling
My product based recommender takes all of the details of each movie in my dataset, turns these values into a vector, calculates the cosine similarity score to all the other films, and then returns a list of the most similar movies based on what films the user reported that they had enjoyed. The similarity score is calculated based on the film's genre tags, writers, directors, cast, IMDB/Metacritic/Rotten Tomatoes score, and plot polarity score. Unfortunately, it is very difficult to capture all of the aspects of a film in a numerical manner, and so the product based recommender will sometimes return movies that are seemingly not very similar to the input movies. However, this can be an asset rather than a flaw because it may return some interesting movies that you had not previously heard of or considered watching. 

My Review based recommender utilizes a database of over 150,000 unique users reviews of over 8,000 films. The recommender takes each users reviews, and vectorizes the review scores all the films they have seen, calculates the cosine similarity score to all other users, and then when you input a movie, the recommender returns a list of films that were liked by similar users. This recommender tends to return a far less surprising list of movies, for example if you input a pixar film, you are likely to get another pixar film as a recommended movie. This  indicates that the recommender is working exactly as intended.

My hybrid recommender functions in the same ways as the two recommenders above, but simply returns a mixed list of outputs based on both product similarity and review similarity.
    
## Conclusion
I set out to build a movie recommender that could take user input (a list of several movies) and return recommendations based on these movies. I wanted to try and capture as many aspects of a film as possible through the construction of my dataset, but ultimately I overestimated the availability of this data, as well as the ease with which I could compile the existing data on the internet. When building my product based recommender, I found that the movies that my recommender would sometimes return odd films. I attributed this to my dataset being somewhat limited, as there are many intangible aspects of films that are difficult to measure with numbers, and due to the limitations of the hardware I was working with, I was unable to do extensive natural langauge processing on the complete synopses of the films to try and tease out more measurable similarities between films.  
    
Next I built my review based recommender. The review based recommender returned much less suprising films as recommendations, but felt a little uninspired in its basic state. What I ultimately settled on was a hybrid recommender that took some recommendations from the review based recommender, and some recommendations from the product based recommender which would spit out a list of 5-7 more well known movies, and a few oddball movies that might be appealing to a more adventurous viewer.
    
The next steps for this project would be to continue improving on the recommender, so that it can handle feedback on its recommendations, store that feedback, and provide more personally tailored future recommendations. I would like it to do all this while keeping track of films that the viewer has seen/have already been recommended so that the recommender does not continue to output a list of the same films over and over. 
