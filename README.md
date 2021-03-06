# Analyzing the King County Real Estate Market

## The Goal

Using a dataset of 21,597 home sales between May 2014 and May 2015, the goal is to analyze the data to find the variables that most influence the sale of the home. We will use this information to inform real estate transactions and predict future sales.

## The First Step

The first step in analyzing a large dataset is to clean and organize the data. A solid foundation is just as important in data as it is in home buying.
Our very first step is to remove outliers which are causing our data to be warped to the extremes, making it far more difficult to find a standard.
The home prices ranged from $78,000 to $7,700,000. Far too wide a range to find meaningful conclusions for all homes.
After calculation the mean price, we settled on keeping all homes within 2 standard deviations of the mean. This eliminated 841 homes from our data. Next, we applied the same formula to remove outliers from all of the other continuous factors.
In total, our revised dataset contained 19688 data points with prices between $78,000 and $1,270,000. These should better represent the range of homes in King County.

## Working with the Prices

Let's take a closer look at our home prices.

![price](Images/LogPrice.png)

 The first image is a histogram visualizing our distribution of homes based on their price. In order to fit better to our modeling process, we prefer to see a normal curve for our price distribution. By changing our price values to their logarithm, we maintain their relative value while transforming their distribution to a smoother, normalized curve.

## Look Closer at Our Variables

Two variables in particular stood out under our analysis. One measured the square footage of a home's basement, if it had one. Through study, we found less of a utility to our data in the size of a home's basement than whether or not a home had a basement. This seems to track logically with the thought process in buying a home. We changed our dataset from measuring square footage to a binary measurement of whether a home had a basement.

The other variable we felt needed immediate work was the 'Waterfront' property. This measured whether or not a home was a waterfront property. The main issue was how many instances of homes in our data had unavailable information for this property. 

![waterfront](Images/latlong.png)

Here we plot all of our properties by latitude and longitude, making a map of King County. We color in our properties that have missing information in their 'Waterfront' description. Inspecting the map, we see no pattern in how these properties are distributed. We made the decision to turn all our missing values to NOT being waterfront properties. The map shows us that a small percentage of the missing properties are likely waterfront, and the missing data represents a small percentage of our total dataset. We are introducing some error into our model, but relatively small for what we determined was a likely important factor. This point could be retouched on in the future.

Finally, we rid our data of some variables that are outside the scope of this project. Latitude, longitude, zipcode, id, etc.

## Start Modeling

![model1](Images/firstmodel.png)

A few notes: Our R-squared is relatively low, but our Adjusted R-squared is very high relative. Our condition number is high, which implies high collinearity, or conflicting variables. Our p-scores are generally very good, with one glaring exception. This needs further investigation.

## Further Investigation

![heatmap](Images/heatmap.png)

Heatmap to check collinearity. As highlighted, there seems to be large collinearity between the square footage above a basement area and square footage of the living space. This makes a lot of sense. As the information is redundant, we drop the square footage above basement data.

Next we create scatter plots of our remaining variables.

![scatterplots](Images/scatter.png)

After analyzing the scatterplots, we log transform to normalize the square footage of the lot variable. We also find a home with 33 bedrooms, a clear outlier that is skewing our data. We drop that home too.

## Work with our Categorical Variables

After some trial and error, we came to the conclusion that what's best for our model is to categorize some of our variables into smaller, more significant groups. Our home 'grade,' for example, has 9 different qualifications, but we could combine them into 'low,' 'medium' and 'high' categories.

## Our Final Model

![finalmodel](Images/FinalModel.png)

Our R-squared is 0.404, which is lower than we would like it to be. Adjusted R-squared is very high relative, which tells us that the variables we've chosen all contribute significantly, and don't conflict much. 5 of our 9 variables chosen for this model were created for this project using the supplied King County housing data, while 4 were taken from the data itself. Our p-values all look good.

## Conclusions

With some massaging of the data, we have created a model which explains about 40% of the value of a home's price. This obviously isn't ideal. Our next steps are to look into forms of modeling aside from linear regression, as we feel there is a better fit for our data out there.