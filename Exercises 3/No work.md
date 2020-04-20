Predictive Model Building
=========================

The data being analyzed regarding commercail rental properties from
across the Unites States contains twenty-one variables, ranging from the
rent amount charged to tenants to the annual precipitation of the
buildings’ geographoic region to whether or not the building is
economically-green certified. The full list of variables can be seen in
the preview of the data below.

    ## Observations: 7,894
    ## Variables: 23
    ## $ CS_PropertyID     <int> 379105, 122151, 379839, 94614, 379285, 94765, 236...
    ## $ cluster           <int> 1, 1, 1, 1, 1, 1, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 8...
    ## $ size              <int> 260300, 67861, 164848, 93372, 174307, 231633, 210...
    ## $ empl_gr           <dbl> 2.22, 2.22, 2.22, 2.22, 2.22, 2.22, 4.01, 4.01, 4...
    ## $ Rent              <dbl> 38.56, 28.57, 33.31, 35.00, 40.69, 43.16, 12.50, ...
    ## $ leasing_rate      <dbl> 91.39, 87.14, 88.94, 97.04, 96.58, 92.74, 94.33, ...
    ## $ stories           <int> 14, 5, 13, 13, 16, 14, 11, 15, 31, 21, 11, 15, 15...
    ## $ age               <int> 16, 27, 36, 46, 5, 20, 38, 24, 34, 36, 32, 25, 26...
    ## $ renovated         <int> 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0...
    ## $ class_a           <int> 1, 0, 0, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1...
    ## $ class_b           <int> 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0...
    ## $ LEED              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ Energystar        <int> 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1...
    ## $ green_rating      <int> 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1...
    ## $ net               <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0...
    ## $ amenities         <int> 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0...
    ## $ cd_total_07       <int> 4988, 4988, 4988, 4988, 4988, 4988, 2746, 2746, 2...
    ## $ hd_total07        <int> 58, 58, 58, 58, 58, 58, 1670, 1670, 1670, 1670, 1...
    ## $ total_dd_07       <int> 5046, 5046, 5046, 5046, 5046, 5046, 4416, 4416, 4...
    ## $ Precipitation     <dbl> 42.57, 42.57, 42.57, 42.57, 42.57, 42.57, 25.55, ...
    ## $ Gas_Costs         <dbl> 0.01370000, 0.01373149, 0.01373149, 0.01373149, 0...
    ## $ Electricity_Costs <dbl> 0.02900000, 0.02904455, 0.02904455, 0.02904455, 0...
    ## $ cluster_rent      <dbl> 36.78, 36.78, 36.78, 36.78, 36.78, 36.78, 17.50, ...

What is the best model for predicting price?
--------------------------------------------

There are many different models that can be used to predict the prices
of the buildings in our dataset. Once the different models have been
established, the Roor Mean Square Errors (RMSE) of each model are
compared to identify which predictive model is the most accurate.
Although the prices of the buildings is not a variable in the data set,
I have combined rent, gas costs, and electricity costs in order to
create a price variable for each building. Whether or not a building is
LEED certified and whether or not a building is Energystar certified
were decided to keep seperately, as each of the two indicates it’s own
specific kinds of green certifications. the building ID column has also
been removed. A preview of the altered data can be seen below.

    ## Observations: 7,894
    ## Variables: 20
    ## $ cluster       <int> 1, 1, 1, 1, 1, 1, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 8, 8,...
    ## $ size          <int> 260300, 67861, 164848, 93372, 174307, 231633, 210038,...
    ## $ empl_gr       <dbl> 2.22, 2.22, 2.22, 2.22, 2.22, 2.22, 4.01, 4.01, 4.01,...
    ## $ leasing_rate  <dbl> 91.39, 87.14, 88.94, 97.04, 96.58, 92.74, 94.33, 91.0...
    ## $ stories       <int> 14, 5, 13, 13, 16, 14, 11, 15, 31, 21, 11, 15, 15, 31...
    ## $ age           <int> 16, 27, 36, 46, 5, 20, 38, 24, 34, 36, 32, 25, 26, 28...
    ## $ renovated     <int> 0, 0, 1, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0,...
    ## $ class_a       <int> 1, 0, 0, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 0,...
    ## $ class_b       <int> 0, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0,...
    ## $ LEED          <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,...
    ## $ Energystar    <int> 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0,...
    ## $ green_rating  <int> 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0,...
    ## $ net           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,...
    ## $ amenities     <int> 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0,...
    ## $ cd_total_07   <int> 4988, 4988, 4988, 4988, 4988, 4988, 2746, 2746, 2746,...
    ## $ hd_total07    <int> 58, 58, 58, 58, 58, 58, 1670, 1670, 1670, 1670, 1670,...
    ## $ total_dd_07   <int> 5046, 5046, 5046, 5046, 5046, 5046, 4416, 4416, 4416,...
    ## $ Precipitation <dbl> 42.57, 42.57, 42.57, 42.57, 42.57, 42.57, 25.55, 25.5...
    ## $ cluster_rent  <dbl> 36.78, 36.78, 36.78, 36.78, 36.78, 36.78, 17.50, 17.5...
    ## $ Price         <dbl> 38.60270, 28.61278, 33.35278, 35.04278, 40.73278, 43....

Linear regression
=================

The first model I have used to predict building prices was a linear
model. The data has been split into two different sets, the training set
that contains a sample of 80% of the buildings observations, and the
testing set that contains the remaining 20% of observations. The
training set is used to create a multiple linear regression model using
variables that are presumed to have a significant affect on price. Once
the regression model had been determined, the prices of the buildings in
the testing set had then been predicted using the model and then a RMSE
value was calculated between the predicted prices and the actual prices
of the testing set. This process has been repeated 100 times to get an
accurate RMSE, which was calculated by finding the average RMSE of all
100 tests ran.

    ## 
    ## Call:
    ## lm(formula = Price ~ age + stories + green_rating, data = greenb_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -26.852  -9.313  -2.883   5.483 217.865 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  28.961947   0.440508  65.747  < 2e-16 ***
    ## age          -0.041535   0.006162  -6.741 1.71e-11 ***
    ## stories       0.103167   0.015639   6.597 4.54e-11 ***
    ## green_rating  0.305369   0.684488   0.446    0.656    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 15.09 on 6261 degrees of freedom
    ## Multiple R-squared:  0.01716,    Adjusted R-squared:  0.01669 
    ## F-statistic: 36.43 on 3 and 6261 DF,  p-value: < 2.2e-16

![](Figs/unnamed-chunk-3-1.png)

    ##   result 
    ## 14.88697

Here is a visual of the predicted values of the linear model shown
against the actual values for green versus non green buildings
(nongreen=0, green=1), as well as a summary of the result. Looking at
the coefficients, the predictive formula for price was able to be
determined as `lm_formula` “The adjusted R-squared value is pretty low,
which reflects a model that fits the data poorly. We can also conclude
from the plots that the model might not be a great fit since the
residuals for both green and non-green buildings seem to be pretty
large. The calculated RMSE value is `RMSE1` which will be compared to
our other models later on.”

Stepwise linear regression
==========================

Now, instead of coming up with a linear model using variables that I
think significantly impact building prices, I used stepwise selections
to take the base model I created and add variables that will make the
multiple regression model more accurate in it’s prediction of price. The
linear model using the stepwise selection method is described below
along with the model’s coefficients and summary of it’s statistic
values.

    ## 
    ## Call:
    ## lm(formula = Price ~ age + stories + green_rating + cluster_rent + 
    ##     size + cd_total_07 + class_a + cluster + leasing_rate + class_b + 
    ##     Precipitation + net + empl_gr + stories:cluster_rent + cluster_rent:size + 
    ##     size:cluster + cluster_rent:cluster + size:cd_total_07 + 
    ##     size:leasing_rate + age:class_b + age:class_a + cluster_rent:leasing_rate + 
    ##     size:Precipitation + stories:cluster + cd_total_07:net + 
    ##     class_a:empl_gr + class_b:Precipitation + class_a:Precipitation + 
    ##     cluster:leasing_rate + green_rating:class_a + stories:class_b, 
    ##     data = greenb_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -57.645  -3.529  -0.669   2.584 156.457 
    ## 
    ## Coefficients:
    ##                             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)                3.184e-01  2.037e+00   0.156 0.875828    
    ## age                        2.034e-02  1.073e-02   1.895 0.058126 .  
    ## stories                    1.647e-01  4.684e-02   3.515 0.000442 ***
    ## green_rating               1.868e+00  8.903e-01   2.098 0.035917 *  
    ## cluster_rent               6.768e-01  5.586e-02  12.117  < 2e-16 ***
    ## size                      -2.164e-05  4.015e-06  -5.389 7.35e-08 ***
    ## cd_total_07               -4.941e-04  1.802e-04  -2.743 0.006111 ** 
    ## class_a                    8.921e+00  1.477e+00   6.042 1.61e-09 ***
    ## cluster                   -2.098e-03  1.395e-03  -1.504 0.132727    
    ## leasing_rate              -2.557e-02  1.852e-02  -1.380 0.167587    
    ## class_b                    7.207e+00  1.305e+00   5.522 3.49e-08 ***
    ## Precipitation              1.005e-01  2.987e-02   3.363 0.000776 ***
    ## net                       -3.668e+00  1.040e+00  -3.525 0.000426 ***
    ## empl_gr                    5.793e-03  2.306e-02   0.251 0.801631    
    ## stories:cluster_rent      -6.599e-03  1.471e-03  -4.488 7.33e-06 ***
    ## cluster_rent:size          7.523e-07  5.706e-08  13.185  < 2e-16 ***
    ## size:cluster               1.087e-08  2.116e-09   5.138 2.87e-07 ***
    ## cluster_rent:cluster       1.692e-04  3.056e-05   5.536 3.22e-08 ***
    ## size:cd_total_07          -1.152e-09  5.078e-10  -2.268 0.023375 *  
    ## size:leasing_rate          1.010e-07  3.574e-08   2.827 0.004716 ** 
    ## age:class_b               -4.808e-02  1.198e-02  -4.013 6.08e-05 ***
    ## age:class_a               -4.851e-02  1.565e-02  -3.100 0.001941 ** 
    ## cluster_rent:leasing_rate  1.850e-03  6.098e-04   3.034 0.002427 ** 
    ## size:Precipitation        -1.111e-07  4.584e-08  -2.424 0.015368 *  
    ## stories:cluster           -1.093e-04  4.831e-05  -2.263 0.023656 *  
    ## cd_total_07:net            1.286e-03  4.293e-04   2.996 0.002744 ** 
    ## class_a:empl_gr            5.284e-02  3.045e-02   1.736 0.082663 .  
    ## class_b:Precipitation     -1.117e-01  3.342e-02  -3.344 0.000831 ***
    ## class_a:Precipitation     -1.030e-01  3.690e-02  -2.791 0.005273 ** 
    ## cluster:leasing_rate      -2.822e-05  1.500e-05  -1.881 0.059984 .  
    ## green_rating:class_a      -1.716e+00  1.019e+00  -1.683 0.092333 .  
    ## stories:class_b            8.703e-02  2.714e-02   3.207 0.001348 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 9.338 on 6233 degrees of freedom
    ## Multiple R-squared:  0.6255, Adjusted R-squared:  0.6237 
    ## F-statistic: 335.9 on 31 and 6233 DF,  p-value: < 2.2e-16

The r-squared value of `r_val` reveals that this model fits the data
pretty well. This value is higher than the previous linear regression,
hinting that this stepwise selected model is accurate at predicting
building prices. We will use the 100 training/testing procedure used
earlier to once again calculate a reliable RMSE value. The RMSE for our
stepwise linear model is `RMSE2`, which is in the same ballpark as our
first linear regression model.

    ##  RMSE =  15.21981

What causes what?
=================

**1. Why can’t I just get data from a few different cities and run the
regression of “Crime” on “Police” to understand how more cops in the
streets affect crime?** This is because the assumption you’re making
about the correlation may not be accurate. For example, in the podcast
they discuss how the terrorist threat level impacts the amount of police
out in the public, which in turn affects crime amount in that area. So
yes, “Crime” and “Police” may have a correlation, but it is actually do
to a confounding variable. Picking a few different cities would not give
rable data since these confounding variables differ depending on the
city.

**2. How were the researchers from UPenn able to isolate this effect?
Briefly describe their approach and discuss their result in the “Table
2” below, from the researchers’ paper.**

The researchers were able to isolate this affect by looking at
confounding variables during times when police on the streets was higher
during for non-crime related reasons. They noticed that the times when
the terrorist threat level was raised to orange seem to have aligned
with their other data, which led them to question if raised threat
levels, which leads more cops to be on the streats, was actually the
reason crime was lower. Before they could correctly make this
conclusion, they checked to see if the there is any correlation between
orange level terrorist threat days and the amount of tourists that
visited D.C., which is shown in the table that there in fact is not a
correlation.

**3. Why did they have to control for Metro ridership? What was that
trying to capture?** The researchers controlled Metro ridership to
determine if the reduction in crime was actually becuase the criminals
were staying home due to the raised terrorist threat level, which would
be seen because other people of the general public would also stay home
and would not be riding the metro.

**4. Below I am showing you “Table 4” from the researchers’ paper. Just
focus on the first column of the table. Can you describe the model being
estimated here? What is the conclusion?**

The model seems to be a predictive model describing the relationship
between each variable used and crime. The two variables “High Alert x
District 1” and “High Alert x Other Districts” are used to described how
orange level threats in District 1 and how orabge level threats in other
districs impact crime. Raised alerts in Distric 1 has a significant
impact on crime, while raised alerts in other districs has a much
smaller impact on crime. The “Log(midday ridership)” variable reaffirms
the earlier belief that people are still out an about on high alert
days. Overall, I think the model shows that reductions in crime due to
more police being out is actually caused by raised terrorist threat
levels.

Clustering and PCA
==================

Our data set of various bottles of wine has descriptive properties that
include 11 chemical properties and two other variables, color and
quality (on a 1-10 scale). The goal was to find a model that could
distinguish red wines from white wines, and potentially even sort the
higher from the lower quality wines. Below is the summary of the
dataset.

    ##  fixed.acidity    volatile.acidity  citric.acid     residual.sugar  
    ##  Min.   : 3.800   Min.   :0.0800   Min.   :0.0000   Min.   : 0.600  
    ##  1st Qu.: 6.400   1st Qu.:0.2300   1st Qu.:0.2500   1st Qu.: 1.800  
    ##  Median : 7.000   Median :0.2900   Median :0.3100   Median : 3.000  
    ##  Mean   : 7.215   Mean   :0.3397   Mean   :0.3186   Mean   : 5.443  
    ##  3rd Qu.: 7.700   3rd Qu.:0.4000   3rd Qu.:0.3900   3rd Qu.: 8.100  
    ##  Max.   :15.900   Max.   :1.5800   Max.   :1.6600   Max.   :65.800  
    ##    chlorides       free.sulfur.dioxide total.sulfur.dioxide    density      
    ##  Min.   :0.00900   Min.   :  1.00      Min.   :  6.0        Min.   :0.9871  
    ##  1st Qu.:0.03800   1st Qu.: 17.00      1st Qu.: 77.0        1st Qu.:0.9923  
    ##  Median :0.04700   Median : 29.00      Median :118.0        Median :0.9949  
    ##  Mean   :0.05603   Mean   : 30.53      Mean   :115.7        Mean   :0.9947  
    ##  3rd Qu.:0.06500   3rd Qu.: 41.00      3rd Qu.:156.0        3rd Qu.:0.9970  
    ##  Max.   :0.61100   Max.   :289.00      Max.   :440.0        Max.   :1.0390  
    ##        pH          sulphates         alcohol         quality        color     
    ##  Min.   :2.720   Min.   :0.2200   Min.   : 8.00   Min.   :3.000   red  :1599  
    ##  1st Qu.:3.110   1st Qu.:0.4300   1st Qu.: 9.50   1st Qu.:5.000   white:4898  
    ##  Median :3.210   Median :0.5100   Median :10.30   Median :6.000               
    ##  Mean   :3.219   Mean   :0.5313   Mean   :10.49   Mean   :5.818               
    ##  3rd Qu.:3.320   3rd Qu.:0.6000   3rd Qu.:11.30   3rd Qu.:6.000               
    ##  Max.   :4.010   Max.   :2.0000   Max.   :14.90   Max.   :9.000

K-means++
=========

First, the clusterning method of K-means++ was used to assign each wine
bottle to a common centroid. This was used instead of the basic K-means
clustering because K-means++ uses the bias of distance when choosing the
starting centroid points, which helps reduce final cluster errors. To
find out how many k number of clusters will best fit the data, we looked
at a plot of trial k’s and their assocaited SSE’s, which describes how
well using that number of k-means fits the data.

![](Figs/unnamed-chunk-9-1.png)

Looking at the plot above, the “elbow” point is estimated to be about 5,
which is the reason that k=5 clusters was chosen. After running the wine
bottle data through the K-means++ algorithm using 5 clusters, each
cluster’s average wine bottle was found and the chemical properties of
those 5 bottles were determined:

    ##   fixed acity volatile acidity citric acid residual sugar  chlorides
    ## 1  6.73443971       31.9497564  10.1488205     0.07914152  0.5932674
    ## 2  0.25880633      135.9619367   7.2877211    16.40530697 10.2535727
    ## 3  0.31523143        0.9937968   0.6162227    50.30072841  7.2877211
    ## 4  3.84704629        3.2598112   0.1329657     0.99609555  0.6162227
    ## 5  0.05012363        0.5100609   2.4723205     3.37497399  0.1329657
    ##   free sulfur dioxide total sulfur oxide     density         pH   sulphates
    ## 1          2.47232050          3.3749740  0.13296566  0.9960955  0.61622268
    ## 2          0.07914152          0.5932674  2.47232050  3.3749740  0.13296566
    ## 3         16.40530697         10.2535727  0.07914152  0.5932674  2.47232050
    ## 4         50.30072841          7.2877211 16.40530697 10.2535727  0.07914152
    ## 5          0.99609555          0.6162227 50.30072841  7.2877211 16.40530697
    ##      alcohol
    ## 1 50.3007284
    ## 2  0.9960955
    ## 3  3.3749740
    ## 4  0.5932674
    ## 5 10.2535727

To determine whether K-means successfully formed reasonable clusters of
wine, we looked at single plots of each cluster. We were able to roughly
visualize the results of our clustering approach by looking at the
clusters on a few of the chemical properties.
![](Figs/unnamed-chunk-11-1.png)![](Figs/unnamed-chunk-11-2.png)

Looking at the two plots above, each cluster seemed to be relatively
centrally located in a specific region of each plot, which lead us to
believe that K-means++ created reasonable clusters of wines from the
data. To see if the clustering method could distinguish red wines from
white wines, single clusters were looked at, with color determining
whether the observations in that cluster were either a red or a white
wine.

![](Figs/unnamed-chunk-12-1.png)![](Figs/unnamed-chunk-12-2.png)![](Figs/unnamed-chunk-12-3.png)![](Figs/unnamed-chunk-12-4.png)![](Figs/unnamed-chunk-12-5.png)
From the graphs above, clusters 1, 2, and 4 are all predominantly
saturated with white wines, while clusters 3 and 5 contain nearly all
red wines. This was a good indicator that K-means++ performs well when
sorting wine by color.

PCA
---

Secondly, instead of clustering to sort the wine bottles in our data, we
have created a principal component analysis (PCA) to reduce the number
of variables used when describing the data and distinguishing the
observations. From the original chemical elements, the PCA algorithm
created 11 new summary variables variables, named PC1 to PC11.

    ## Importance of components:
    ##                           PC1    PC2    PC3     PC4     PC5     PC6     PC7
    ## Standard deviation     1.7407 1.5792 1.2475 0.98517 0.84845 0.77930 0.72330
    ## Proportion of Variance 0.2754 0.2267 0.1415 0.08823 0.06544 0.05521 0.04756
    ## Cumulative Proportion  0.2754 0.5021 0.6436 0.73187 0.79732 0.85253 0.90009
    ##                            PC8     PC9   PC10    PC11
    ## Standard deviation     0.70817 0.58054 0.4772 0.18119
    ## Proportion of Variance 0.04559 0.03064 0.0207 0.00298
    ## Cumulative Proportion  0.94568 0.97632 0.9970 1.00000

Each summary variable is a linear combination that maximizes the amount
of variability retained from the original data. Combined, the first four
of our summary variables explain about 73% of the variation in our data.
The linear combinations of these components are:

    ##                        PC1   PC2   PC3   PC4
    ## fixed.acidity        -0.24  0.34 -0.43  0.16
    ## volatile.acidity     -0.38  0.12  0.31  0.21
    ## citric.acid           0.15  0.18 -0.59 -0.26
    ## residual.sugar        0.35  0.33  0.16  0.17
    ## chlorides            -0.29  0.32  0.02 -0.24
    ## free.sulfur.dioxide   0.43  0.07  0.13 -0.36
    ## total.sulfur.dioxide  0.49  0.09  0.11 -0.21
    ## density              -0.04  0.58  0.18  0.07
    ## pH                   -0.22 -0.16  0.46 -0.41
    ## sulphates            -0.29  0.19 -0.07 -0.64
    ## alcohol              -0.11 -0.47 -0.26 -0.11

To understand how well PCA performs at identifying similar wines, we
looked at plots of our top three summary variables.

![](Figs/unnamed-chunk-15-1.png)![](Figs/unnamed-chunk-15-2.png)![](Figs/unnamed-chunk-15-3.png)
In two out of our three graphs, PV1 v PV2 and PV1 v PV3, the
observations seem to cluster by wine color pretty well in their own
regions. The third graph of PV2 v PV3 still shows significant clustering
among wine colors, except the overlapping of the clusters makes it
harder to 100% tell how significant the clusters are. Overall, PCA has
shown to perform well in sorting the data. Regarding the actual values
of our summary variables, PC1 looks to be positive for white wines and
negative for red wines. For PC2, it seems that half of each color
cluster is positive and half is megative. The same goes for PC3.

### Which dimensionality technique makes more sense to you for this data?

The dimensionality reduction technique that makes the most sense to me
for this data is K-means++ clustering. The single cluster plots showing
which points in each cluster were white annd red showed the high
accuracy that the technique had on distinguishing out data. Although PCA
is helpful since it reduces the amount of noise created by variables, I
had a hard time determining whether its performance was adequate.

### Convince yourself that your chosen method is easily capable of distinguishing the reds from the whites. Does this technique also seem capable of sorting the higher from the lower quality wine?

The visuals of red and white wines in each cluster frome earlier has
convinced me that K-means++ is easily capable of distinguishing the reds
from the whites. To see whether this method is also capable of sorting
the higher from the lower quality wines, I will recreate the plot from
before, except labeling each point by quality instead of color.

![](Figs/unnamed-chunk-16-1.png)![](Figs/unnamed-chunk-16-2.png)![](Figs/unnamed-chunk-16-3.png)![](Figs/unnamed-chunk-16-4.png)![](Figs/unnamed-chunk-16-5.png)

This clustering method does not seem to distinguish higher quality and
lower quality wines very well. Each cluster has a mix of wines of all
quality types. However, thepattern that higher quality wines typically
have a higher alcohol concentration and a lower density than lower
quality wines can be observed. It is highly possible that there is too
much noise in the data set dor clustering to be succeddult. In that
case, using PCA might have been a better option for sorting by quality.
Another explanation could be that the qualities of the wines may be
influenced more by personal preference of those who rated them than the
other variables, which may explain why K-means++ was not able to to use
the 11 chemical variables to distinguish quality.

Market segmentation
===================

The social marketing data collected by NutrientH20’s advertizing firm
contains 36 categories that single tweets were categorized into. Our
goal was to analyze the data and give feedback to the firm if any
interesting details regarding market segmentations were found. Market
segments can be described as a subgroups of a population that consists
of peoople with similar cahractereistics related to that market. Since
it is a nutrition company, we are focused on discovering groupings of
categories that may be associated with interest in nutrition. Before we
could decide in which direction to go to analyze the data, we altered
the original dataset, changing each entry from a count to a frequency so
we could see the proportions of categories that each user tweeted about.
Since the “spam” and “adult” categories are not of high interest to the
company, those categories were removed when calculating each frequency.

    ##      chatter current_events     travel photo_sharing uncategorized    tv_film
    ## 1 0.03278689     0.00000000 0.03278689    0.03278689    0.03278689 0.01639344
    ## 2 0.10000000     0.10000000 0.06666667    0.03333333    0.03333333 0.03333333
    ## 3 0.12765957     0.06382979 0.08510638    0.06382979    0.02127660 0.10638298
    ## 4 0.04761905     0.23809524 0.09523810    0.09523810    0.00000000 0.04761905
    ## 5 0.16666667     0.06666667 0.00000000    0.20000000    0.03333333 0.00000000
    ## 6 0.17647059     0.11764706 0.05882353    0.20588235    0.00000000 0.02941176
    ##   sports_fandom   politics       food     family home_and_garden      music
    ## 1    0.01639344 0.00000000 0.06557377 0.01639344      0.03278689 0.00000000
    ## 2    0.13333333 0.03333333 0.06666667 0.06666667      0.03333333 0.00000000
    ## 3    0.00000000 0.04255319 0.02127660 0.02127660      0.02127660 0.02127660
    ## 4    0.00000000 0.04761905 0.00000000 0.04761905      0.00000000 0.00000000
    ## 5    0.00000000 0.06666667 0.00000000 0.03333333      0.00000000 0.00000000
    ## 6    0.02941176 0.00000000 0.05882353 0.02941176      0.02941176 0.02941176
    ##        news online_gaming   shopping college_uni sports_playing    cooking
    ## 1 0.0000000           0.0 0.01639344  0.00000000     0.03278689 0.08196721
    ## 2 0.0000000           0.0 0.00000000  0.00000000     0.03333333 0.00000000
    ## 3 0.0212766           0.0 0.04255319  0.00000000     0.00000000 0.04255319
    ## 4 0.0000000           0.0 0.00000000  0.04761905     0.00000000 0.00000000
    ## 5 0.0000000           0.1 0.06666667  0.13333333     0.00000000 0.03333333
    ## 6 0.0000000           0.0 0.14705882  0.00000000     0.00000000 0.00000000
    ##          eco  computers   business   outdoors     crafts automotive       art
    ## 1 0.01639344 0.01639344 0.00000000 0.03278689 0.01639344 0.00000000 0.0000000
    ## 2 0.00000000 0.00000000 0.03333333 0.00000000 0.06666667 0.00000000 0.0000000
    ## 3 0.02127660 0.00000000 0.00000000 0.00000000 0.04255319 0.00000000 0.1702128
    ## 4 0.00000000 0.00000000 0.04761905 0.00000000 0.14285714 0.00000000 0.0952381
    ## 5 0.00000000 0.03333333 0.00000000 0.03333333 0.00000000 0.00000000 0.0000000
    ## 6 0.00000000 0.02941176 0.02941176 0.00000000 0.00000000 0.02941176 0.0000000
    ##     religion     beauty  parenting     dating    school personal_fitness
    ## 1 0.01639344 0.00000000 0.01639344 0.01639344 0.0000000        0.1803279
    ## 2 0.00000000 0.00000000 0.00000000 0.03333333 0.1333333        0.0000000
    ## 3 0.00000000 0.02127660 0.00000000 0.02127660 0.0000000        0.0000000
    ## 4 0.00000000 0.04761905 0.00000000 0.00000000 0.0000000        0.0000000
    ## 5 0.00000000 0.00000000 0.00000000 0.00000000 0.0000000        0.0000000
    ## 6 0.00000000 0.00000000 0.00000000 0.00000000 0.0000000        0.0000000
    ##     fashion small_business
    ## 1 0.0000000     0.00000000
    ## 2 0.0000000     0.00000000
    ## 3 0.0212766     0.00000000
    ## 4 0.0000000     0.00000000
    ## 5 0.0000000     0.03333333
    ## 6 0.0000000     0.00000000

The summary of the data above can be used to get a rough idea of how
often each interest/category was mentioned. The category that had the
highest frequency of being categoriezd into it was “chatter”. This does
not come as a surprise since social media is heavily used to keep in
contact with or to “chatter” with others. The chatter frequencies among
the observed twitter users is summarized below.

Chatter: `max`

This observation provides little to no useful insight on potential
market segments that could be used in the designing of NutrientH2O’s
advertizing strategies.

We determined that principal component analysis could be effective in
reducing the 34 categories we were considering into just a few summary
variables. These PC variables retain the maximum variance from the data
set they are pulled from, and allowed us to categorize the main types of
audiences that follow NutrientH2O’s twitter account. Becuase

    ## Importance of components:
    ##                           PC1     PC2     PC3     PC4     PC5     PC6     PC7
    ## Standard deviation     0.1009 0.07843 0.07524 0.06786 0.05696 0.05194 0.05180
    ## Proportion of Variance 0.1771 0.10706 0.09851 0.08015 0.05645 0.04695 0.04669
    ## Cumulative Proportion  0.1771 0.28415 0.38266 0.46281 0.51926 0.56621 0.61290
    ##                           PC8     PC9    PC10    PC11    PC12    PC13    PC14
    ## Standard deviation     0.0483 0.04386 0.03954 0.03783 0.03597 0.03542 0.03373
    ## Proportion of Variance 0.0406 0.03349 0.02721 0.02490 0.02252 0.02183 0.01980
    ## Cumulative Proportion  0.6535 0.68699 0.71420 0.73910 0.76163 0.78345 0.80325
    ##                           PC15    PC16    PC17    PC18    PC19    PC20    PC21
    ## Standard deviation     0.03098 0.03044 0.02940 0.02806 0.02717 0.02676 0.02599
    ## Proportion of Variance 0.01670 0.01613 0.01505 0.01370 0.01285 0.01247 0.01175
    ## Cumulative Proportion  0.81995 0.83608 0.85113 0.86483 0.87768 0.89014 0.90190
    ##                           PC22    PC23    PC24    PC25    PC26    PC27    PC28
    ## Standard deviation     0.02523 0.02472 0.02399 0.02386 0.02320 0.02269 0.02239
    ## Proportion of Variance 0.01107 0.01064 0.01002 0.00990 0.00937 0.00896 0.00873
    ## Cumulative Proportion  0.91297 0.92361 0.93363 0.94353 0.95290 0.96186 0.97059
    ##                           PC29    PC30    PC31    PC32    PC33
    ## Standard deviation     0.02140 0.02061 0.01962 0.01741 0.01092
    ## Proportion of Variance 0.00797 0.00739 0.00670 0.00528 0.00207
    ## Cumulative Proportion  0.97856 0.98595 0.99265 0.99793 1.00000

All 34 summary variable have been calculated. The first six component
variables describe about 56%% of the variance in our data. More
specifically, we observed and evaluated the first three, PC1, PC2, and
PC3, which combine to explain almost 40% of the data, to evaulate any
market segmentations.

    ##                      PC1     PC2     PC3
    ## chatter           0.8514 -0.1159  0.0660
    ## current_events    0.0770 -0.0579  0.0050
    ## travel           -0.0513 -0.2924 -0.0480
    ## photo_sharing     0.3310  0.2462 -0.1170
    ## uncategorized     0.0167  0.0077  0.0069
    ## tv_film          -0.0329 -0.0379  0.1003
    ## sports_fandom    -0.0968 -0.1276 -0.0444
    ## politics         -0.1095 -0.5367 -0.1516
    ## food             -0.0985 -0.0324 -0.0222
    ## family           -0.0165 -0.0282 -0.0002
    ## home_and_garden   0.0059 -0.0053 -0.0016
    ## music             0.0023  0.0242  0.0193
    ## news             -0.1075 -0.3050 -0.0996
    ## online_gaming    -0.0887  0.1100  0.5621
    ## shopping          0.2162  0.0350 -0.0213
    ## college_uni      -0.0979  0.1146  0.6668
    ## sports_playing   -0.0150  0.0257  0.1090
    ## cooking          -0.1332  0.5432 -0.3382
    ## eco               0.0116  0.0032 -0.0080
    ## computers        -0.0192 -0.0942 -0.0321
    ## business          0.0122 -0.0063 -0.0042
    ## outdoors         -0.0573  0.0234 -0.0467
    ## crafts           -0.0026 -0.0071 -0.0024
    ## automotive       -0.0150 -0.1164 -0.0283
    ## art              -0.0452  0.0011  0.0375
    ## religion         -0.0953 -0.0384 -0.0309
    ## beauty           -0.0315  0.1381 -0.0908
    ## parenting        -0.0607 -0.0353 -0.0340
    ## dating            0.0060 -0.0047 -0.0041
    ## school           -0.0195 -0.0053 -0.0298
    ## personal_fitness -0.0949  0.1294 -0.1130
    ## fashion          -0.0333  0.2277 -0.1294
    ## small_business    0.0027 -0.0040  0.0109

We then plotted each pair of components against each other and have
color-labeled each point based on its associated “health and nutrition”
frequency. By doing this, we are able to identify what other categories
are mentioned by twitter users who are interested in health and
nutrition.

![](Figs/unnamed-chunk-20-1.png)![](Figs/unnamed-chunk-20-2.png)![](Figs/unnamed-chunk-20-3.png)

Each pairs-model shows distinguishable clustering of frequency rates for
heath and nutrition related tweets. Out first summary variable, PC1, has
the highest health and nutrition frequency observations as typically
being negative. The second component identifies most of these high
frequency observations as being slightly above zero. For PC3 the high
frequencies tend to be slightly below zero. These models infer that the
PCA method has performed moderately well at distinguishing twitter users
by health and nutrition frequency. The clusters of the high frequencies
are didentifiable, but not enough to make strong claims. From here, we
can look at the top categories that are the most significant of each PC.

    ## [1] "chatter"        "photo_sharing"  "shopping"       "current_events"
    ## [5] "uncategorized"

    ## [1] "cooking"          "photo_sharing"    "fashion"          "beauty"          
    ## [5] "personal_fitness"

    ## [1] "college_uni"    "online_gaming"  "sports_playing" "tv_film"       
    ## [5] "chatter"

    ## PC1: #1 chatter  #2 photo_sharing  #3 shopping  #4  current_events

    ## PC2: #1 cooking  #2 photo_sharing  #3 fashion  #4  beauty

    ## PC3: #1 college_uni  #2 online_gaming  #3 sports_playing  #4  tv_film

The most significant market segment that may be used to predict health
and nutrition interest includes chatter, photo sharing, shopping, and
current events, and it accounts for amost 18% of the data collected. The
second most influential market segment consists of those who tweet about
cooking, photo sharing, fashion, and beauty. Another market segment is
identified by college status, online gaming, playing sports, and
TV/film. These can be used to generalize specific target audiences and
use social media advertizing strategies to reach them.
