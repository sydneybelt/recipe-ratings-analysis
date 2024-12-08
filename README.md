## Introduction 

The basis for this analysis is a series of recipes taken from food.com and their associated user ratings. It is centered around the question of what types of recipes tend to have higher average ratings. This creates an interesting investigation into what food.com users tend to value most in a recipe, whether it’s health, taste, difficulty level, and whether the rating correlates more with the user-dependent process or the recipe-dependent ingredients. This dataset includes 83781 rows of unique recipes and 25 total columns. The predicted column is the average user rating of the recipe on a scale of 5. The columns used for fitting the models include those relevant to preparation procedure (the amount of time it takes to make a recipe and the number of steps it takes), the text of the review itself, the tags the recipe is associated with, and the nutritional information about the recipe (included caloric, fat, sugar, protein, and carbohydrate content). 

## Data Cleaning and Exploratory Data Analysis

Data Cleaning 

Data preparation was critical in this scenario due to the potential for incomplete information included in an online review forum. The initial stage included merging general information about the recipe with the associated reviews, then finding the average rating of a recipe given the potential for multiple reviewers. Ratings of zero were replaced with np.nan to represent that on a five star scale, zero means a rating was not given. Including a value of zero would incorrectly imply that it was a poor recipe. Another important component was extracting relevant detail from the ‘nutrition’ data column, which included varied information in a single location. This was split up into separate information on calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. This cleaning improved the ability to have specific analysis for prediction and gave more useful correlation information between features. 

Univariate Analysis 

The distribution of average ratings across recipes is included in the box plot below to demonstrate the range of ratings that we are trying to predict in this analysis. Given a five-star scale, there is limited variation among average ratings which makes a carefully crafted prediction model necessary for quality results. The average ratings metric indicates a regression problem due to the continuous numerical data, but a categorical approach could be applied to separate the ratings into discrete buckets from ‘excellent’ to ‘poor’. 

<iframe
  src="assets/rating_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Bivariate Analysis 

A correlation between the number of steps in a recipe and its average rating is included below as this metric could indicate factors like the amount of time the recipe takes, the difficulty in making it, and the amount of detail included in the description of the steps, all of which could impact the resulting rating. This plot shows that while any number of steps could yield a high recipe rating, those with significantly more steps are generally rated higher, likely due to detailed instructions, complicated and flavorful dishes, and the quality of cooks willing to take on the challenge. 

<iframe
  src="assets/steps_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Interesting Aggregates 

Imputation 


## Framing a Prediction Problem

## Baseline Model

## Final Model
