# Phase Two Project Repo

# King County, Washington: Data Analysis & Strategy Recommendations

**Authors**: Pete VanZandt, Emma Choate, Alex Valencia

## Overview

For this project, we used linear regression to model housing sales in King County, a northwestern county in Washington state.

## Business Problem

A Seattle real estate firm wants their clients to have a prediction for the sale price of their home based on the information of their home. In order to achieve this, they would like a tool that can be as accurate as possible in their predictions. We have come in to create this tool and use it for this real estate firm’s clients.

## Data

We used data from kc_house_data.csv and column_names.md. This data contains the following information:

* **id** - unique ID for a house
* **date** - date house was sold
* **price** -  price house was sold; is prediction target
* **bedrooms** -  number of bedrooms
* **bathrooms** -  number of bathrooms
* **sqft_living** -  square footage of the home
* **sqft_lot** -  square footage of the lot
* **floors** -  floors (levels) in house
* **waterfront** - house does or does not have a waterfront
* **view** - how good the property view is
* **condition** - how good the condition is (1 - 5)
* **grade** - overall grade given to the housing unit building construction and design, based on King County grading system
* **sqft_above** - square footage of house apart from basement
* **sqft_basement** - square footage of the basement
* **yr_built** - year when house was built
* **yr_renovated** - year when house was renovated
* **zipcode** - zipcode area of the house
* **lat** - latitude
* **long** - longitude
* **sqft_living15** - square footage of interior housing living space for the nearest 15 neighbors
* **sqft_lot15** - square footage of the land lots of the nearest 15 neighbors

### Process
We screened the data and looked at the range of total prices to find any patterns. We didn't drop any residual outliers. We saw what features were the most promising by creating correlation plots. We then built a model with the one predictor whose correlation was strongest with price - sqft_living.

We used an iterative process to create more models and come up with the best predicitability on house prices for all house price ranges.

## Methods

First, we pulled the original dataframe and created three separate functions that would run a multiple regression model, a residual model, and a bin-error model. The bin-error model cuts the dataframe into 10 bins based on house prices, shows us how much error there is in predicting house prices in each bin, and shows us the standard deviation of each bin.

Next, we built our first model using sqft_living as our main predictor because its correlation was strongest with price. Our train error was 0.489 and our test error was 0.502 -- this told us that sqft_living didn't account for as much variance as we had originally expected, and there were plenty of other predictors we needed to include in our model. Our residual model showed us there were many outliers in the data and our bin-error model showed us the errors for a few bins were high, especially for houses in the top 10% price range.

We continued modifying our model by adding a new column called **area_basement** which was created by subtracting the difference between sqft_living and sqft_above. We selected 12 numerical features and scaled them using RobustScaler(), and changed our target variable from **price** to **log_price**.

We added three interaction features to the model:
 - **living_bath** (sqft_living * bathrooms)
 - **living_grade** (sqft_living * grade)
 - **grade_bath** (grade * bathrooms).

We saw significant improvement in this model because our train error increased to 0.74 and our test error increased to 0.739. Our residual model contained less outliers. Our bin-error model showed us less errors in all 10 bins -- 9 out of 10 bins contained errors that were less than $50,000. We included 20 features to get this output.

Finally, we used iterative modeling to remove the poor predictors and simplify our model. We kept 13 features - bedrooms, bathrooms, sqft_living, floors, condition, grade, yr_built, zipcode, grade * bath, lat, waterfront, long, view - and received a train error of 0.728 and a test error of 0.733. Our residual model did not change, and bin-error model still showed us our errors for 9 out of 10 bins were less than $50,000, and our Q-Q Plot revealed our data was under-disperesed which means we reduced the number of outliers in our data. 

## Results

We would suggest picking a genre of movie to make based on what is popular. 
Then, pick from a list of directors, actors, and actresses who are both popular and profitable.
Next, pick some writers who are profitable.
Finally, pick a release date based on the genre.

### Visual 1
![graph1](./images/PopGenres.png)

### Visual 2
![graph2](./images/TopPopDirectos.png)

### Visual 3
![graph3](./images/ProfitableDirectors.png)

### Visual 4
![graph4](./images/ProfitableActorsActresses.png)

### Visual 5
![graph5](./images/ProfitableWriters.png)

## Conclusions

We recommend: 
* Focus on Adventure and Action genres. 
* The top five actors are Steve Carell, Neal H, Moritz, Jason Bateman, Dwayne Johnson, and Ben Stiller. The top five actresses are Bryce Dallas Howard, Emma Stone, Kristen Bell, Brie Larson, and Mizuki Sashide.
* The top five directors are Pierre Coffin, Michael Bay, Rob Muir, Michael Colburn, and Neil Boultby. Choosing any of these would be a good idea.
* The top five writers by average movie profit are Steve Carell, Jack Kirby, Gary Whitta, Rob Muir, and Amy Poehler. 
* Release the movie at the beginning of June.

We plotted the most profitable genres by the month that they were released. In general, Adventure and Action do well any time, but it is best to release in June. We suspect that more people can go see movies during the summer so releasing at the beginning is a good move. Additionally, Thriller and Drama movies do well in October for Halloween. Romance movies make an appearance in the top five in February because of Valentine's day, but Action and Adventure are always a safe bet.

## For More Information

Please review our full analysis in [our Jupyter Notebook](./microsoft_movie_analysis_final.ipynb) or our [presentation](./Microsoft_Movie_Analysis_Presentation.pdf)

For any additional questions, please contact **Pete VanZandt - pevanzandt@gmail.com, Emma Choate - emmachoate11@gmail.com, Alex Valencia - asvalencia1688@gmail.com**

## Repository Structure

Describe the structure of your repository and its contents, for example:

```
├── README.md                           <- The top-level README for reviewers of this project
├── microsoft_movie_analysis_final.ipynb   <- Narrative documentation of analysis in Jupyter notebook
├── Microsoft_Movie_Analysis_Presentation.pdf         <- PDF version of project presentation
├── data                                <- Both sourced externally and generated from code
└── images                              <- Both sourced externally and generated from code
