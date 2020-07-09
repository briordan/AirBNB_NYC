# AirBNB_NYC
Use regression to predict NYC AirBNB prices based on features available in the Kaggle dataset.  The features include data
on reviews, the minimum stay required, location, room type, and days available.

## Overview
I started with plotting the data to look for which features that appeared to be correlated with price. 

I cleaned the data and experimented with different techniques to handle outliers.  I removed records 
where the rental price was more than 3 standard deviations outside the mean.  While the average rental
price was $153/night, some prices were as high as $10,000.  Because there was so little data for 
properties that were 3 standard deviations above the mean, I discarded prices that exceeded $873.  I also tried 
polynomial fitting but it did not improve the model accuracy or reduce the error significantly.  I scaled 
the data between 0 and 1 and that helped with improving results.  I tried robust scaling to minimize
the effect of outliers but that did not improve the model.  Approximately 10.000 properties were 
missing data for reviews per month.  I set these to the mean value.  

I also winsorized the minimum nights stay data.  This improved the accuracy and reduced the error of the model.  
Winsorizing other data with outliers made the model less accurate.

I used Ridge regression and Decision Tree regression with hyper parameter tuning to create the model.  
Ridge regression was the recommended approach by scikit learn, and I chose Descision Tree regression because that
model accomodates outliers better.

## Results
With minimal data cleaning and prep the initial R-squared value for Ridge regression was approximately 0.1250

After cleaning the data and some experimenation the Ridge regression had an R-squared accuracy of 0.3863 and a 
mean squared error of 7153.  Decision Tree regression reguression had an R-squared accuracy of 0.4252 and a 
mean squared error of 6414.  The graphs of the actual price versus the predicted price show a linear 
clustering up to approximately $300/night, after that the ridge regression model fails.  There is just 
too little data at that price range.  The decision tree handles the outliers above $300/night.  But it 
is still too inaccurate.

The number of reviews and reviews/month appear to be negatively correlated with the price.  

## Next Steps
Combining data from other sources on the details of the rooms for rent, proximity to the subway, proximity 
to popular attractions and landmarks may help improve the model.  As may looking at how prices vary seasonally.

You can explore the data with the Tableau visualization here: 
https://public.tableau.com/profile/btriordan#!/vizhome/NYC_AirBNB/NYC_AirBNB

![Image of Visualization](https://github.com/briordan/AirBNB_NYC/blob/master/NYCAirBNBviz.jpg)


