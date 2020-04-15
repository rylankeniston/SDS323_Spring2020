Predictive Model Building
=========================

I am going to use different predictivve modeling techniques to find the best model for this data (simple linear model then forward something then KNN)
------------------------------------------------------------------------------------------------------------------------------------------------------

### First: Basic linear model

First, I created a linear model using the variables that I believed have
the largest influence on the price of rent of the apartment buildings in
the data set.

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

    ## 
    ## Call:
    ## lm(formula = Rent ~ age + renovated + LEED + Energystar + class_a + 
    ##     cluster, data = buildings_train)
    ## 
    ## Coefficients:
    ## (Intercept)          age    renovated         LEED   Energystar      class_a  
    ##    21.61060      0.02847     -3.13721      1.62593     -1.76803      7.32996  
    ##     cluster  
    ##     0.00649

    ## 
    ## Call:
    ## lm(formula = Rent ~ age + renovated + LEED + Energystar + class_a + 
    ##     cluster, data = buildings_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -28.663  -8.563  -2.461   4.984 219.575 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 21.610599   0.554289  38.988  < 2e-16 ***
    ## age          0.028469   0.007356   3.870  0.00011 ***
    ## renovated   -3.137214   0.425825  -7.367 1.96e-13 ***
    ## LEED         1.625926   2.282231   0.712  0.47623    
    ## Energystar  -1.768027   0.694812  -2.545  0.01096 *  
    ## class_a      7.329964   0.439863  16.664  < 2e-16 ***
    ## cluster      0.006490   0.000460  14.108  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 14.53 on 6308 degrees of freedom
    ## Multiple R-squared:  0.08382,    Adjusted R-squared:  0.08295 
    ## F-statistic: 96.19 on 6 and 6308 DF,  p-value: < 2.2e-16

    ##                    2.5 %       97.5 %
    ## (Intercept) 20.524003843 22.697193472
    ## age          0.014047777  0.042889660
    ## renovated   -3.971974971 -2.302452248
    ## LEED        -2.848023532  6.099875618
    ## Energystar  -3.130095498 -0.405959108
    ## class_a      6.467683452  8.192243996
    ## cluster      0.005588086  0.007391683

![](HW--3-code_files/figure-markdown_strict/unnamed-chunk-1-1.png)![](HW--3-code_files/figure-markdown_strict/unnamed-chunk-1-2.png)![](HW--3-code_files/figure-markdown_strict/unnamed-chunk-1-3.png)![](HW--3-code_files/figure-markdown_strict/unnamed-chunk-1-4.png)

    ##   result 
    ## 14.33506

![](HW--3-code_files/figure-markdown_strict/unnamed-chunk-1-5.png)
