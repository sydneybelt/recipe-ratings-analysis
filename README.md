## Introduction 

The basis for this analysis is a series of recipes taken from food.com and their associated user ratings. It is centered around the question of what types of recipes tend to have higher average ratings. This creates an interesting investigation into what food.com users tend to value most in a recipe, whether it’s health, taste, difficulty level, and whether the rating correlates more with the user-dependent process or the recipe-dependent ingredients. This dataset includes 83781 rows of unique recipes and 25 total columns. The predicted column is the average user rating of the recipe on a scale of 5. The columns used for fitting the models include those relevant to preparation procedure (the amount of time it takes to make a recipe and the number of steps it takes), the text of the review itself, the tags the recipe is associated with, and the nutritional information about the recipe (included caloric, fat, sugar, protein, and carbohydrate content). 

## Data Cleaning and Exploratory Data Analysis

Data Cleaning 

Data preparation was critical in this scenario due to the potential for incomplete information included in an online review forum. The initial stage included merging general information about the recipe with the associated reviews, then finding the average rating of a recipe given the potential for multiple reviewers. Ratings of zero were replaced with np.nan to represent that on a five star scale, zero means a rating was not given. Including a value of zero would incorrectly imply that it was a poor recipe. Another important component was extracting relevant detail from the ‘nutrition’ data column, which included varied information in a single location. This was split up into separate information on calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. This cleaning improved the ability to have specific analysis for prediction and gave more useful correlation information between features. 

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>id</th>
      <th>minutes</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>nutrition</th>
      <th>n_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>user_id</th>
      <th>recipe_id</th>
      <th>date</th>
      <th>rating</th>
      <th>review</th>
      <th>rating_avg</th>
      <th>calories</th>
      <th>total fat</th>
      <th>sugar</th>
      <th>sodium</th>
      <th>protein</th>
      <th>saturated fat</th>
      <th>carbohydrates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']</td>
      <td>[138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]</td>
      <td>10</td>
      <td>'heat the oven to 350f and arrange the rack in the middle'...</td>
      <td>these are the most; chocolatey, moist, rich, dense, fudgy...</td>
      <td>['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']</td>
      <td>9</td>
      <td>3.87e+05</td>
      <td>333281.0</td>
      <td>2008-11-19</td>
      <td>4.0</td>
      <td>These were pretty good, but took forever to bake...</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']</td>
      <td>[595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl...']</td>
      <td>this is the recipe that we use at my school...</td>
      <td>['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']</td>
      <td>11</td>
      <td>4.25e+05</td>
      <td>453467.0</td>
      <td>2012-01-26</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half ...</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>[194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees'...]</td>
      <td>since there are already 411 recipes for broccoli...</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>2.98e+04</td>
      <td>306168.0</td>
      <td>2008-12-31</td>
      <td>5.0</td>
      <td>This was one of the best broccoli casseroles that...</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>2008-02-12</td>
      <td>['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less']</td>
      <td>[878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0]</td>
      <td>7</td>
      <td>['freheat the oven to 300 degrees'...]</td>
      <td>why a millionaire pound cake?  because it's super rich!...</td>
      <td>['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']</td>
      <td>7</td>
      <td>8.13e+05</td>
      <td>286009.0</td>
      <td>2008-04-09</td>
      <td>5.0</td>
      <td>don't let the calories and fat grams scare you off. ...</td>
      <td>5.0</td>
      <td>878.3</td>
      <td>63.0</td>
      <td>326.0</td>
      <td>13.0</td>
      <td>20.0</td>
      <td>123.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>2012-03-06</td>
      <td>['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']</td>
      <td>[267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]</td>
      <td>17</td>
      <td>['pan fry bacon , and set aside on a paper towel to absorb...]</td>
      <td>ready, set, cook! special edition contest entry: a mediterranean flavor...</td>
      <td>['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil']</td>
      <td>13</td>
      <td>2.20e+06</td>
      <td>475785.0</td>
      <td>2012-03-07</td>
      <td>5.0</td>
      <td>Delicious!!!!! -- the goat cheese made the difference.  My new favorite meatloaf.</td>
      <td>5.0</td>
      <td>267.0</td>
      <td>30.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>48.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>

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

This
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>high_protein</th>
      <th colspan="4" halign="left">False</th>
      <th colspan="4" halign="left">True</th>
    </tr>
    <tr>
      <th>high_fat</th>
      <th colspan="2" halign="left">False</th>
      <th colspan="2" halign="left">True</th>
      <th colspan="2" halign="left">False</th>
      <th colspan="2" halign="left">True</th>
    </tr>
    <tr>
      <th>high_sugar</th>
      <th>False</th>
      <th>True</th>
      <th>False</th>
      <th>True</th>
      <th>False</th>
      <th>True</th>
      <th>False</th>
      <th>True</th>
    </tr>
    <tr>
      <th>high_cal</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>False</th>
      <td>4.64</td>
      <td>4.63</td>
      <td>4.66</td>
      <td>4.66</td>
      <td>4.57</td>
      <td>4.60</td>
      <td>4.63</td>
      <td>4.64</td>
    </tr>
    <tr>
      <th>True</th>
      <td>4.71</td>
      <td>4.63</td>
      <td>4.66</td>
      <td>4.64</td>
      <td>4.55</td>
      <td>4.57</td>
      <td>4.62</td>
      <td>4.62</td>
    </tr>
  </tbody>
</table>

Imputation 


## Framing a Prediction Problem

## Baseline Model

## Final Model
