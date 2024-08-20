# Latest-Movie-Recommendation-System

This project consists of two main Jupyter notebooks that together form a comprehensive movie recommendation system.

Notebooks Overview
1. trendingsan.ipynb: Focuses on generating movie recommendations based on trending metrics, such as vote counts and average ratings.
   
2. contentsan.ipynb: Builds a content-based recommendation system that uses the textual content (such as genres, production companies, and overviews) of movies to suggest similar movies.

Prerequisites
-Python 3.x

-Jupyter Notebook

-Libraries: pandas, numpy, sklearn





# 1. trendingsan.ipynb
   
 This notebook is used to analyze trending movies based on their popularity metrics, such as vote counts and ratings. It calculates a weighted score to recommend movies that are currently trending. 

Key Sections

Loading the Dataset: The dataset is loaded using pandas and any missing data is handled.

Calculating Weighted Scores: A function is defined to calculate a weighted IMDB-like rating based on vote count and vote average.

Generating Recommendations: The movies are sorted based on their weighted scores to identify the top trending movies.

Customization:

*Adjusting the Weighting: Users can modify the weighted_IMDB_rating function to adjust how the vote count and vote average influence the final score.

*Filtering Data: Additional filters can be applied to focus on specific genres, release years, or other criteria.



# 2. contentsan.ipynb
This notebook creates a content-based recommendation system using textual data such as genres, production companies, and movie overviews. It vectorizes the text and uses cosine similarity to recommend movies that are similar to a given movie.

Key Sections

Text Preprocessing: The clean_data function cleans and preprocesses the text data by converting it to lowercase and removing spaces.



          def clean_data(x):

                  if isinstance(x, list):
    
                      return [str.lower(i.replace(" ", "")) for i in x]
        
                  else:
    
                        if isinstance(x, str):
        
                            return str.lower(x.replace(" ", ""))
            
                        else:
        
                            return ''

            
Creating the Soup: A combined text column called soup is created by merging the genres, production companies, and overview for each movie.



                latest_movies['soup'] = latest_movies['production_companies'].fillna('') + ' ' + latest_movies['genres'].fillna('') + ' ' + latest_movies['overview'].fillna('')

Vectorization: The CountVectorizer is used to convert the soup column into a matrix of token counts.



                count = CountVectorizer(stop_words='english')

                count_matrix = count.fit_transform(latest_movies['soup'])

Calculating Similarity: Cosine similarity is calculated between the movies based on the vectorized soup.



                cosine_sim = linear_kernel(count_matrix, count_matrix)

Generating Recommendations: The system returns the top 10 most similar movies based on the cosine similarity score.


            

   
Customization
Switch to TF-IDF: Users can easily switch from CountVectorizer to TfidfVectorizer if they prefer to account for the importance of terms across the entire dataset.


              from sklearn.feature_extraction.text import TfidfVectorizer

              tfidf = TfidfVectorizer(stop_words='english')

              tfidf_matrix = tfidf.fit_transform(latest_movies['soup'])

Change Input Data: The soup can be customized by including other features such as director names or keywords, depending on what features you think are important for the recommendations.

This project provides a strong foundation for building a movie recommendation system using both trending metrics and content-based similarity. Users are encouraged to experiment with the provided functions and customize the process according to their specific needs.


AUTHOR: SANTTOSH MUNIYANDY
