# CST383_final_project
## Introduction

We wanted to select a fun, compelling topic that would also allow us to apply the knowledge we acquired throughout the course. With the recent acknowledgements made by the United States government pertaining to UFOs and their existence, we thought a subject related to UFOs would be both interesting and relevant.

The initial objective was to predict the likelihood of seeing a UFO given a particular location and time. However, the time-series nature of the dataset was well outside the scope of the course. We then adjusted our objectives to make them more achieveable. Our revised objective was to predict the shape of a UFO based on the sighting location. In particular, we initially wanted to separate the location data by U.S. state. Upon becoming more familiar with the curriculum as the course progressed, we had to make a final revision to our research question. 

Ultimately, our research question is to determine **whether we are able to predict the shape of a UFO given certain contextual features associated with the encounter**. Our hypothesis is that making such a prediction may prove difficult but we will attempt to do so nevertheless.

## Selection of Data

The dataset used in this project was scraped from NUFORC.org by Timothy Renner and posted to data.world. It contains nearly 90,000 reports of UFO sightings in the US and Canada including information on the location, time, shape, duration, etc. We intended to use this data to predict the shape of a UFO in a particular U.S. state.

The majority of the columns in this dataset were non-numeric. In addition, the majority of the columns had no predictive value related to the shape of the UFO, so
some of these columns were removed.

#### The Data

The data contained a total of 12 features, 10 of which were non-numeric:

**non-numeric**
- summary
- city
- state
- date_time
- shape
- duration
- stats
- report_link
- text
- posted
**numeric**
- city_longitude
- city_latitude

#### Feature Engineering

We determined that the following columns had little predictive value and we decided to remove them:

- date_time
- stats
- posted
- summary
- text

Several columns also contained a significant number of NA values. This required a substantial amount of preprocessing to reformat the data in a manner that would allow us to achieve our objective. Here are the NA counts for each of the remaining columns:

- city                301
- state              5646
- shape              3671
- duration           4401
- report_link           0
- city_latitude     17870
- city_longitude    17870

Upon analizing the shapes in the dataset, we discovered two values that could be grouped together: unknown and other. We decided to replace these values, along with any NA values, with a new value called 'unidentified'.

Since we originally intended to use location data for our predictors, we decided to drop any rows where location data contained NA values.

After the feature engineering above was complete, we still had 3351 NA values in the duration feature. While this data would require a lot of processing to convert the datapoints to a standardized numeric format, we decided to leave this feature in place initially. At this point we realized the dataset did not contain a significant number of viable predictors. Due to this, we added several contextual features pertaining to UFO sightings and populated these features with random 0s and 1s. The features we added were:

- rural_area
- city_area
- observer_alone
- driving
- ufo_believer
- alcohol_consumed
- multiple_ufo_sighted
- near_ocean

## Methods

While working on this project, we used the standard suite of tools we had used throughout the course. 

#### Tools
- sklearn (linear_model, model_selection, metrics)
- NumPy
- Pandas
- Matplotlib
- Seaborn
- SciPy

The majority of the feature engineering we had to do for this project was accomplished using Pandas and NumPy.

While we recognized linear regression likely wasn't the best model to use for this problem due to the discrete target variables, we decided to explore its viability due to the simplicity of the approach. If successful this strategy would prove much more efficient than any alternatives.

## Results

Due to the discrete nature of our target variable being a class of shape, even though we assigned numeric values to each shape, our conclusion is that a linear regression model is not the correct one to use for this problem. Evaluating RMSE and R-squared show no relationship with the single predictor since the R-square value is essentially 0 and RMSE is the same as the baseline (~4.3).

Since we don't really have enough numerical features to make any meaninful predictions, we're going to bring in some more data from a dataset containing all of the churches in the US. We will combine that data with what we have in order to predict the number of UFO sightings based on the number of churches in a city.

Introducing the church data required more feature engineering. The data we used is from the following url: https://query.data.world/s/w2iiqg4xblabbhqg3sq76lk3x2h6rq . Upon merging the church and ufo data and performing the necessary feature engineering, we were able to to achieve a better R-Squared value but our RMSE was still far from ideal:

R-Squared: 0.57
RMSE: 16.824712187743078

Our models predictions for the number of UFO sightings were consistently lower than the actual data, even more so when the actual number of sightings was higher.

## Discussion

There are several conclusions that may be drawn from the results above. First, introducing additional data did actually help. While our models predictions were by no means accurate, they were noticeably better once we integrated the church data. Due to the dicrete nature of our target, the linear regression model is not suited to the problem. There were no fundamental issues with the data itself (though several columns had less predictive value). The tools we used to work on this project, namely Pandas, NumPy, and Seaborn were excellent and allowed us to quickly prepare and execute our predictions.

Regardless of what tools or data we decided to use for this project, the results likely would have been the same. The problem arose from using a linear regression model with a discrete target. A polynomial or exponential model would give us miuch better predictions, and this is the approach we will take for any future projects with similar data.

## Summary

The data required quite a bit of feature engineering before we moved on to our predictions. We initially attempted to predict UFO shape based on location, but found this was not viable with our linear regression model. We then introduced several new features in an attempt to improve the accuracy of our predictions. This was also unsuccessful, as our RMSE hovered around the baseline. In a final attempt to derive any meaningful predictions, we integrated another dataset containing church locations across the United States, and attempted to predict the number of UFO sightings in a given area based on the number of nearby churches. While the results were better (R-Squared: 0.57), we were unable to make any truly accurate predictions. From our linear regression we can conclude that there is a moderate correlation between number of churches and number of UFO sightings. Therefore, we can make some predictions about the number of UFO sightings in a given area based on how many churches are present, but we need more data in order to make such predictions with more accuracy.

### References

#### Datasets
UFO sightings within the United States and Canada: https://query.data.world/s/4vicgqesotkow23wc4q2g22vbrh5kz
Churches in the United States: https://query.data.world/s/w2iiqg4xblabbhqg3sq76lk3x2h6rq