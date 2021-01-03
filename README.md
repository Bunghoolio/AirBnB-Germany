### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
    1. [Business Understanding](#business_understanding)
    2. [Data Understanding](#data_understanding)
    3. [Prepare Data](#prepare_data)
    4. [Data Modeling](#data_modeling)
    5. [Evaluate the Results](#results)
3. [File Descriptions](#files)
5. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name ='installation'></a>

There should be no necessary libraries to run the code here beyond the Anaconda distribution of Python.  The code should run with no issues using Python versions 3.*.

## Project Motivation<a name="motivation"></a>
This project was created as part of my Udacity Data Science Nano Degree project.
Within this project I was using the [CRISP-DM](https://en.wikipedia.org/wiki/Cross-industry_standard_process_for_data_mining) process. The CRISP-DM process includes the following steps:

### Business Understanding<a name='business_understanding'></a>
This analysis aims to better understand what influences the vacation rental prices in Munich.
In particular the analysis is designed to answer the following 3 questions:

1. Is there any seasonality for Airbnb rentals in Munich?
2. Did COVID-19 affect the rental prices in Munich?
3. What features of a rental affect the rental prices in Munich most?

### Data Understanding<a name='data_understanding'></a>
The data is from Inside [Airbnb](#http://insideairbnb.com/get-the-data.html). Inside Airbnb fetches in regular periods information from Airbnb and makes these public accessible.

Out of the different files which are provided by Inside Airbnb in this analysis the following three different types of files are used:
* calendar: contains the date, price and listing_id incl. availability for one year.
* listings: contains basic listing information per vacation rental.
* listings_detailed: contains detailed listing information including descriptions, features, host information etc. per vacation rental.
The files 'calendar' and 'listings' are present for five different dates of retrieval: Oct 26th 2020, Jun 20th 2020, Apr 25th 2020, Jan 22nd 2020 and Jun 24th 2019. The file 'listings_detailed' is present for the date of retrieval Oct 26th 2020.

An detailed overview about the structure and content of the data can be seen in the notebook in the beginning of the notebook and at the beginning of section 3.


### Prepare Data<a name='prepare_data'></a>
To answer the first question the calendar file from January and October was merged together to have a continuous time frame from January 2020 until October 2021. The price was aggregated calculating the mean on day level. In the second step the listing file was used to get the neighbourhood information. The mean price plot was segregated on neighbourhood level. In the last step, the dataframe was split into a Octoberfest time and Non-Octoberfest time dataframe to calculate the price increase rate during the Octoberfest time vs Non-Octoberfest time per neighbourhood.

The second question was answered by joining calendar file with listing file for the January 2020, April 2020, June 2020, and June 2019 file. Using these joined dataframes the development of the offered vacation rentals and the development of the price per retrieval date was compared.
Using these four dataframes a joined dataframe was generated by inner joining on listing_id level. This leads to a comparison for only these listings available in all four files. Per listing and file the average price was calculated and compared over all four files to see, how many listings had a price reduction and how much was the price reduced.

The third question was analyzed using the October file of listings_detailed and calendar. The files were joined and at the beginning of the third section a deep dive into the available data structure and features had been performed. In the first step the features with no expected value for price prediction had been identified. ID and URL features had been classified as features with no expected value for price prediction. Furthermore, there had been similar features for different purposes. For these similar features only 1-2 had been kept for further modeling and the other had been dropped. (e.g. neighbourhood, neighbourhood_cleansed, Longitude, Latitude as features for location; neighbourhood has been kept for further analysis). These features with no expected value for prediction had been dropped.
The remaining features had been transformed into categorical values following a dummy creation approach.

### Data Modeling<a name='data_modeling'></a>
The third question was answered by data modeling. The prepared data was used to train a Random Forest Regressor. The trained model resulted into a r2 score 0.999982 for training data and 0.999978 for test data.

### Evaluate the Results<a name='results'></a>
The main findings of the code can be found at the post available [here](https://ulio.medium.com/airbnb-in-munich-what-influences-the-rental-prices-in-the-german-metropole-86e8ebb5e718).


## File Descriptions <a name="files"></a>

There is one notebook available here to showcase work related to the above questions. This notebooks is exploratory in searching through the data pertaining to the questions showcased in the Markdown cells in the notebook.  Markdown cells, comments and docstrings were used to assist in walking through the thought process for individual steps.  

The raw data used for the analysis is stored in the folder Munich:
* calendar: contains the date, price and listing_id incl. availability for one year.
* listings: contains basic listing information per vacation rental.
* listings_detailed: contains detailed listing information including descriptions, features, host information etc. per vacation rental.
The files 'calendar' and 'listings' are present for five different dates of retrieval: Oct 26th 2020, Jun 20th 2020, Apr 25th 2020, Jan 22nd 2020 and Jun 24th 2019. The file 'listings_detailed' is present for the date of retrieval Oct 26th 2020.

The folder 'Munich' also includes an image 'Map_of_districts_in_Munich.png' used in the notebook for orientation purposes.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>

Must give credit to ['Inside Airbnb'])(http://insideairbnb.com/about.html) for the data.  You can find the Licensing for the data and other descriptive information at the homepage of 'Inside Airbnb' available [here](http://insideairbnb.com/get-the-data.html).  Otherwise, feel free to use the code here as you would like!
Another thank goes to [jjrunner](https://github.com/jjrunner). The project [stackoverflow](https://github.com/jjrunner/stackoverflow.git) was used as a blue print for the structure of a blogpost project.
