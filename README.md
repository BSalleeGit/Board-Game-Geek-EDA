# Board-Game-Geek-EDA

# Project Overview:
We will be examining a dataset from the BoardGameGeek database from the perspective of someone looking for guidance on developing their own board game. Our primary concern is to explore the dataset to discover any features or aspects of a board game which may lead to a more successful product. As the project progresses we choose to focus on a more in depth examination of the Rating Average data column under the assumption that a game with a higher Rating Average score would better reflect consumer's tastes. We also produce and evaluate a couple of regression models to attempt to understand which data features are the most likely to predict a better potential Rating Average score.



# Installation & Setup:

## Resources Used:
**Editor Used:** Jupyter Lab 4.0.11

**Python Version:** 3.12.4

## Python Packages Used:
**General Purpose:** RE (Regular Expressions), Collections, Warnings

**Data Manipulation:** Pandas, Numpy

**Data Visualization:** Matplotlib, Seaborn

**Machine Learning:** Scikit Learn



# Data
## Source Data
**Initial Dataset** - The dataset as sourced from Kaggle. Includes 14 unique columns with data on a game's name, number of users owned, its ranking on the BoardGameGeek website, its rating average, etc.

**Cleaned Full Dataset** - The dataset after having accounted for NaN and missing values, outliers, and adjusting the formatting for several text and numeric data columns.

**Cleaned Numeric Dataset** - Same as the cleaned dataset above, but all of the  non-numeric data columns have been removed to make some of our analytical approaches easier and quicker.

**One Hot Encoded Dataset** - The same as the cleaned numeric dataset, but all individual items from the Mechanics and Domains text columns have been converted with One Hot Encoding and then re-attached for use in our machine learning models.


## Data Acquisition
Original dataset was acquired from the Kaggle website at:

[BGG Dataset](https://www.kaggle.com/datasets/andrewmvd/board-games)

## Data Preprocessing
The original dataset was initially cleaned through the removal of NaN and missing values and edited for outliers in a few select data columns. Several of the numeric columns were using commas where decimals values needed to be and thus required swapping. 

After the initial dataset was cleaned it was separated into a full version and a numeric column only version. This was done to enable easier use of the dataset in the analysis and plotting of the various columns with each other. The ID, Name, Mechanics, and Domains columns were removed because they were either irrelevant (ID and Name) or would be dealt with separately later (Mechanics, Domains). 

The text-based columns of Mechanics and Domains used a mix of commas and slashes to indicate separate items within their string values, so those columns had the slashes replaced with commas for standardization and later had a couple of functions applied to them which separated each individual item within the strings and were then used to build dictionaries so that they could be analyzed. After this, one hot encoding was used to create numeric values and new columns for each of the items within the Mechanics and Domains columns before being re-attached to our cleaned numeric dataset and used in two random forest regression models.


# Code Structure

The four dataset files included represent the changes applied to our dataset as the project progressed. All four are not required to recreate the project (only the initial dataset is), they are simply included for convenience if someone would like to re-create a specific part of the project. 

The code of the notebook is organized into eight general sections which can be jumped to in the Table of Contents at the top of the notebook. They are:

1) Importing the necessary packages and libraries and loading the dataset.

2) Data cleaning, where the initial dataset is cleaned and processed for use.

3) Initial exploration of numeric data, where a series of pair-plots and a correlation matrix heatmap are used to visualize how different data columns correlate and compare with each other and leads us to choose to focus on the Rating Average column.

4) Linear regression model, where a linear regression model is created and evaluated for predicting rating average scores from the complexity average values.

5) Mechanics and domains, where the mechanics and domains columns are processed for a basic analysis of their individual item counts and their most/least frequently occurring items.

6) Data preprocessing of mechanics and domains, where the items within the two columns have one hot encoding applied and are rejoined to our cleaned dataset for use in machine learning models.

7) Random forest regression models, where two models are created and evaluated with our dataset to understand which features are the most influential on predicting a rating average score.

8) Conclusion, where we draw our final thoughts on what the data exploration has revealed to us.



# Results & Evaluation
The exploration of the dataset led to the discovery of a moderate positive correlation between the complexity average and the rating average of a game as indicated by this heatmap:![Correlation Matrix Heatmap](https://github.com/user-attachments/assets/4dbb5a6c-c732-4100-828e-1dce3c5f3142)


Following this a linear regression model and random forest regression model were constructed and evaluated examine predictions for rating averages based off of the dataset's features. The models were evaluated using mean squared error, root mean squared error and mean absolute error to evaluate the model's performance (where closer to 0 is better) and using r-squared to evaluate the model's fit (where closer to 1 is better). The linear regression model used only the complexity average as a variable and produced expectedly low, inaccurate scores as a result of the model's simplicity. 

The scores were: 

**Mean Absolute Error:** 0.6271243481764985

**Mean Squared Error:** 0.6601674404295852

**Root Mean Squared Error:** 0.8125068863890232

**R^2 Score:** 0.24410413791119123
<br>
<br>

The random forest regression model used most of the features included in the dataset and better reflected expectations drawn from the heatmap seen earlier. The scores were moderate and better reflected the small to moderate correlations that some of the features had with the rating average. 

The final scores were:

**Mean Absolute Error:** 0.4618715727295101

**Mean Squared Error:** 0.4047420189318237

**Root Mean Squared Error:** 0.6361933817101713

**R^2 Score:** 0.5540315219962973
<br>
<br>

Our random forest regression model for the data features revealed that the complexity average was the most important contributing feature in our model followed by the year published, users rated, and owned users data columns.![Feature Importances](https://github.com/user-attachments/assets/74408e01-1275-4abc-add8-13bd23c6ac4f)

However, complexity average was only a moderate contribution to our predictions and the rest were minor contributions. These results can be interpreted as indicating that implementing some level of complexity to a game will help to improve its rating average to an extent, but is not a defining feature of board game development. The other, minor contributing features are more a representation of the growing popularity of the board game hobby leading to more reviews of games in general and a small bump to rating averages.



# Future Work
Possible future work could explore further beyond the Rating Average column within the dataset. The Owned Users column would be the next logical place to explore to attempt to gain insights into what may motivate more people to purchase the game being developed. The problem with this is that the Owned Users column has either low or negligible correlations with the other features in the dataset, so it is most likely a dead-end. However, attempting to discover some correlations with, or feature importance to, the Owned Users column through the Mechanics and Domains columns might possibly gleam some insights. Gaining insights into which mechanics and domains are associated with a higher amount of owned users could be useful to a game developer. Another random forest model or other machine learning models may reveal new insights.


# Acknowledgments/References
[Kaggle data source](https://www.kaggle.com/datasets/andrewmvd/board-games)

[Karnika Kapoor's Board Game Analysis notebook](https://www.kaggle.com/code/karnikakapoor/board-games-analysis) on Kaggle for functions to strip and clean the Mechanics & Domains columns.



# License
Under [MIT License](https://opensource.org/license/mit)
