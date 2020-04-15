    library(tidyverse)
    library(mosaic)
    library(dplyr)

Predictive Model Building
=========================

I am going to use different predictivve modeling techniques to find the best model for this data (simple linear model then forward something then KNN)
------------------------------------------------------------------------------------------------------------------------------------------------------

### First: Basic linear model

First, I created a linear model using the variables that I believed have
the largest influence on the price of rent of the apartment buildings in
the data set.

    ## 
    ## Call:
    ## lm(formula = Rent ~ age + renovated + LEED + Energystar + class_a + 
    ##     cluster, data = buildings_train)
    ## 
    ## Coefficients:
    ## (Intercept)          age    renovated         LEED   Energystar      class_a  
    ##   21.041188     0.029414    -2.835463     1.614511    -2.001018     7.469907  
    ##     cluster  
    ##    0.006874

    ## 
    ## Call:
    ## lm(formula = Rent ~ age + renovated + LEED + Energystar + class_a + 
    ##     cluster, data = buildings_train)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -28.685  -8.619  -2.399   5.270 214.869 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 21.0411875  0.5347583  39.347  < 2e-16 ***
    ## age          0.0294144  0.0070542   4.170 3.09e-05 ***
    ## renovated   -2.8354632  0.4101104  -6.914 5.18e-12 ***
    ## LEED         1.6145111  2.1611462   0.747  0.45505    
    ## Energystar  -2.0010177  0.6732006  -2.972  0.00297 ** 
    ## class_a      7.4699066  0.4222225  17.692  < 2e-16 ***
    ## cluster      0.0068743  0.0004389  15.662  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 13.92 on 6308 degrees of freedom
    ## Multiple R-squared:  0.093,  Adjusted R-squared:  0.09213 
    ## F-statistic: 107.8 on 6 and 6308 DF,  p-value: < 2.2e-16

    ##                    2.5 %       97.5 %
    ## (Intercept) 19.992879267 22.089495755
    ## age          0.015585826  0.043242921
    ## renovated   -3.639419078 -2.031507380
    ## LEED        -2.622070591  5.851092798
    ## Energystar  -3.320719815 -0.681315671
    ## class_a      6.642206782  8.297606340
    ## cluster      0.006013858  0.007734714

![](HW--3---markdown_files/figure-markdown_strict/unnamed-chunk-2-1.png)![](HW--3---markdown_files/figure-markdown_strict/unnamed-chunk-2-2.png)![](HW--3---markdown_files/figure-markdown_strict/unnamed-chunk-2-3.png)![](HW--3---markdown_files/figure-markdown_strict/unnamed-chunk-2-4.png)

    ##  result 
    ## 14.3941

![](HW--3---markdown_files/figure-markdown_strict/unnamed-chunk-2-5.png)
