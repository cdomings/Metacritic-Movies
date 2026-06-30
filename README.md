# Movie Revenue Analysis — 2008

## Project Overview

This project was completed as an assignment for **DA320: Data Acquisition & Management**. The goal of the assignment was to create a portfolio-quality Jupyter Notebook that demonstrates the ability to acquire, clean, merge, analyze, and visualize real-world movie data.

For this project, I selected the year **2008** and analyzed movie data from both **IMDB** and **Metacritic**. The two datasets were retrieved from MongoDB, merged using Pandas, and analyzed using regression modeling and machine learning sentiment analysis.

The final notebook explores relationships between movie ratings, critic scores, audience responses, and sentiment patterns in movie-related text data.

## Research Question

The main question explored in this project is:

**What can movie data from 2008 tell us about the relationship between ratings, critic scores, audience reception, and sentiment?**

By combining IMDB and Metacritic data, this project investigates whether different movie quality indicators align with one another and whether machine learning sentiment analysis can reveal additional insights about movie reception.

## Data Sources

This project uses two MongoDB collections:

1. **IMDB movie data**

   * Movie title
   * Release year
   * IMDB rating
   * Votes
   * Genre and other available movie metadata

2. **Metacritic movie data**

   * Movie title
   * Metascore
   * User score
   * Summary or description fields
   * Additional critic and audience-related information

Only movies from the year **2008** were retrieved from both datasets.

## Data Pipeline

The project follows the data pipeline below:

1. Load the MongoDB connection string from a hidden credentials file.
2. Connect to MongoDB using Python.
3. Retrieve all IMDB movie records from the year 2008.
4. Retrieve all Metacritic movie records from the year 2008.
5. Convert both query results into Pandas DataFrames.
6. Merge the IMDB and Metacritic datasets using:

```python
pandas.merge(imdb, metacritic, how="inner", on="title")
```

7. Clean and prepare the merged dataset for analysis.
8. Run regression analysis using `statsmodels.formula.api.ols()`.
9. Apply machine learning sentiment analysis.
10. Create charts to visualize the results.
11. Write a conclusion explaining the findings.

## Machine Learning Component

This project uses a Hugging Face Transformers sentiment analysis model:

```python
cardiffnlp/twitter-xlm-roberta-base-sentiment
```

The model is used to classify movie-related text into sentiment categories such as positive, neutral, or negative.

A new machine learning analysis column is added to the merged dataset. This column is then used to filter and compare movies based on sentiment.

## Regression Analysis

A regression model is created using:

```python
statsmodels.formula.api.ols()
```

The regression analysis is used to explore possible relationships between movie-related variables, such as critic scores, user scores, IMDB ratings, and other numeric features available in the merged dataset.

## Visualizations

The notebook includes at least two plots based on the merged and machine-learning-enhanced dataset.

The charts are designed to show patterns such as:

* How sentiment categories relate to IMDB ratings
* How Metacritic scores compare across sentiment groups
* Whether critic scores and audience ratings appear to move together
* Whether positively classified movies tend to receive higher ratings

## Key Findings

The analysis of 2008 movie data produced several interesting findings:

* Adding sentiment values to the regression model improved the R-squared value slightly, but the improvement was not very large. This suggests that sentiment may add some explanatory value, but it was not the strongest predictor in the model.

* Most user ratings were between 5 and 8. Within this rating range, the majority of movies had a negative sentiment value.

* For movies released in 2008, gross sales generally increased as user ratings increased. This suggests a positive relationship between user ratings and gross sales.

* September had the highest number of movie releases in the dataset, with 12 movies released during that month. November had the lowest number, with only 2 movie releases.

* Movie releases were also fairly consistent during the summer season. From June through August, around 7 to 8 movies were released each month.

* There were more movies with negative sentiment scores than positive sentiment scores. Only three movies in the dataset had positive sentiment scores.


## How to Run the Notebook

1. Clone this repository.
2. Open the Jupyter Notebook.
3. Make sure your hidden credentials file contains the MongoDB connection string.
4. Install the required Python packages.
5. Run the notebook cells from top to bottom.

Example package installation:

```python
%pip install pandas pymongo statsmodels transformers matplotlib seaborn
```

## Conclusion

This project demonstrates the full data analysis process, from data acquisition to machine learning and visualization. By focusing on movies from 2008, the notebook provides a focused case study of how multiple data sources can be combined to produce a richer analysis.

The project also shows how machine learning can be used as part of an exploratory data analysis workflow. Sentiment analysis does not replace traditional ratings or critic scores, but it can help reveal patterns that may not be obvious from numeric data alone.
