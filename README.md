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

## Results



## Discussion

## Summary