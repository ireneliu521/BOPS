Logit & Probit Model (Returns)
------------------------------

``` r
#Reading Data
BOPS<-read.csv("Monthly Sales Data_Final.csv")
summary(BOPS)
```

    ##        X           store_number     summary        month_index  
    ##  Min.   :   1.0   Min.   :   2   Min.   : 1.000   Min.   :13.0  
    ##  1st Qu.: 270.2   1st Qu.:   2   1st Qu.: 4.000   1st Qu.:19.0  
    ##  Median : 539.5   Median :   6   Median : 9.000   Median :25.0  
    ##  Mean   : 539.5   Mean   :1677   Mean   : 9.356   Mean   :25.4  
    ##  3rd Qu.: 808.8   3rd Qu.:5998   3rd Qu.:13.000   3rd Qu.:31.0  
    ##  Max.   :1078.0   Max.   :5998   Max.   :21.000   Max.   :37.0  
    ##                                                                 
    ##  monthly_sales          BOPS            month          year     
    ##  Min.   :     19   Min.   :0.0000   AUG    :122   Min.   :2010  
    ##  1st Qu.:   9746   1st Qu.:0.0000   DEC    : 92   1st Qu.:2011  
    ##  Median :  29009   Median :0.0000   JAN    : 90   Median :2011  
    ##  Mean   : 166785   Mean   :0.3738   JUL    : 90   Mean   :2011  
    ##  3rd Qu.: 174640   3rd Qu.:1.0000   JUN    : 90   3rd Qu.:2012  
    ##  Max.   :4727543   Max.   :1.0000   FEB    : 89   Max.   :2012  
    ##                                     (Other):505                 
    ##    treatment          bridal      
    ##  Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :1.0000   Median :0.0000  
    ##  Mean   :0.7208   Mean   :0.4007  
    ##  3rd Qu.:1.0000   3rd Qu.:1.0000  
    ##  Max.   :1.0000   Max.   :1.0000  
    ## 

``` r
Return<-read.csv("Transaction data merged.csv")
summary(Return)
```

    ##        X            customer_id                   purchase_date    
    ##  Min.   :      1   Min.   :1.003e+05   13DEC2012:00:00:00:  12989  
    ##  1st Qu.: 417876   1st Qu.:2.569e+07   12DEC2012:00:00:00:  12286  
    ##  Median : 835752   Median :3.015e+07   18DEC2012:00:00:00:  12234  
    ##  Mean   : 835752   Mean   :2.944e+10   06DEC2012:00:00:00:  11614  
    ##  3rd Qu.:1253627   3rd Qu.:3.499e+07   11DEC2012:00:00:00:  10228  
    ##  Max.   :1671502   Max.   :9.197e+11   22DEC2011:00:00:00:   9896  
    ##                                        (Other)           :1602255  
    ##  transaction_id     store_number    net_purchase_amount      sku          
    ##  Min.   :   7198   Min.   :   2.0   Min.   :    0.00    Min.   :10033405  
    ##  1st Qu.:2649367   1st Qu.:   2.0   1st Qu.:   45.13    1st Qu.:17859869  
    ##  Median :3355444   Median :   2.0   Median :   90.00    Median :18126698  
    ##  Mean   :3338930   Mean   : 229.5   Mean   :  170.33    Mean   :18300993  
    ##  3rd Qu.:4030256   3rd Qu.:   2.0   3rd Qu.:  189.00    3rd Qu.:18584417  
    ##  Max.   :4702552   Max.   :5998.0   Max.   :39422.00    Max.   :80006100  
    ##                                                                           
    ##      return                  return_date       return_store    
    ##  Min.   :0.000                     :1502656   Min.   :   2.0   
    ##  1st Qu.:0.000   02JUN2011:00:00:00:    921   1st Qu.:   2.0   
    ##  Median :0.000   21JUL2011:00:00:00:    803   Median :   2.0   
    ##  Mean   :0.101   25APR2012:00:00:00:    802   Mean   : 756.7   
    ##  3rd Qu.:0.000   10JAN2013:00:00:00:    781   3rd Qu.:1479.0   
    ##  Max.   :1.000   08JAN2013:00:00:00:    744   Max.   :5998.0   
    ##                  (Other)           : 164795   NA's   :1502656  
    ##  time_to_return    gender        age_band     est_income_code
    ##  Min.   :   0.0     :210507   Min.   : 0.00   Min.   :1.00   
    ##  1st Qu.:   8.0    F:693941   1st Qu.: 0.00   1st Qu.:4.00   
    ##  Median :  17.0    M:719292   Median : 5.00   Median :6.00   
    ##  Mean   :  27.8    U: 47762   Mean   : 4.95   Mean   :5.42   
    ##  3rd Qu.:  33.0               3rd Qu.: 8.00   3rd Qu.:7.00   
    ##  Max.   :1679.0               Max.   :13.00   Max.   :9.00   
    ##  NA's   :1502656              NA's   :72038   NA's   :68664  
    ##   ethnic_code     homeowner_code length_of_residence child     
    ##  N      :615387    :  68664      Min.   : 0.00        : 68664  
    ##  S      :204830   O:1064498      1st Qu.: 2.00       N:977479  
    ##  H      :187647   R: 538340      Median : 6.00       Y:625359  
    ##  Z      :161313                  Mean   : 7.14                 
    ##  G      :120011                  3rd Qu.:13.00                 
    ##  U      : 71027                  Max.   :15.00                 
    ##  (Other):311287                  NA's   :68664                 
    ##       year          month         month_index       summary     
    ##  Min.   :2010   DEC    :425369   Min.   :13.00   Min.   : 1.00  
    ##  1st Qu.:2011   NOV    :187468   1st Qu.:22.00   1st Qu.: 5.00  
    ##  Median :2012   FEB    :179716   Median :31.00   Median : 9.00  
    ##  Mean   :2012   MAY    :143596   Mean   :31.47   Mean   :10.07  
    ##  3rd Qu.:2012   JAN    :127777   3rd Qu.:41.00   3rd Qu.:12.00  
    ##  Max.   :2013   APR    :102339   Max.   :48.00   Max.   :21.00  
    ##                 (Other):505237                   NA's   :4      
    ##       fy12              fy13       
    ##  Min.   :0.00000   Min.   :0.0000  
    ##  1st Qu.:0.00000   1st Qu.:0.0000  
    ##  Median :0.00000   Median :0.0000  
    ##  Mean   :0.05689   Mean   :0.1095  
    ##  3rd Qu.:0.00000   3rd Qu.:0.0000  
    ##  Max.   :1.00000   Max.   :1.0000  
    ## 

``` r
#Cleaning Data
return<-Return[!(is.na(Return$age_band)),]
return<-return[!(is.na(return$est_income_code)),]
return<-return[!(is.na(return$length_of_residence)),]
return<-return[!(is.na(return$summary)),]
return<-return[!(return$gender=="U"),]
return<-return[!(return$net_purchase_amount==0),]

return$gender<-ifelse(return$gender=="M",1,0)
return$homeowner_code<-ifelse(return$homeowner_code=="O",1,0)
return$child<-ifelse(return$child=="Y",1,0)

return$BOPS<-return$fy12+return$fy13
return$X<-NULL

return[is.na(return)] <- " "

#return$age_band<-as.numeric(Return$age_band)
#return$est_income_code<-as.numeric(Return$est_income_code)
#return$length_of_residence<-as.numeric(Return$length_of_residence)
#return$summary<-as.numeric(Return$summary)

return$Cgroup<-ifelse(return$summary==1,1,
                     ifelse(return$summary==2,1,
                          ifelse(return$summary==20,1,
                                ifelse(return$summary==3,2,
                                      ifelse(return$summary==4,2,
                                           ifelse(return$summary==7,2,
                                                ifelse(return$summary==11,2,
                                                     ifelse(return$summary==12,2,
                                                          ifelse(return$summary==15,2,           
                                                                ifelse(return$summary==5,3,
                                                                      ifelse(return$summary==21,3,                                      
                                                                              4)))))))))))

return$Month<-ifelse(return$month=="JAN",1,
                     ifelse(return$month=="FEB",2,
                            ifelse(return$month=="MAR",3,
                                   ifelse(return$month=="APR",4,
                                          ifelse(return$month=="MAY",5,
                                              ifelse(return$month=="JUN",6,
                                                     ifelse(return$month=="JUL",7,
                                                           ifelse(return$month=="AUG",8,
                                                                ifelse(return$month=="SEP",9,
                                                                     ifelse(return$month=="OCT",10,
                                                                          ifelse(return$month=="NOV",11,
                                                                                        12)))))))))))

#Summary
hist(return$net_purchase_amount)
```

![](Irene_files/figure-markdown_github/unnamed-chunk-1-1.png)

``` r
hist(log(return$net_purchase_amount)) #use log
return$lognet_purchase_amount<-log(return$net_purchase_amount)

cor(return$homeowner_code,return$est_income_code) #0.35
```

    ## [1] 0.355759

``` r
summary(return)
```

    ##   customer_id                   purchase_date     transaction_id   
    ##  Min.   :1.003e+05   13DEC2012:00:00:00:  12022   Min.   :   7206  
    ##  1st Qu.:2.581e+07   12DEC2012:00:00:00:  11582   1st Qu.:2639234  
    ##  Median :3.015e+07   18DEC2012:00:00:00:  11138   Median :3316969  
    ##  Mean   :3.060e+10   06DEC2012:00:00:00:  10670   Mean   :3330541  
    ##  3rd Qu.:3.490e+07   22DEC2011:00:00:00:   9382   3rd Qu.:4002518  
    ##  Max.   :9.197e+11   11DEC2012:00:00:00:   9338   Max.   :4702379  
    ##                      (Other)           :1441842                    
    ##   store_number      net_purchase_amount      sku          
    ##  Min.   :   2.000   Min.   :    0.01    Min.   :10033405  
    ##  1st Qu.:   2.000   1st Qu.:   49.00    1st Qu.:17856907  
    ##  Median :   2.000   Median :   94.99    Median :18118190  
    ##  Mean   :   4.437   Mean   :  174.07    Mean   :18282413  
    ##  3rd Qu.:   2.000   3rd Qu.:  190.48    3rd Qu.:18559310  
    ##  Max.   :5998.000   Max.   :39422.00    Max.   :40005720  
    ##                                                           
    ##      return                   return_date      return_store      
    ##  Min.   :0.0000                     :1349914   Length:1505974    
    ##  1st Qu.:0.0000   02JUN2011:00:00:00:    900   Class :character  
    ##  Median :0.0000   21JUL2011:00:00:00:    792   Mode  :character  
    ##  Mean   :0.1036   25APR2012:00:00:00:    761                     
    ##  3rd Qu.:0.0000   10JAN2013:00:00:00:    730                     
    ##  Max.   :1.0000   08JAN2013:00:00:00:    713                     
    ##                   (Other)           : 152164                     
    ##  time_to_return         gender          age_band      est_income_code
    ##  Length:1505974     Min.   :0.0000   Min.   : 0.000   Min.   :1.000  
    ##  Class :character   1st Qu.:0.0000   1st Qu.: 0.000   1st Qu.:4.000  
    ##  Mode  :character   Median :0.0000   Median : 5.000   Median :6.000  
    ##                     Mean   :0.4624   Mean   : 5.071   Mean   :5.425  
    ##                     3rd Qu.:1.0000   3rd Qu.: 8.000   3rd Qu.:7.000  
    ##                     Max.   :1.0000   Max.   :13.000   Max.   :9.000  
    ##                                                                      
    ##   ethnic_code     homeowner_code   length_of_residence     child       
    ##  N      :583396   Min.   :0.0000   Min.   : 0.00       Min.   :0.0000  
    ##  S      :194533   1st Qu.:0.0000   1st Qu.: 2.00       1st Qu.:0.0000  
    ##  H      :174091   Median :1.0000   Median : 6.00       Median :0.0000  
    ##  Z      :148988   Mean   :0.6672   Mean   : 7.17       Mean   :0.3905  
    ##  G      :114840   3rd Qu.:1.0000   3rd Qu.:13.00       3rd Qu.:1.0000  
    ##  U      : 66311   Max.   :1.0000   Max.   :15.00       Max.   :1.0000  
    ##  (Other):223815                                                        
    ##       year          month         month_index       summary     
    ##  Min.   :2010   DEC    :399820   Min.   :13.00   Min.   : 1.00  
    ##  1st Qu.:2011   NOV    :172176   1st Qu.:22.00   1st Qu.: 5.00  
    ##  Median :2012   FEB    :167100   Median :31.00   Median : 9.00  
    ##  Mean   :2012   MAY    :129747   Mean   :31.22   Mean   :10.21  
    ##  3rd Qu.:2012   JAN    :108860   3rd Qu.:41.00   3rd Qu.:13.00  
    ##  Max.   :2013   OCT    : 85378   Max.   :48.00   Max.   :21.00  
    ##                 (Other):442893                                  
    ##       fy12              fy13             BOPS           Cgroup     
    ##  Min.   :0.00000   Min.   :0.0000   Min.   :0.000   Min.   :1.000  
    ##  1st Qu.:0.00000   1st Qu.:0.0000   1st Qu.:0.000   1st Qu.:2.000  
    ##  Median :0.00000   Median :0.0000   Median :0.000   Median :2.000  
    ##  Mean   :0.06084   Mean   :0.1052   Mean   :0.166   Mean   :2.471  
    ##  3rd Qu.:0.00000   3rd Qu.:0.0000   3rd Qu.:0.000   3rd Qu.:3.000  
    ##  Max.   :1.00000   Max.   :1.0000   Max.   :1.000   Max.   :4.000  
    ##                                                                    
    ##      Month       lognet_purchase_amount
    ##  Min.   : 1.00   Min.   :-4.605        
    ##  1st Qu.: 4.00   1st Qu.: 3.892        
    ##  Median : 8.00   Median : 4.554        
    ##  Mean   : 7.51   Mean   : 4.589        
    ##  3rd Qu.:12.00   3rd Qu.: 5.250        
    ##  Max.   :12.00   Max.   :10.582        
    ## 

``` r
xtabs(~ return + BOPS, data = return)
```

    ##       BOPS
    ## return       0       1
    ##      0 1127629  222285
    ##      1  128361   27699

``` r
#Return-OLS
model0<-lm(return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return)
summary(model0)
```

    ## 
    ## Call:
    ## lm(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, data = return)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.36080 -0.12107 -0.09116 -0.05901  1.02914 
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)              -3.006e-02  2.857e-03 -10.522  < 2e-16 ***
    ## lognet_purchase_amount    3.494e-02  3.465e-04 100.830  < 2e-16 ***
    ## factor(gender)1          -2.767e-02  5.070e-04 -54.581  < 2e-16 ***
    ## age_band                  1.373e-04  6.429e-05   2.136 0.032668 *  
    ## est_income_code           2.274e-03  1.111e-04  20.477  < 2e-16 ***
    ## factor(BOPS)1             1.477e-02  6.662e-04  22.171  < 2e-16 ***
    ## factor(store_number)6    -3.415e-03  9.673e-04  -3.531 0.000415 ***
    ## factor(store_number)5998 -3.637e-02  1.294e-02  -2.811 0.004944 ** 
    ## factor(summary)2          4.970e-02  2.118e-03  23.462  < 2e-16 ***
    ## factor(summary)3         -7.693e-03  2.579e-03  -2.983 0.002855 ** 
    ## factor(summary)4         -1.840e-02  1.822e-03 -10.101  < 2e-16 ***
    ## factor(summary)5         -2.933e-02  1.871e-03 -15.674  < 2e-16 ***
    ## factor(summary)6          2.371e-02  2.349e-03  10.096  < 2e-16 ***
    ## factor(summary)7         -4.593e-02  2.251e-03 -20.408  < 2e-16 ***
    ## factor(summary)8          9.216e-02  9.139e-03  10.084  < 2e-16 ***
    ## factor(summary)9         -2.054e-02  2.481e-03  -8.278  < 2e-16 ***
    ## factor(summary)10         1.045e-01  2.379e-02   4.391 1.13e-05 ***
    ## factor(summary)11        -3.511e-02  2.277e-03 -15.414  < 2e-16 ***
    ## factor(summary)12        -2.930e-02  1.880e-03 -15.585  < 2e-16 ***
    ## factor(summary)13        -3.309e-02  2.380e-03 -13.903  < 2e-16 ***
    ## factor(summary)14         1.110e-02  2.838e-03   3.911 9.20e-05 ***
    ## factor(summary)15         7.494e-05  5.798e-02   0.001 0.998969    
    ## factor(summary)17        -3.002e-02  5.178e-03  -5.799 6.69e-09 ***
    ## factor(summary)20         4.188e-02  2.433e-03  17.211  < 2e-16 ***
    ## factor(summary)21        -2.646e-02  1.905e-03 -13.892  < 2e-16 ***
    ## Month                    -1.138e-03  6.194e-05 -18.365  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.3011 on 1505948 degrees of freedom
    ## Multiple R-squared:  0.02381,    Adjusted R-squared:  0.02379 
    ## F-statistic:  1469 on 25 and 1505948 DF,  p-value: < 2.2e-16

``` r
predictedprobability_lm<-predict(model0)
range(predictedprobability_lm)
```

    ## [1] -0.2519388  0.3608037

``` r
#the range can not be negative

#Return-Logit Ratio
a<-sum(return$return==1)
b<-sum(return$return==0)
#8 variables
print(a/8)
```

    ## [1] 19507.5

``` r
print(b/8)
```

    ## [1] 168739.2

``` r
#Logit Model
library(aod)
logit1<-glm(return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return, family="binomial")
summary(logit1)
```

    ## 
    ## Call:
    ## glm(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, family = "binomial", data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.1635  -0.4967  -0.4285  -0.3622   2.8011  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error  z value Pr(>|z|)    
    ## (Intercept)              -3.7613358  0.0293407 -128.195  < 2e-16 ***
    ## lognet_purchase_amount    0.3641270  0.0037416   97.318  < 2e-16 ***
    ## factor(gender)1          -0.2989171  0.0056485  -52.919  < 2e-16 ***
    ## age_band                  0.0011642  0.0007106    1.638 0.101368    
    ## est_income_code           0.0245533  0.0012303   19.957  < 2e-16 ***
    ## factor(BOPS)1             0.1596335  0.0071852   22.217  < 2e-16 ***
    ## factor(store_number)6    -0.0406505  0.0110070   -3.693 0.000221 ***
    ## factor(store_number)5998 -0.4128376  0.1567756   -2.633 0.008456 ** 
    ## factor(summary)2          0.5473665  0.0187653   29.169  < 2e-16 ***
    ## factor(summary)3         -0.0360564  0.0224140   -1.609 0.107691    
    ## factor(summary)4         -0.0186899  0.0162576   -1.150 0.250304    
    ## factor(summary)5         -0.1348549  0.0172518   -7.817 5.42e-15 ***
    ## factor(summary)6          0.2942750  0.0207772   14.163  < 2e-16 ***
    ## factor(summary)7         -0.7952926  0.0271023  -29.344  < 2e-16 ***
    ## factor(summary)8          0.6134323  0.0700742    8.754  < 2e-16 ***
    ## factor(summary)9         -0.1303657  0.0276037   -4.723 2.33e-06 ***
    ## factor(summary)10         0.7178547  0.1809793    3.967 7.29e-05 ***
    ## factor(summary)11        -0.1856125  0.0216703   -8.565  < 2e-16 ***
    ## factor(summary)12        -0.1416295  0.0173568   -8.160 3.35e-16 ***
    ## factor(summary)13        -0.1605009  0.0232874   -6.892 5.49e-12 ***
    ## factor(summary)14         0.2498520  0.0279416    8.942  < 2e-16 ***
    ## factor(summary)15         0.1362366  0.5446474    0.250 0.802481    
    ## factor(summary)17        -0.3083705  0.0446093   -6.913 4.76e-12 ***
    ## factor(summary)20         0.3458585  0.0204505   16.912  < 2e-16 ***
    ## factor(summary)21        -0.1240058  0.0177070   -7.003 2.50e-12 ***
    ## Month                    -0.0124147  0.0006839  -18.152  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  967982  on 1505948  degrees of freedom
    ## AIC: 968034
    ## 
    ## Number of Fisher Scoring iterations: 6

``` r
logit2<-glm(return~net_purchase_amount+gender+age_band+est_income_code+factor(BOPS)+store_number+summary+Month,data=return, family="binomial")
summary(logit2)
```

    ## 
    ## Call:
    ## glm(formula = return ~ net_purchase_amount + gender + age_band + 
    ##     est_income_code + factor(BOPS) + store_number + summary + 
    ##     Month, family = "binomial", data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -6.4685  -0.4836  -0.4506  -0.4156   2.3747  
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error  z value Pr(>|z|)    
    ## (Intercept)         -1.978e+00  9.956e-03 -198.672  < 2e-16 ***
    ## net_purchase_amount  5.844e-04  6.657e-06   87.792  < 2e-16 ***
    ## gender              -2.361e-01  5.502e-03  -42.913  < 2e-16 ***
    ## age_band            -2.278e-03  7.004e-04   -3.252  0.00115 ** 
    ## est_income_code      1.918e-02  1.218e-03   15.752  < 2e-16 ***
    ## factor(BOPS)1        8.192e-02  7.076e-03   11.577  < 2e-16 ***
    ## store_number        -5.302e-05  2.615e-05   -2.027  0.04262 *  
    ## summary             -1.473e-02  4.276e-04  -34.454  < 2e-16 ***
    ## Month               -2.056e-02  6.711e-04  -30.640  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  990247  on 1505965  degrees of freedom
    ## AIC: 990265
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
with(logit1, null.deviance - deviance)
```

    ## [1] 34938.21

``` r
with(logit1, df.null - df.residual)
```

    ## [1] 25

``` r
with(logit1, pchisq(null.deviance - deviance, df.null - df.residual, lower.tail = FALSE))
```

    ## [1] 0

``` r
#p-value=0, significant

exp(coef(logit1))
```

    ##              (Intercept)   lognet_purchase_amount          factor(gender)1 
    ##               0.02325266               1.43925692               0.74162089 
    ##                 age_band          est_income_code            factor(BOPS)1 
    ##               1.00116485               1.02485721               1.17308081 
    ##    factor(store_number)6 factor(store_number)5998         factor(summary)2 
    ##               0.96016464               0.66176977               1.72869453 
    ##         factor(summary)3         factor(summary)4         factor(summary)5 
    ##               0.96458586               0.98148365               0.87384269 
    ##         factor(summary)6         factor(summary)7         factor(summary)8 
    ##               1.34215297               0.45144912               1.84675921 
    ##         factor(summary)9        factor(summary)10        factor(summary)11 
    ##               0.87777435               2.05003054               0.83059538 
    ##        factor(summary)12        factor(summary)13        factor(summary)14 
    ##               0.86794279               0.85171707               1.28383540 
    ##        factor(summary)15        factor(summary)17        factor(summary)20 
    ##               1.14595303               0.73464307               1.41320257 
    ##        factor(summary)21                    Month 
    ##               0.88337469               0.98766209

``` r
newdata1 <- with(return,data.frame(net_purchase_amount = mean(lognet_purchase_amount), gender = mean(gender), age_band = mean(age_band), est_income_code = mean(est_income_code), store_number = mean(store_number), summary = mean(summary), Month = mean(Month), BOPS = factor(c(0,1))))

newdata1
```

    ##   net_purchase_amount   gender age_band est_income_code store_number
    ## 1            4.589477 0.462427 5.070692         5.42532     4.436687
    ## 2            4.589477 0.462427 5.070692         5.42532     4.436687
    ##    summary    Month BOPS
    ## 1 10.21452 7.510413    0
    ## 2 10.21452 7.510413    1

``` r
newdata1$BOPSP <- predict(logit2, newdata = newdata1, type = "response", se.fit=FALSE)

newdata1
```

    ##   net_purchase_amount   gender age_band est_income_code store_number
    ## 1            4.589477 0.462427 5.070692         5.42532     4.436687
    ## 2            4.589477 0.462427 5.070692         5.42532     4.436687
    ##    summary    Month BOPS      BOPSP
    ## 1 10.21452 7.510413    0 0.09136769
    ## 2 10.21452 7.510413    1 0.09840007

``` r
newdata2 <- with(return, data.frame(net_purchase_amount = rep(seq(from = 0, to = 40000, length.out = 1000), 2),
  gender = mean(gender), age_band = mean(age_band), est_income_code = mean(est_income_code), store_number = mean(store_number), summary = mean(summary), Month = mean(Month), BOPS = factor(c(0,1))))

newdata3 <- cbind(newdata2, predict(logit2, newdata = newdata2, type="link", se=TRUE))
newdata3 <- within(newdata3, {
  PredictedProb <- plogis(fit)
  LL <- plogis(fit - (1.96 * se.fit))
  UL <- plogis(fit + (1.96 * se.fit))})

head(newdata3)
```

    ##   net_purchase_amount   gender age_band est_income_code store_number
    ## 1             0.00000 0.462427 5.070692         5.42532     4.436687
    ## 2            40.04004 0.462427 5.070692         5.42532     4.436687
    ## 3            80.08008 0.462427 5.070692         5.42532     4.436687
    ## 4           120.12012 0.462427 5.070692         5.42532     4.436687
    ## 5           160.16016 0.462427 5.070692         5.42532     4.436687
    ## 6           200.20020 0.462427 5.070692         5.42532     4.436687
    ##    summary    Month BOPS       fit      se.fit residual.scale         UL
    ## 1 10.21452 7.510413    0 -2.299731 0.003301816              1 0.09168277
    ## 2 10.21452 7.510413    1 -2.194412 0.006542114              1 0.10141600
    ## 3 10.21452 7.510413    0 -2.252931 0.003111797              1 0.09562305
    ## 4 10.21452 7.510413    1 -2.147613 0.006470915              1 0.10574792
    ## 5 10.21452 7.510413    0 -2.206132 0.003005479              1 0.09972881
    ## 6 10.21452 7.510413    1 -2.100813 0.006443180              1 0.11025052
    ##           LL PredictedProb
    ## 1 0.09061059    0.09114526
    ## 2 0.09910272    0.10025343
    ## 3 0.09457335    0.09509690
    ## 4 0.10337305    0.10455453
    ## 5 0.09867601    0.09920117
    ## 6 0.10779719    0.10901780

``` r
#ggplot(newdata3, aes(x = net_purchase_amount, y = PredictedProb)) +
#  geom_ribbon(aes(ymin = LL, ymax = UL, fill = BOPS), alpha = .2) +
#  geom_line(aes(colour = BOPS), size=1)

#Check Multicollineary - No
library(VIF)
library(usdm)
```

    ## Loading required package: sp

    ## Loading required package: raster

    ## 
    ## Attaching package: 'usdm'

    ## The following object is masked from 'package:VIF':
    ## 
    ##     vif

![](Irene_files/figure-markdown_github/unnamed-chunk-1-2.png)

``` r
df<-data.frame(return$net_purchase_amount,return$gender,return$age_band,return$est_income_code,return$BOPS,return$Month)
#take factor variables out (store_number,month)
cor(df)
```

    ##                            return.net_purchase_amount return.gender
    ## return.net_purchase_amount               1.0000000000    0.09756170
    ## return.gender                            0.0975616969    1.00000000
    ## return.age_band                          0.0003710182    0.04069056
    ## return.est_income_code                  -0.0024527297    0.06457983
    ## return.BOPS                             -0.0112614092   -0.03173979
    ## return.Month                            -0.0338921618    0.04898091
    ##                            return.age_band return.est_income_code
    ## return.net_purchase_amount    0.0003710182            -0.00245273
    ## return.gender                 0.0406905558             0.06457983
    ## return.age_band               1.0000000000             0.17056570
    ## return.est_income_code        0.1705656962             1.00000000
    ## return.BOPS                  -0.0367181108            -0.01847097
    ## return.Month                  0.0592982644             0.05080511
    ##                            return.BOPS return.Month
    ## return.net_purchase_amount -0.01126141  -0.03389216
    ## return.gender              -0.03173979   0.04898091
    ## return.age_band            -0.03671811   0.05929826
    ## return.est_income_code     -0.01847097   0.05080511
    ## return.BOPS                 1.00000000  -0.01238196
    ## return.Month               -0.01238196   1.00000000

``` r
vif(df)
```

    ##                    Variables      VIF
    ## 1 return.net_purchase_amount 1.013345
    ## 2              return.gender 1.019280
    ## 3            return.age_band 1.034647
    ## 4     return.est_income_code 1.037860
    ## 5                return.BOPS 1.002388
    ## 6               return.Month 1.007942

``` r
#Interaction - No
logit2<-glm(return~factor(BOPS)*factor(Cgroup)+factor(BOPS)+lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(store_number)+factor(Cgroup),data=return, family="binomial")
summary(logit2) #factor(BOPS)*factor(Cgroup) - sig
```

    ## 
    ## Call:
    ## glm(formula = return ~ factor(BOPS) * factor(Cgroup) + factor(BOPS) + 
    ##     lognet_purchase_amount + factor(gender) + age_band + est_income_code + 
    ##     factor(store_number) + factor(Cgroup), family = "binomial", 
    ##     data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.3653  -0.4900  -0.4265  -0.3661   2.7120  
    ## 
    ## Coefficients:
    ##                                 Estimate Std. Error  z value Pr(>|z|)    
    ## (Intercept)                   -3.5800819  0.0186773 -191.681  < 2e-16 ***
    ## factor(BOPS)1                 -0.0071149  0.0186994   -0.380  0.70358    
    ## factor(Cgroup)2               -0.4985390  0.0094176  -52.937  < 2e-16 ***
    ## factor(Cgroup)3               -0.4874342  0.0100304  -48.596  < 2e-16 ***
    ## factor(Cgroup)4               -0.3009895  0.0126931  -23.713  < 2e-16 ***
    ## lognet_purchase_amount         0.3877956  0.0028052  138.241  < 2e-16 ***
    ## factor(gender)1               -0.3162343  0.0056024  -56.446  < 2e-16 ***
    ## age_band                      -0.0009188  0.0007068   -1.300  0.19361    
    ## est_income_code                0.0232227  0.0012275   18.919  < 2e-16 ***
    ## factor(store_number)6         -0.0448871  0.0109929   -4.083 4.44e-05 ***
    ## factor(store_number)5998      -0.4420847  0.1568787   -2.818  0.00483 ** 
    ## factor(BOPS)1:factor(Cgroup)2  0.1561221  0.0216240    7.220 5.20e-13 ***
    ## factor(BOPS)1:factor(Cgroup)3  0.1843194  0.0225099    8.188 2.65e-16 ***
    ## factor(BOPS)1:factor(Cgroup)4  0.1802891  0.0290310    6.210 5.29e-10 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  971817  on 1505960  degrees of freedom
    ## AIC: 971845
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
logit3<-glm(return~factor(BOPS)*factor(store_number)+factor(BOPS)+lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(store_number)+factor(Cgroup),data=return, family="binomial")
summary(logit3) #factor(BOPS)*factor(store_number) - sig
```

    ## 
    ## Call:
    ## glm(formula = return ~ factor(BOPS) * factor(store_number) + 
    ##     factor(BOPS) + lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(store_number) + factor(Cgroup), 
    ##     family = "binomial", data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.3668  -0.4898  -0.4265  -0.3663   2.8687  
    ## 
    ## Coefficients:
    ##                                          Estimate Std. Error  z value
    ## (Intercept)                            -3.6053600  0.0184928 -194.961
    ## factor(BOPS)1                           0.1433055  0.0072977   19.637
    ## factor(store_number)6                  -0.0306352  0.0115736   -2.647
    ## factor(store_number)5998               -0.2868829  0.1617701   -1.773
    ## lognet_purchase_amount                  0.3873806  0.0028027  138.215
    ## factor(gender)1                        -0.3166053  0.0056023  -56.513
    ## age_band                               -0.0009501  0.0007067   -1.344
    ## est_income_code                         0.0231677  0.0012275   18.874
    ## factor(Cgroup)2                        -0.4696920  0.0085980  -54.628
    ## factor(Cgroup)3                        -0.4539872  0.0092147  -49.268
    ## factor(Cgroup)4                        -0.2674185  0.0115037  -23.246
    ## factor(BOPS)1:factor(store_number)6    -0.1458529  0.0369676   -3.945
    ## factor(BOPS)1:factor(store_number)5998 -1.5495000  0.7303080   -2.122
    ##                                        Pr(>|z|)    
    ## (Intercept)                             < 2e-16 ***
    ## factor(BOPS)1                           < 2e-16 ***
    ## factor(store_number)6                   0.00812 ** 
    ## factor(store_number)5998                0.07616 .  
    ## lognet_purchase_amount                  < 2e-16 ***
    ## factor(gender)1                         < 2e-16 ***
    ## age_band                                0.17883    
    ## est_income_code                         < 2e-16 ***
    ## factor(Cgroup)2                         < 2e-16 ***
    ## factor(Cgroup)3                         < 2e-16 ***
    ## factor(Cgroup)4                         < 2e-16 ***
    ## factor(BOPS)1:factor(store_number)6    7.97e-05 ***
    ## factor(BOPS)1:factor(store_number)5998  0.03386 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  971868  on 1505961  degrees of freedom
    ## AIC: 971894
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
#try
logit4<-glm(return~factor(BOPS)*age_band+factor(BOPS)+lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(store_number)+factor(Cgroup),data=return, family="binomial")
summary(logit4) #factor(BOPS)*age_band - not sig
```

    ## 
    ## Call:
    ## glm(formula = return ~ factor(BOPS) * age_band + factor(BOPS) + 
    ##     lognet_purchase_amount + factor(gender) + age_band + est_income_code + 
    ##     factor(store_number) + factor(Cgroup), family = "binomial", 
    ##     data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.3684  -0.4898  -0.4265  -0.3662   2.7082  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error  z value Pr(>|z|)    
    ## (Intercept)              -3.6015867  0.0185463 -194.195  < 2e-16 ***
    ## factor(BOPS)1             0.1217796  0.0114277   10.657  < 2e-16 ***
    ## age_band                 -0.0014620  0.0007714   -1.895  0.05805 .  
    ## lognet_purchase_amount    0.3873074  0.0028027  138.190  < 2e-16 ***
    ## factor(gender)1          -0.3166672  0.0056026  -56.521  < 2e-16 ***
    ## est_income_code           0.0232088  0.0012274   18.908  < 2e-16 ***
    ## factor(store_number)6    -0.0453904  0.0109917   -4.130 3.64e-05 ***
    ## factor(store_number)5998 -0.4387998  0.1568645   -2.797  0.00515 ** 
    ## factor(Cgroup)2          -0.4694972  0.0085977  -54.607  < 2e-16 ***
    ## factor(Cgroup)3          -0.4539735  0.0092147  -49.266  < 2e-16 ***
    ## factor(Cgroup)4          -0.2673146  0.0115035  -23.238  < 2e-16 ***
    ## factor(BOPS)1:age_band    0.0032226  0.0018669    1.726  0.08431 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  971888  on 1505962  degrees of freedom
    ## AIC: 971912
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
AIC(logit1,logit2,logit3) #logit2
```

    ##        df      AIC
    ## logit1 26 968034.1
    ## logit2 14 971844.9
    ## logit3 13 971894.5

``` r
BIC(logit1,logit2,logit3) #logit2
```

    ##        df      BIC
    ## logit1 26 968351.9
    ## logit2 14 972016.1
    ## logit3 13 972053.4

``` r
#Endogeneity - (omitted variable: price sensitive customers)
library(AER)
```

    ## Loading required package: car

    ## 
    ## Attaching package: 'car'

    ## The following object is masked from 'package:usdm':
    ## 
    ##     vif

    ## The following object is masked from 'package:VIF':
    ## 
    ##     vif

    ## Loading required package: lmtest

    ## Loading required package: zoo

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

    ## Loading required package: sandwich

    ## Loading required package: survival

    ## 
    ## Attaching package: 'survival'

    ## The following object is masked from 'package:aod':
    ## 
    ##     rats

``` r
library(foreign)
df<-data.frame(return$return,return$BOPS,return$net_purchase_amount,return$gender,return$age_band,return$est_income_code,return$homeowner_code,return$length_of_residence,return$child)
cor(df)
```

    ##                            return.return return.BOPS
    ## return.return                1.000000000  0.01050394
    ## return.BOPS                  0.010503940  1.00000000
    ## return.net_purchase_amount   0.088305830 -0.01126141
    ## return.gender               -0.028025026 -0.03173979
    ## return.age_band             -0.004141329 -0.03671811
    ## return.est_income_code       0.008205077 -0.01847097
    ## return.homeowner_code       -0.003979457 -0.01902712
    ## return.length_of_residence  -0.009519720 -0.01121900
    ## return.child                -0.001182970  0.02071476
    ##                            return.net_purchase_amount return.gender
    ## return.return                            0.0883058304   -0.02802503
    ## return.BOPS                             -0.0112614092   -0.03173979
    ## return.net_purchase_amount               1.0000000000    0.09756170
    ## return.gender                            0.0975616969    1.00000000
    ## return.age_band                          0.0003710182    0.04069056
    ## return.est_income_code                  -0.0024527297    0.06457983
    ## return.homeowner_code                   -0.0096625761    0.05083119
    ## return.length_of_residence              -0.0206360086    0.02418361
    ## return.child                            -0.0222139305   -0.01770479
    ##                            return.age_band return.est_income_code
    ## return.return                -0.0041413288            0.008205077
    ## return.BOPS                  -0.0367181108           -0.018470973
    ## return.net_purchase_amount    0.0003710182           -0.002452730
    ## return.gender                 0.0406905558            0.064579830
    ## return.age_band               1.0000000000            0.170565696
    ## return.est_income_code        0.1705656962            1.000000000
    ## return.homeowner_code         0.2410726302            0.355759045
    ## return.length_of_residence    0.1622123028            0.160235066
    ## return.child                  0.0175396345            0.091726525
    ##                            return.homeowner_code
    ## return.return                       -0.003979457
    ## return.BOPS                         -0.019027118
    ## return.net_purchase_amount          -0.009662576
    ## return.gender                        0.050831190
    ## return.age_band                      0.241072630
    ## return.est_income_code               0.355759045
    ## return.homeowner_code                1.000000000
    ## return.length_of_residence           0.293794532
    ## return.child                         0.216630218
    ##                            return.length_of_residence return.child
    ## return.return                             -0.00951972  -0.00118297
    ## return.BOPS                               -0.01121900   0.02071476
    ## return.net_purchase_amount                -0.02063601  -0.02221393
    ## return.gender                              0.02418361  -0.01770479
    ## return.age_band                            0.16221230   0.01753963
    ## return.est_income_code                     0.16023507   0.09172652
    ## return.homeowner_code                      0.29379453   0.21663022
    ## return.length_of_residence                 1.00000000  -0.02857371
    ## return.child                              -0.02857371   1.00000000

``` r
model1<- ivreg(return~factor(BOPS)+lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(store_number)+factor(summary)+Month|factor(child)+length_of_residence+lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(store_number)+factor(summary)+Month,data=return)

summary(model1,diagnostics = TRUE)
```

    ## 
    ## Call:
    ## ivreg(formula = return ~ factor(BOPS) + lognet_purchase_amount + 
    ##     factor(gender) + age_band + est_income_code + factor(store_number) + 
    ##     factor(summary) + Month | factor(child) + length_of_residence + 
    ##     lognet_purchase_amount + factor(gender) + age_band + est_income_code + 
    ##     factor(store_number) + factor(summary) + Month, data = return)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -0.46223 -0.12705 -0.08120 -0.04378  1.05382 
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)              -7.085e-02  1.306e-02  -5.425 5.79e-08 ***
    ## factor(BOPS)1             1.294e-01  3.579e-02   3.614 0.000301 ***
    ## lognet_purchase_amount    3.685e-02  6.917e-04  53.270  < 2e-16 ***
    ## factor(gender)1          -2.640e-02  6.485e-04 -40.709  < 2e-16 ***
    ## age_band                  5.112e-04  1.336e-04   3.827 0.000130 ***
    ## est_income_code           2.468e-03  1.274e-04  19.377  < 2e-16 ***
    ## factor(store_number)6     5.868e-03  3.059e-03   1.918 0.055073 .  
    ## factor(store_number)5998 -3.693e-02  1.307e-02  -2.826 0.004712 ** 
    ## factor(summary)2          5.605e-02  2.916e-03  19.221  < 2e-16 ***
    ## factor(summary)3         -3.055e-03  2.980e-03  -1.025 0.305222    
    ## factor(summary)4         -7.183e-03  3.958e-03  -1.815 0.069514 .  
    ## factor(summary)5         -1.925e-02  3.670e-03  -5.246 1.56e-07 ***
    ## factor(summary)6          2.734e-02  2.628e-03  10.402  < 2e-16 ***
    ## factor(summary)7         -5.088e-02  2.748e-03 -18.517  < 2e-16 ***
    ## factor(summary)8          1.093e-01  1.066e-02  10.247  < 2e-16 ***
    ## factor(summary)9         -2.010e-02  2.509e-03  -8.014 1.12e-15 ***
    ## factor(summary)10         1.293e-01  2.524e-02   5.121 3.03e-07 ***
    ## factor(summary)11        -2.072e-02  5.048e-03  -4.104 4.06e-05 ***
    ## factor(summary)12        -2.232e-02  2.891e-03  -7.720 1.16e-14 ***
    ## factor(summary)13        -2.266e-02  4.046e-03  -5.601 2.13e-08 ***
    ## factor(summary)14         2.990e-02  6.532e-03   4.577 4.72e-06 ***
    ## factor(summary)15         2.511e-02  5.906e-02   0.425 0.670739    
    ## factor(summary)17        -3.212e-02  5.269e-03  -6.095 1.09e-09 ***
    ## factor(summary)20         4.802e-02  3.118e-03  15.403  < 2e-16 ***
    ## factor(summary)21        -1.725e-02  3.460e-03  -4.986 6.17e-07 ***
    ## Month                    -1.000e-03  7.588e-05 -13.179  < 2e-16 ***
    ## 
    ## Diagnostic tests:
    ##                      df1     df2 statistic  p-value    
    ## Weak instruments       2 1505947    266.12  < 2e-16 ***
    ## Wu-Hausman             1 1505947     10.46  0.00122 ** 
    ## Sargan                 1      NA     29.04 7.11e-08 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.3041 on 1505948 degrees of freedom
    ## Multiple R-Squared: 0.004632,    Adjusted R-squared: 0.004615 
    ## Wald test:  1422 on 25 and 1505948 DF,  p-value: < 2.2e-16

``` r
#Marginal effects
library(mfx)
```

    ## Loading required package: MASS

    ## 
    ## Attaching package: 'MASS'

    ## The following objects are masked from 'package:raster':
    ## 
    ##     area, select

    ## Loading required package: betareg

``` r
logitmfx(return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return)
```

    ## Call:
    ## logitmfx(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, data = return)
    ## 
    ## Marginal Effects:
    ##                                dF/dx   Std. Err.        z     P>|z|    
    ## lognet_purchase_amount    3.1182e-02  3.1585e-04  98.7253 < 2.2e-16 ***
    ## factor(gender)1          -2.5412e-02  4.7523e-04 -53.4726 < 2.2e-16 ***
    ## age_band                  9.9694e-05  6.0854e-05   1.6383 0.1013677    
    ## est_income_code           2.1026e-03  1.0529e-04  19.9705 < 2.2e-16 ***
    ## factor(BOPS)1             1.4278e-02  6.7014e-04  21.3056 < 2.2e-16 ***
    ## factor(store_number)6    -3.4321e-03  9.1613e-04  -3.7463 0.0001794 ***
    ## factor(store_number)5998 -2.9925e-02  9.4841e-03  -3.1553 0.0016032 ** 
    ## factor(summary)2          5.7325e-02  2.3512e-03  24.3808 < 2.2e-16 ***
    ## factor(summary)3         -3.0443e-03  1.8656e-03  -1.6318 0.1027287    
    ## factor(summary)4         -1.5917e-03  1.3770e-03  -1.1559 0.2477087    
    ## factor(summary)5         -1.1160e-02  1.3794e-03  -8.0902 5.957e-16 ***
    ## factor(summary)6          2.8228e-02  2.2172e-03  12.7313 < 2.2e-16 ***
    ## factor(summary)7         -5.1576e-02  1.2751e-03 -40.4491 < 2.2e-16 ***
    ## factor(summary)8          6.7113e-02  9.4938e-03   7.0691 1.559e-12 ***
    ## factor(summary)9         -1.0619e-02  2.1360e-03  -4.9715 6.645e-07 ***
    ## factor(summary)10         8.1792e-02  2.6288e-02   3.1114 0.0018621 ** 
    ## factor(summary)11        -1.4801e-02  1.6055e-03  -9.2192 < 2.2e-16 ***
    ## factor(summary)12        -1.1737e-02  1.3919e-03  -8.4323 < 2.2e-16 ***
    ## factor(summary)13        -1.2917e-02  1.7582e-03  -7.3466 2.034e-13 ***
    ## factor(summary)14         2.3609e-02  2.8984e-03   8.1456 3.775e-16 ***
    ## factor(summary)15         1.2329e-02  5.2003e-02   0.2371 0.8125985    
    ## factor(summary)17        -2.3324e-02  2.9568e-03  -7.8883 3.062e-15 ***
    ## factor(summary)20         3.3880e-02  2.2702e-03  14.9237 < 2.2e-16 ***
    ## factor(summary)21        -1.0300e-02  1.4262e-03  -7.2214 5.144e-13 ***
    ## Month                    -1.0631e-03  5.8532e-05 -18.1633 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## dF/dx is for discrete change for the following variables:
    ## 
    ##  [1] "factor(gender)1"          "factor(BOPS)1"           
    ##  [3] "factor(store_number)6"    "factor(store_number)5998"
    ##  [5] "factor(summary)2"         "factor(summary)3"        
    ##  [7] "factor(summary)4"         "factor(summary)5"        
    ##  [9] "factor(summary)6"         "factor(summary)7"        
    ## [11] "factor(summary)8"         "factor(summary)9"        
    ## [13] "factor(summary)10"        "factor(summary)11"       
    ## [15] "factor(summary)12"        "factor(summary)13"       
    ## [17] "factor(summary)14"        "factor(summary)15"       
    ## [19] "factor(summary)17"        "factor(summary)20"       
    ## [21] "factor(summary)21"

``` r
#Heteroscedasticity - Yes
library(lmtest)
gqtest(logit1) # Goldfeld-Quandt test indicates no heteroscedasticity
```

    ## 
    ##  Goldfeld-Quandt test
    ## 
    ## data:  logit1
    ## GQ = 0.92468, df1 = 752960, df2 = 752960, p-value = 1
    ## alternative hypothesis: variance increases from segment 1 to 2

``` r
bptest(logit1) # Breusch-Pagan test indicates heteroscedasticity
```

    ## 
    ##  studentized Breusch-Pagan test
    ## 
    ## data:  logit1
    ## BP = 34700, df = 25, p-value < 2.2e-16

``` r
#Fix
library(sandwich)
library(foreign)
logitmfx(return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+factor(month),data=return,robust=TRUE)
```

    ## Call:
    ## logitmfx(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + factor(month), data = return, robust = TRUE)
    ## 
    ## Marginal Effects:
    ##                                dF/dx   Std. Err.        z     P>|z|    
    ## lognet_purchase_amount    3.1059e-02  3.2135e-04  96.6497 < 2.2e-16 ***
    ## factor(gender)1          -2.4543e-02  4.7861e-04 -51.2797 < 2.2e-16 ***
    ## age_band                  1.2059e-04  6.0568e-05   1.9910 0.0464782 *  
    ## est_income_code           2.0158e-03  1.0509e-04  19.1824 < 2.2e-16 ***
    ## factor(BOPS)1             1.4514e-02  6.7253e-04  21.5810 < 2.2e-16 ***
    ## factor(store_number)6    -3.7439e-03  9.1023e-04  -4.1132 3.903e-05 ***
    ## factor(store_number)5998 -2.9911e-02  9.4870e-03  -3.1529 0.0016168 ** 
    ## factor(summary)2          5.6267e-02  2.3677e-03  23.7651 < 2.2e-16 ***
    ## factor(summary)3         -3.1022e-03  1.8715e-03  -1.6576 0.0973953 .  
    ## factor(summary)4         -4.9080e-04  1.4029e-03  -0.3498 0.7264578    
    ## factor(summary)5         -1.0256e-02  1.4102e-03  -7.2731 3.514e-13 ***
    ## factor(summary)6          2.8304e-02  2.2375e-03  12.6499 < 2.2e-16 ***
    ## factor(summary)7         -4.9457e-02  1.3357e-03 -37.0280 < 2.2e-16 ***
    ## factor(summary)8          6.4702e-02  9.4592e-03   6.8400 7.917e-12 ***
    ## factor(summary)9         -8.7872e-03  2.1929e-03  -4.0071 6.148e-05 ***
    ## factor(summary)10         7.6201e-02  2.6036e-02   2.9268 0.0034250 ** 
    ## factor(summary)11        -1.3640e-02  1.6307e-03  -8.3650 < 2.2e-16 ***
    ## factor(summary)12        -1.0767e-02  1.4173e-03  -7.5968 3.036e-14 ***
    ## factor(summary)13        -1.2119e-02  1.7817e-03  -6.8015 1.035e-11 ***
    ## factor(summary)14         2.2609e-02  2.8992e-03   7.7983 6.276e-15 ***
    ## factor(summary)15         1.4001e-02  5.2712e-02   0.2656 0.7905331    
    ## factor(summary)17        -2.4238e-02  2.9607e-03  -8.1864 2.692e-16 ***
    ## factor(summary)20         3.3984e-02  2.2820e-03  14.8921 < 2.2e-16 ***
    ## factor(summary)21        -9.1960e-03  1.4591e-03  -6.3027 2.925e-10 ***
    ## factor(month)AUG          8.5264e-03  1.4798e-03   5.7618 8.323e-09 ***
    ## factor(month)DEC         -1.0010e-02  1.0274e-03  -9.7436 < 2.2e-16 ***
    ## factor(month)FEB         -3.8772e-03  1.1540e-03  -3.3597 0.0007801 ***
    ## factor(month)JAN          2.0431e-02  1.4301e-03  14.2865 < 2.2e-16 ***
    ## factor(month)JUL          1.5218e-02  1.5595e-03   9.7585 < 2.2e-16 ***
    ## factor(month)JUN          1.0233e-02  1.5143e-03   6.7575 1.404e-11 ***
    ## factor(month)MAR          7.3426e-03  1.4108e-03   5.2045 1.945e-07 ***
    ## factor(month)MAY         -8.0777e-03  1.1786e-03  -6.8536 7.200e-12 ***
    ## factor(month)NOV          5.8716e-04  1.1795e-03   0.4978 0.6186103    
    ## factor(month)OCT          1.1215e-02  1.4649e-03   7.6557 1.923e-14 ***
    ## factor(month)SEP          4.3963e-03  1.4601e-03   3.0109 0.0026045 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## dF/dx is for discrete change for the following variables:
    ## 
    ##  [1] "factor(gender)1"          "factor(BOPS)1"           
    ##  [3] "factor(store_number)6"    "factor(store_number)5998"
    ##  [5] "factor(summary)2"         "factor(summary)3"        
    ##  [7] "factor(summary)4"         "factor(summary)5"        
    ##  [9] "factor(summary)6"         "factor(summary)7"        
    ## [11] "factor(summary)8"         "factor(summary)9"        
    ## [13] "factor(summary)10"        "factor(summary)11"       
    ## [15] "factor(summary)12"        "factor(summary)13"       
    ## [17] "factor(summary)14"        "factor(summary)15"       
    ## [19] "factor(summary)17"        "factor(summary)20"       
    ## [21] "factor(summary)21"        "factor(month)AUG"        
    ## [23] "factor(month)DEC"         "factor(month)FEB"        
    ## [25] "factor(month)JAN"         "factor(month)JUL"        
    ## [27] "factor(month)JUN"         "factor(month)MAR"        
    ## [29] "factor(month)MAY"         "factor(month)NOV"        
    ## [31] "factor(month)OCT"         "factor(month)SEP"

``` r
#Prediction
pred = predict(logit2, data=return)
return_prediction <- ifelse(pred >= 0.5,1,0)
misClasificError <- mean(return_prediction != return$return)
print(paste('Accuracy',1-misClasificError))
```

    ## [1] "Accuracy 0.896372712941923"

``` r
table(return$return, pred>=0.5)
```

    ##    
    ##       FALSE
    ##   0 1349914
    ##   1  156060

``` r
# Probit model
probit1<- glm(return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return, family=binomial(link="probit")) # This is the command to run a probit regression 
summary(probit1)
```

    ## 
    ## Call:
    ## glm(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, family = binomial(link = "probit"), 
    ##     data = return)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.0982  -0.4989  -0.4294  -0.3592   2.8448  
    ## 
    ## Coefficients:
    ##                            Estimate Std. Error  z value Pr(>|z|)    
    ## (Intercept)              -2.0867002  0.0155984 -133.776  < 2e-16 ***
    ## lognet_purchase_amount    0.1909827  0.0019677   97.060  < 2e-16 ***
    ## factor(gender)1          -0.1539945  0.0029235  -52.676  < 2e-16 ***
    ## age_band                  0.0004790  0.0003687    1.299 0.193914    
    ## est_income_code           0.0128334  0.0006380   20.115  < 2e-16 ***
    ## factor(BOPS)1             0.0863040  0.0037618   22.942  < 2e-16 ***
    ## factor(store_number)6    -0.0219783  0.0056607   -3.883 0.000103 ***
    ## factor(store_number)5998 -0.2069866  0.0783826   -2.641 0.008273 ** 
    ## factor(summary)2          0.2844931  0.0104766   27.155  < 2e-16 ***
    ## factor(summary)3         -0.0231000  0.0125966   -1.834 0.066680 .  
    ## factor(summary)4         -0.0261801  0.0090428   -2.895 0.003790 ** 
    ## factor(summary)5         -0.0857045  0.0094719   -9.048  < 2e-16 ***
    ## factor(summary)6          0.1544633  0.0116097   13.305  < 2e-16 ***
    ## factor(summary)7         -0.3698521  0.0133070  -27.794  < 2e-16 ***
    ## factor(summary)8          0.3458561  0.0413541    8.363  < 2e-16 ***
    ## factor(summary)9         -0.0685159  0.0140869   -4.864 1.15e-06 ***
    ## factor(summary)10         0.4038945  0.1070925    3.771 0.000162 ***
    ## factor(summary)11        -0.1125962  0.0117615   -9.573  < 2e-16 ***
    ## factor(summary)12        -0.0850843  0.0095242   -8.933  < 2e-16 ***
    ## factor(summary)13        -0.0994907  0.0125047   -7.956 1.77e-15 ***
    ## factor(summary)14         0.1115142  0.0150707    7.399 1.37e-13 ***
    ## factor(summary)15         0.0587110  0.2974834    0.197 0.843547    
    ## factor(summary)17        -0.1582564  0.0251298   -6.298 3.02e-10 ***
    ## factor(summary)20         0.1855339  0.0116398   15.940  < 2e-16 ***
    ## factor(summary)21        -0.0771094  0.0096869   -7.960 1.72e-15 ***
    ## Month                    -0.0063122  0.0003546  -17.800  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1002920  on 1505973  degrees of freedom
    ## Residual deviance:  967932  on 1505948  degrees of freedom
    ## AIC: 967984
    ## 
    ## Number of Fisher Scoring iterations: 5

``` r
with(probit1, null.deviance - deviance)
```

    ## [1] 34987.98

``` r
with(probit1, df.null - df.residual)
```

    ## [1] 25

``` r
with(probit1, pchisq(null.deviance - deviance, df.null - df.residual, lower.tail = FALSE))
```

    ## [1] 0

``` r
probitmfx(formula=return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return)
```

    ## Call:
    ## probitmfx(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, data = return)
    ## 
    ## Marginal Effects:
    ##                                dF/dx   Std. Err.        z     P>|z|    
    ## lognet_purchase_amount    3.2544e-02  3.3330e-04  97.6429 < 2.2e-16 ***
    ## factor(gender)1          -2.6062e-02  4.9068e-04 -53.1143 < 2.2e-16 ***
    ## age_band                  8.1619e-05  6.2828e-05   1.2991  0.193914    
    ## est_income_code           2.1869e-03  1.0869e-04  20.1210 < 2.2e-16 ***
    ## factor(BOPS)1             1.5267e-02  6.8985e-04  22.1304 < 2.2e-16 ***
    ## factor(store_number)6    -3.6992e-03  9.4093e-04  -3.9314 8.446e-05 ***
    ## factor(store_number)5998 -3.0710e-02  9.9827e-03  -3.0763  0.002096 ** 
    ## factor(summary)2          5.7007e-02  2.4207e-03  23.5498 < 2.2e-16 ***
    ## factor(summary)3         -3.8791e-03  2.0842e-03  -1.8612  0.062720 .  
    ## factor(summary)4         -4.4059e-03  1.5029e-03  -2.9316  0.003373 ** 
    ## factor(summary)5         -1.4097e-02  1.5030e-03  -9.3794 < 2.2e-16 ***
    ## factor(summary)6          2.8909e-02  2.3710e-03  12.1926 < 2.2e-16 ***
    ## factor(summary)7         -5.0598e-02  1.4086e-03 -35.9201 < 2.2e-16 ***
    ## factor(summary)8          7.2830e-02  1.0417e-02   6.9917 2.715e-12 ***
    ## factor(summary)9         -1.1187e-02  2.2011e-03  -5.0826 3.722e-07 ***
    ## factor(summary)10         8.7879e-02  2.8482e-02   3.0854  0.002033 ** 
    ## factor(summary)11        -1.7878e-02  1.7342e-03 -10.3093 < 2.2e-16 ***
    ## factor(summary)12        -1.4042e-02  1.5216e-03  -9.2280 < 2.2e-16 ***
    ## factor(summary)13        -1.5922e-02  1.8743e-03  -8.4948 < 2.2e-16 ***
    ## factor(summary)14         2.0373e-02  2.9412e-03   6.9267 4.308e-12 ***
    ## factor(summary)15         1.0392e-02  5.4633e-02   0.1902  0.849146    
    ## factor(summary)17        -2.4283e-02  3.4443e-03  -7.0504 1.784e-12 ***
    ## factor(summary)20         3.5401e-02  2.4639e-03  14.3679 < 2.2e-16 ***
    ## factor(summary)21        -1.2740e-02  1.5512e-03  -8.2133 < 2.2e-16 ***
    ## Month                    -1.0756e-03  6.0414e-05 -17.8040 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## dF/dx is for discrete change for the following variables:
    ## 
    ##  [1] "factor(gender)1"          "factor(BOPS)1"           
    ##  [3] "factor(store_number)6"    "factor(store_number)5998"
    ##  [5] "factor(summary)2"         "factor(summary)3"        
    ##  [7] "factor(summary)4"         "factor(summary)5"        
    ##  [9] "factor(summary)6"         "factor(summary)7"        
    ## [11] "factor(summary)8"         "factor(summary)9"        
    ## [13] "factor(summary)10"        "factor(summary)11"       
    ## [15] "factor(summary)12"        "factor(summary)13"       
    ## [17] "factor(summary)14"        "factor(summary)15"       
    ## [19] "factor(summary)17"        "factor(summary)20"       
    ## [21] "factor(summary)21"

``` r
probitmfx(formula=return~lognet_purchase_amount+factor(gender)+age_band+est_income_code+factor(BOPS)+factor(store_number)+factor(summary)+Month,data=return, robust=TRUE)
```

    ## Call:
    ## probitmfx(formula = return ~ lognet_purchase_amount + factor(gender) + 
    ##     age_band + est_income_code + factor(BOPS) + factor(store_number) + 
    ##     factor(summary) + Month, data = return, robust = TRUE)
    ## 
    ## Marginal Effects:
    ##                                dF/dx   Std. Err.        z     P>|z|    
    ## lognet_purchase_amount    3.2544e-02  3.4156e-04  95.2822 < 2.2e-16 ***
    ## factor(gender)1          -2.6062e-02  4.9488e-04 -52.6634 < 2.2e-16 ***
    ## age_band                  8.1619e-05  6.2714e-05   1.3014  0.193106    
    ## est_income_code           2.1869e-03  1.0876e-04  20.1078 < 2.2e-16 ***
    ## factor(BOPS)1             1.5267e-02  6.9166e-04  22.0724 < 2.2e-16 ***
    ## factor(store_number)6    -3.6992e-03  9.3854e-04  -3.9414 8.101e-05 ***
    ## factor(store_number)5998 -3.0710e-02  1.0110e-02  -3.0377  0.002384 ** 
    ## factor(summary)2          5.7007e-02  2.4499e-03  23.2691 < 2.2e-16 ***
    ## factor(summary)3         -3.8791e-03  2.0951e-03  -1.8515  0.064096 .  
    ## factor(summary)4         -4.4059e-03  1.5197e-03  -2.8991  0.003742 ** 
    ## factor(summary)5         -1.4097e-02  1.5283e-03  -9.2240 < 2.2e-16 ***
    ## factor(summary)6          2.8909e-02  2.3947e-03  12.0721 < 2.2e-16 ***
    ## factor(summary)7         -5.0598e-02  1.4348e-03 -35.2655 < 2.2e-16 ***
    ## factor(summary)8          7.2830e-02  1.0475e-02   6.9530 3.575e-12 ***
    ## factor(summary)9         -1.1187e-02  2.2259e-03  -5.0259 5.010e-07 ***
    ## factor(summary)10         8.7879e-02  2.8740e-02   3.0577  0.002230 ** 
    ## factor(summary)11        -1.7878e-02  1.7428e-03 -10.2584 < 2.2e-16 ***
    ## factor(summary)12        -1.4042e-02  1.5410e-03  -9.1123 < 2.2e-16 ***
    ## factor(summary)13        -1.5922e-02  1.8875e-03  -8.4355 < 2.2e-16 ***
    ## factor(summary)14         2.0373e-02  2.9565e-03   6.8908 5.549e-12 ***
    ## factor(summary)15         1.0392e-02  5.4477e-02   0.1908  0.848720    
    ## factor(summary)17        -2.4283e-02  3.5022e-03  -6.9337 4.100e-12 ***
    ## factor(summary)20         3.5401e-02  2.4743e-03  14.3078 < 2.2e-16 ***
    ## factor(summary)21        -1.2740e-02  1.5754e-03  -8.0870 6.116e-16 ***
    ## Month                    -1.0756e-03  5.9904e-05 -17.9558 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## dF/dx is for discrete change for the following variables:
    ## 
    ##  [1] "factor(gender)1"          "factor(BOPS)1"           
    ##  [3] "factor(store_number)6"    "factor(store_number)5998"
    ##  [5] "factor(summary)2"         "factor(summary)3"        
    ##  [7] "factor(summary)4"         "factor(summary)5"        
    ##  [9] "factor(summary)6"         "factor(summary)7"        
    ## [11] "factor(summary)8"         "factor(summary)9"        
    ## [13] "factor(summary)10"        "factor(summary)11"       
    ## [15] "factor(summary)12"        "factor(summary)13"       
    ## [17] "factor(summary)14"        "factor(summary)15"       
    ## [19] "factor(summary)17"        "factor(summary)20"       
    ## [21] "factor(summary)21"

``` r
AIC(logit1,probit1)
```

    ##         df      AIC
    ## logit1  26 968034.1
    ## probit1 26 967984.3

``` r
BIC(logit1,probit1)
```

    ##         df      BIC
    ## logit1  26 968351.9
    ## probit1 26 968302.2

OLS Model (Sales)
-----------------

``` r
#read the data
newdata = read.csv("new_project_monthlysales_Final.csv",header = TRUE)
summary(newdata[,1:9])
```

    ##   store_number     summary        month_index   monthly_sales    
    ##  Min.   :   2   Min.   : 1.000   Min.   :13.0   Min.   :     19  
    ##  1st Qu.:   2   1st Qu.: 4.000   1st Qu.:19.0   1st Qu.:   9746  
    ##  Median :   6   Median : 9.000   Median :25.0   Median :  29009  
    ##  Mean   :1677   Mean   : 9.356   Mean   :25.4   Mean   : 166785  
    ##  3rd Qu.:5998   3rd Qu.:13.000   3rd Qu.:31.0   3rd Qu.: 174640  
    ##  Max.   :5998   Max.   :21.000   Max.   :37.0   Max.   :4727543  
    ##                                                                  
    ##    pol_change         month          year        treatment     
    ##  Min.   :0.0000   AUG    :122   Min.   :2010   Min.   :0.0000  
    ##  1st Qu.:0.0000   DEC    : 92   1st Qu.:2011   1st Qu.:0.0000  
    ##  Median :1.0000   JAN    : 90   Median :2011   Median :1.0000  
    ##  Mean   :0.5399   JUL    : 90   Mean   :2011   Mean   :0.7208  
    ##  3rd Qu.:1.0000   JUN    : 90   3rd Qu.:2012   3rd Qu.:1.0000  
    ##  Max.   :1.0000   FEB    : 89   Max.   :2012   Max.   :1.0000  
    ##                   (Other):505                                  
    ##      bridal      
    ##  Min.   :0.0000  
    ##  1st Qu.:0.0000  
    ##  Median :0.0000  
    ##  Mean   :0.2004  
    ##  3rd Qu.:0.0000  
    ##  Max.   :1.0000  
    ## 

``` r
#define all variables
monthly_sales=newdata$monthly_sales
hist(monthly_sales)
```

![](Irene_files/figure-markdown_github/unnamed-chunk-2-1.png)

``` r
log_sales=log(monthly_sales)
hist(log_sales) ##normal
```

![](Irene_files/figure-markdown_github/unnamed-chunk-2-2.png)

``` r
store=as.factor(newdata$store_number)
category=as.factor(newdata$summary)
time_index=newdata$month_index
BOPS=as.factor(newdata$pol_change)
month=as.factor(newdata$month)
year=as.factor(newdata$year)
treatment=as.factor(newdata$treatment)
bridal=as.factor(newdata$bridal)

newdata$Nov=as.numeric(newdata$month=="NOV")
newdata$Dec=as.numeric(newdata$month=="DEC")
Nov=as.factor(newdata$Nov)
Dec=as.factor(newdata$Dec)

summary(newdata)
```

    ##   store_number     summary        month_index   monthly_sales    
    ##  Min.   :   2   Min.   : 1.000   Min.   :13.0   Min.   :     19  
    ##  1st Qu.:   2   1st Qu.: 4.000   1st Qu.:19.0   1st Qu.:   9746  
    ##  Median :   6   Median : 9.000   Median :25.0   Median :  29009  
    ##  Mean   :1677   Mean   : 9.356   Mean   :25.4   Mean   : 166785  
    ##  3rd Qu.:5998   3rd Qu.:13.000   3rd Qu.:31.0   3rd Qu.: 174640  
    ##  Max.   :5998   Max.   :21.000   Max.   :37.0   Max.   :4727543  
    ##                                                                  
    ##    pol_change         month          year        treatment     
    ##  Min.   :0.0000   AUG    :122   Min.   :2010   Min.   :0.0000  
    ##  1st Qu.:0.0000   DEC    : 92   1st Qu.:2011   1st Qu.:0.0000  
    ##  Median :1.0000   JAN    : 90   Median :2011   Median :1.0000  
    ##  Mean   :0.5399   JUL    : 90   Mean   :2011   Mean   :0.7208  
    ##  3rd Qu.:1.0000   JUN    : 90   3rd Qu.:2012   3rd Qu.:1.0000  
    ##  Max.   :1.0000   FEB    : 89   Max.   :2012   Max.   :1.0000  
    ##                   (Other):505                                  
    ##      bridal            Nov               Dec         
    ##  Min.   :0.0000   Min.   :0.00000   Min.   :0.00000  
    ##  1st Qu.:0.0000   1st Qu.:0.00000   1st Qu.:0.00000  
    ##  Median :0.0000   Median :0.00000   Median :0.00000  
    ##  Mean   :0.2004   Mean   :0.08163   Mean   :0.08534  
    ##  3rd Qu.:0.0000   3rd Qu.:0.00000   3rd Qu.:0.00000  
    ##  Max.   :1.0000   Max.   :1.00000   Max.   :1.00000  
    ## 

``` r
#check factor variable correlation
#predicitibility matrix
library(GoodmanKruskal)

GK_correlation_matrix <- GKtauDataframe(newdata[,c(1,2,5,6,7,8,9)])

plot(GK_correlation_matrix,diagSize = 0.8,diagColor = "black",

backgroundColor = "white",colorPlot=FALSE)
```

![](Irene_files/figure-markdown_github/unnamed-chunk-2-3.png)

``` r
# OLS model
model1 = lm(log_sales~store+category+time_index+BOPS+month+year+treatment+bridal)
summary(model1) ##all 8 variables
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ store + category + time_index + BOPS + 
    ##     month + year + treatment + bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.9619 -0.2468  0.0341  0.3215  3.3827 
    ## 
    ## Coefficients: (3 not defined because of singularities)
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 12.815873   0.293905  43.605  < 2e-16 ***
    ## store6      -2.578039   0.058301 -44.219  < 2e-16 ***
    ## store5998   -3.122738   0.061490 -50.785  < 2e-16 ***
    ## category2   -1.134516   0.129422  -8.766  < 2e-16 ***
    ## category3   -0.243113   0.129422  -1.878   0.0606 .  
    ## category4    0.688088   0.129422   5.317 1.29e-07 ***
    ## category5    0.188185   0.129422   1.454   0.1462    
    ## category6   -1.023648   0.129422  -7.909 6.56e-15 ***
    ## category7   -2.725687   0.129422 -21.061  < 2e-16 ***
    ## category8   -4.061074   0.168504 -24.101  < 2e-16 ***
    ## category9   -4.091243   0.137257 -29.807  < 2e-16 ***
    ## category10  -5.505318   0.199320 -27.621  < 2e-16 ***
    ## category11  -0.668600   0.129422  -5.166 2.86e-07 ***
    ## category12   0.239848   0.129422   1.853   0.0641 .  
    ## category13  -1.129676   0.129422  -8.729  < 2e-16 ***
    ## category14  -3.013735   0.130850 -23.032  < 2e-16 ***
    ## category15  -6.844201   0.254349 -26.909  < 2e-16 ***
    ## category17  -0.789919   0.183319  -4.309 1.79e-05 ***
    ## category20  -0.748230   0.129422  -5.781 9.78e-09 ***
    ## category21  -0.115835   0.129422  -0.895   0.3710    
    ## time_index   0.001325   0.012451   0.106   0.9153    
    ## BOPS1        0.172373   0.161582   1.067   0.2863    
    ## monthAUG     0.130159   0.119283   1.091   0.2754    
    ## monthDEC     1.292728   0.126439  10.224  < 2e-16 ***
    ## monthFEB     0.563720   0.119724   4.709 2.83e-06 ***
    ## monthJAN     0.214273   0.122653   1.747   0.0809 .  
    ## monthJUL     0.113400   0.122614   0.925   0.3553    
    ## monthJUN     0.004471   0.119447   0.037   0.9701    
    ## monthMAR     0.056186   0.118179   0.475   0.6346    
    ## monthMAY     0.496446   0.118130   4.203 2.87e-05 ***
    ## monthNOV     0.646009   0.132919   4.860 1.35e-06 ***
    ## monthOCT     0.062955   0.142703   0.441   0.6592    
    ## monthSEP     0.011479   0.149530   0.077   0.9388    
    ## year2011    -0.059301   0.049941  -1.187   0.2353    
    ## year2012           NA         NA      NA       NA    
    ## treatment1         NA         NA      NA       NA    
    ## bridal1            NA         NA      NA       NA    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.7765 on 1044 degrees of freedom
    ## Multiple R-squared:  0.8669, Adjusted R-squared:  0.8627 
    ## F-statistic: 206.1 on 33 and 1044 DF,  p-value: < 2.2e-16

``` r
model11 = lm(log_sales~store+category+BOPS+month+year)
summary(model11) ## basic model
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ store + category + BOPS + month + year)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.9619 -0.2468  0.0341  0.3215  3.3827 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 12.827797   0.199994  64.141  < 2e-16 ***
    ## store6      -2.578039   0.058301 -44.219  < 2e-16 ***
    ## store5998   -3.122738   0.061490 -50.785  < 2e-16 ***
    ## category2   -1.134516   0.129422  -8.766  < 2e-16 ***
    ## category3   -0.243113   0.129422  -1.878 0.060597 .  
    ## category4    0.688088   0.129422   5.317 1.29e-07 ***
    ## category5    0.188185   0.129422   1.454 0.146235    
    ## category6   -1.023648   0.129422  -7.909 6.56e-15 ***
    ## category7   -2.725687   0.129422 -21.061  < 2e-16 ***
    ## category8   -4.061074   0.168504 -24.101  < 2e-16 ***
    ## category9   -4.091243   0.137257 -29.807  < 2e-16 ***
    ## category10  -5.505318   0.199320 -27.621  < 2e-16 ***
    ## category11  -0.668600   0.129422  -5.166 2.86e-07 ***
    ## category12   0.239848   0.129422   1.853 0.064132 .  
    ## category13  -1.129676   0.129422  -8.729  < 2e-16 ***
    ## category14  -3.013735   0.130850 -23.032  < 2e-16 ***
    ## category15  -6.844201   0.254349 -26.909  < 2e-16 ***
    ## category17  -0.789919   0.183319  -4.309 1.79e-05 ***
    ## category20  -0.748230   0.129422  -5.781 9.78e-09 ***
    ## category21  -0.115835   0.129422  -0.895 0.370984    
    ## BOPS1        0.172373   0.161582   1.067 0.286314    
    ## monthAUG     0.135458   0.146068   0.927 0.353953    
    ## monthDEC     1.303327   0.189302   6.885 9.96e-12 ***
    ## monthFEB     0.561070   0.117111   4.791 1.90e-06 ***
    ## monthJAN     0.210298   0.116821   1.800 0.072122 .  
    ## monthJUL     0.117375   0.116800   1.005 0.315169    
    ## monthJUN     0.007121   0.116800   0.061 0.951397    
    ## monthMAR     0.054861   0.117503   0.467 0.640676    
    ## monthMAY     0.497770   0.117477   4.237 2.46e-05 ***
    ## monthNOV     0.655282   0.190061   3.448 0.000588 ***
    ## monthOCT     0.070904   0.192351   0.369 0.712487    
    ## monthSEP     0.018103   0.192359   0.094 0.925041    
    ## year2011    -0.043403   0.165554  -0.262 0.793245    
    ## year2012     0.031796   0.298813   0.106 0.915279    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.7765 on 1044 degrees of freedom
    ## Multiple R-squared:  0.8669, Adjusted R-squared:  0.8627 
    ## F-statistic: 206.1 on 33 and 1044 DF,  p-value: < 2.2e-16

``` r
model12 = lm(log_sales~category+BOPS+Nov+Dec+year+treatment)
summary(model12) ## basic model####################
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ category + BOPS + Nov + Dec + year + 
    ##     treatment)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.1357 -1.0973 -0.0347  1.1656  3.4876 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  9.77936    0.20772  47.081  < 2e-16 ***
    ## category2   -1.13452    0.22012  -5.154 3.04e-07 ***
    ## category3   -0.24311    0.22012  -1.104 0.269654    
    ## category4    0.68809    0.22012   3.126 0.001821 ** 
    ## category5    0.18818    0.22012   0.855 0.392797    
    ## category6   -1.02365    0.22012  -4.650 3.73e-06 ***
    ## category7   -2.72569    0.22012 -12.383  < 2e-16 ***
    ## category8   -3.35476    0.28514 -11.765  < 2e-16 ***
    ## category9   -3.86316    0.23325 -16.562  < 2e-16 ***
    ## category10  -4.21753    0.33525 -12.580  < 2e-16 ***
    ## category11  -0.66860    0.22012  -3.037 0.002445 ** 
    ## category12   0.23985    0.22012   1.090 0.276134    
    ## category13  -1.12968    0.22012  -5.132 3.41e-07 ***
    ## category14  -3.01854    0.22253 -13.564  < 2e-16 ***
    ## category15  -5.59003    0.42941 -13.018  < 2e-16 ***
    ## category17   0.49305    0.30786   1.602 0.109559    
    ## category20  -0.74823    0.22012  -3.399 0.000701 ***
    ## category21  -0.11583    0.22012  -0.526 0.598841    
    ## BOPS1        0.01588    0.12668   0.125 0.900242    
    ## Nov1         0.59388    0.16646   3.568 0.000376 ***
    ## Dec1         1.20044    0.16380   7.329 4.62e-13 ***
    ## year2011     0.09883    0.14027   0.705 0.481251    
    ## year2012     0.27878    0.20500   1.360 0.174143    
    ## treatment1   1.85194    0.09244  20.034  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.321 on 1054 degrees of freedom
    ## Multiple R-squared:  0.6113, Adjusted R-squared:  0.6028 
    ## F-statistic: 72.06 on 23 and 1054 DF,  p-value: < 2.2e-16

``` r
model13 = lm(log_sales~category+BOPS+Nov+Dec+year+store+store*BOPS)
summary(model13) ## basic model
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ category + BOPS + Nov + Dec + year + 
    ##     store + store * BOPS)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.2907 -0.2843  0.0451  0.3297  3.5135 
    ## 
    ## Coefficients:
    ##                 Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)     12.95076    0.11977 108.127  < 2e-16 ***
    ## category2       -1.13452    0.12995  -8.731  < 2e-16 ***
    ## category3       -0.24311    0.12995  -1.871  0.06164 .  
    ## category4        0.68809    0.12995   5.295 1.45e-07 ***
    ## category5        0.18818    0.12995   1.448  0.14787    
    ## category6       -1.02365    0.12995  -7.877 8.30e-15 ***
    ## category7       -2.72569    0.12995 -20.975  < 2e-16 ***
    ## category8       -4.05692    0.16913 -23.987  < 2e-16 ***
    ## category9       -4.09888    0.13785 -29.735  < 2e-16 ***
    ## category10      -5.51965    0.20017 -27.575  < 2e-16 ***
    ## category11      -0.66860    0.12995  -5.145 3.19e-07 ***
    ## category12       0.23985    0.12995   1.846  0.06521 .  
    ## category13      -1.12968    0.12995  -8.693  < 2e-16 ***
    ## category14      -3.00942    0.13138 -22.907  < 2e-16 ***
    ## category15      -6.91177    0.25558 -27.044  < 2e-16 ***
    ## category17      -0.79015    0.18406  -4.293 1.93e-05 ***
    ## category20      -0.74823    0.12995  -5.758 1.12e-08 ***
    ## category21      -0.11583    0.12995  -0.891  0.37292    
    ## BOPS1           -0.20267    0.09675  -2.095  0.03643 *  
    ## Nov1             0.62691    0.09863   6.356 3.08e-10 ***
    ## Dec1             1.27880    0.09712  13.167  < 2e-16 ***
    ## year2011         0.16999    0.08404   2.023  0.04337 *  
    ## year2012         0.38600    0.12233   3.155  0.00165 ** 
    ## store6          -2.61645    0.08366 -31.276  < 2e-16 ***
    ## store5998       -3.50583    0.09268 -37.827  < 2e-16 ***
    ## BOPS1:store6     0.07644    0.11301   0.676  0.49891    
    ## BOPS1:store5998  0.65552    0.12010   5.458 6.00e-08 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.7797 on 1051 degrees of freedom
    ## Multiple R-squared:  0.8649, Adjusted R-squared:  0.8616 
    ## F-statistic: 258.8 on 26 and 1051 DF,  p-value: < 2.2e-16

``` r
model2 = lm(log_sales~category+time_index+BOPS+month+year+treatment+bridal)
summary(model2) ##remove store
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ category + time_index + BOPS + month + 
    ##     year + treatment + bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.9523 -1.1035 -0.0167  1.1956  3.1950 
    ## 
    ## Coefficients: (2 not defined because of singularities)
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  9.653241   0.503829  19.160  < 2e-16 ***
    ## category2   -1.134516   0.219261  -5.174 2.74e-07 ***
    ## category3   -0.243113   0.219261  -1.109 0.267779    
    ## category4    0.688088   0.219261   3.138 0.001747 ** 
    ## category5    0.188185   0.219261   0.858 0.390942    
    ## category6   -1.023648   0.219261  -4.669 3.43e-06 ***
    ## category7   -2.725687   0.219261 -12.431  < 2e-16 ***
    ## category8   -3.357232   0.284196 -11.813  < 2e-16 ***
    ## category9   -3.864169   0.232372 -16.629  < 2e-16 ***
    ## category10  -4.226614   0.334108 -12.650  < 2e-16 ***
    ## category11  -0.668600   0.219261  -3.049 0.002351 ** 
    ## category12   0.239848   0.219261   1.094 0.274255    
    ## category13  -1.129676   0.219261  -5.152 3.08e-07 ***
    ## category14  -3.015184   0.221681 -13.601  < 2e-16 ***
    ## category15  -5.574060   0.428152 -13.019  < 2e-16 ***
    ## category17   0.493225   0.306656   1.608 0.108050    
    ## category20  -0.748230   0.219261  -3.413 0.000668 ***
    ## category21  -0.115835   0.219261  -0.528 0.597407    
    ## time_index   0.003542   0.021093   0.168 0.866662    
    ## BOPS1        0.115883   0.273737   0.423 0.672136    
    ## monthAUG     0.130686   0.202084   0.647 0.517973    
    ## monthDEC     1.266980   0.214206   5.915 4.50e-09 ***
    ## monthFEB     0.571899   0.202831   2.820 0.004899 ** 
    ## monthJAN     0.202547   0.207793   0.975 0.329909    
    ## monthJUL     0.088466   0.207726   0.426 0.670285    
    ## monthJUN    -0.018745   0.202360  -0.093 0.926216    
    ## monthMAR     0.042668   0.200213   0.213 0.831282    
    ## monthMAY     0.478081   0.200130   2.389 0.017078 *  
    ## monthNOV     0.663810   0.225186   2.948 0.003271 ** 
    ## monthOCT     0.065239   0.241762   0.270 0.787330    
    ## monthSEP     0.035723   0.253326   0.141 0.887885    
    ## year2011    -0.044227   0.084606  -0.523 0.601272    
    ## year2012           NA         NA      NA       NA    
    ## treatment1   1.851325   0.092084  20.105  < 2e-16 ***
    ## bridal1            NA         NA      NA       NA    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.316 on 1045 degrees of freedom
    ## Multiple R-squared:  0.6176, Adjusted R-squared:  0.6059 
    ## F-statistic: 52.74 on 32 and 1045 DF,  p-value: < 2.2e-16

``` r
model3 = lm(log_sales~time_index+BOPS+month+year+treatment+bridal)
summary(model3) ## remove category
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ time_index + BOPS + month + year + treatment + 
    ##     bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.6240 -1.0491  0.2087  1.3512  3.7637 
    ## 
    ## Coefficients: (1 not defined because of singularities)
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  8.661921   0.709119  12.215  < 2e-16 ***
    ## time_index   0.005163   0.031045   0.166 0.867937    
    ## BOPS1        0.113305   0.402785   0.281 0.778532    
    ## monthAUG     0.031862   0.297325   0.107 0.914680    
    ## monthDEC     1.131156   0.315150   3.589 0.000347 ***
    ## monthFEB     0.506438   0.298469   1.697 0.090031 .  
    ## monthJAN     0.114822   0.305719   0.376 0.707304    
    ## monthJUL     0.002271   0.305623   0.007 0.994073    
    ## monthJUN    -0.102867   0.297729  -0.346 0.729784    
    ## monthMAR     0.032296   0.294474   0.110 0.912688    
    ## monthMAY     0.476442   0.294392   1.618 0.105876    
    ## monthNOV     0.646705   0.331448   1.951 0.051302 .  
    ## monthOCT    -0.043410   0.355763  -0.122 0.902906    
    ## monthSEP    -0.093603   0.372759  -0.251 0.801779    
    ## year2011    -0.068047   0.124368  -0.547 0.584395    
    ## year2012           NA         NA      NA       NA    
    ## treatment1   1.652921   0.133342  12.396  < 2e-16 ***
    ## bridal1      0.541769   0.147412   3.675 0.000250 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.936 on 1061 degrees of freedom
    ## Multiple R-squared:  0.1588, Adjusted R-squared:  0.1461 
    ## F-statistic: 12.52 on 16 and 1061 DF,  p-value: < 2.2e-16

``` r
model4 = lm(log_sales~BOPS+month+year+treatment+bridal)
summary(model4) ## remove time_index
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ BOPS + month + year + treatment + bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.6240 -1.0491  0.2087  1.3512  3.7637 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  8.708391   0.459113  18.968  < 2e-16 ***
    ## BOPS1        0.113305   0.402785   0.281  0.77853    
    ## monthAUG     0.052516   0.364142   0.144  0.88536    
    ## monthDEC     1.172463   0.471969   2.484  0.01314 *  
    ## monthFEB     0.496112   0.291949   1.699  0.08955 .  
    ## monthJAN     0.099332   0.291151   0.341  0.73304    
    ## monthJUL     0.017761   0.291147   0.061  0.95137    
    ## monthJUN    -0.092540   0.291147  -0.318  0.75066    
    ## monthMAR     0.027133   0.292785   0.093  0.92618    
    ## monthMAY     0.481605   0.292768   1.645  0.10026    
    ## monthNOV     0.682849   0.473938   1.441  0.14994    
    ## monthOCT    -0.012430   0.479579  -0.026  0.97933    
    ## monthSEP    -0.067786   0.479586  -0.141  0.88763    
    ## year2011    -0.006087   0.412773  -0.015  0.98824    
    ## year2012     0.123921   0.745075   0.166  0.86794    
    ## treatment1   1.652921   0.133342  12.396  < 2e-16 ***
    ## bridal1      0.541769   0.147412   3.675  0.00025 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.936 on 1061 degrees of freedom
    ## Multiple R-squared:  0.1588, Adjusted R-squared:  0.1461 
    ## F-statistic: 12.52 on 16 and 1061 DF,  p-value: < 2.2e-16

``` r
model5 = lm(log_sales~BOPS+category+Nov+Dec+year+treatment+BOPS*treatment)
summary(model5) ## interaction btw BOPS*treatment w/out bridal
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ BOPS + category + Nov + Dec + year + 
    ##     treatment + BOPS * treatment)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.2474 -1.0878  0.0203  1.1665  3.4763 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        9.4249     0.2291  41.143  < 2e-16 ***
    ## BOPS1              0.4514     0.1751   2.577 0.010098 *  
    ## category2         -1.1345     0.2189  -5.183 2.62e-07 ***
    ## category3         -0.2431     0.2189  -1.111 0.266989    
    ## category4          0.6881     0.2189   3.143 0.001717 ** 
    ## category5          0.1882     0.2189   0.860 0.390159    
    ## category6         -1.0236     0.2189  -4.676 3.30e-06 ***
    ## category7         -2.7257     0.2189 -12.452  < 2e-16 ***
    ## category8         -3.3528     0.2836 -11.824  < 2e-16 ***
    ## category9         -3.8701     0.2320 -16.684  < 2e-16 ***
    ## category10        -4.2378     0.3334 -12.709  < 2e-16 ***
    ## category11        -0.6686     0.2189  -3.054 0.002312 ** 
    ## category12         0.2398     0.2189   1.096 0.273462    
    ## category13        -1.1297     0.2189  -5.161 2.94e-07 ***
    ## category14        -3.0104     0.2213 -13.603  < 2e-16 ***
    ## category15        -5.6341     0.4272 -13.188  < 2e-16 ***
    ## category17         0.4922     0.3062   1.608 0.108181    
    ## category20        -0.7482     0.2189  -3.418 0.000655 ***
    ## category21        -0.1158     0.2189  -0.529 0.596802    
    ## Nov1               0.6439     0.1661   3.876 0.000113 ***
    ## Dec1               1.2544     0.1636   7.668 3.96e-14 ***
    ## year2011           0.1850     0.1416   1.307 0.191452    
    ## year2012           0.3854     0.2060   1.871 0.061671 .  
    ## treatment1         2.2388     0.1419  15.778  < 2e-16 ***
    ## BOPS1:treatment1  -0.6574     0.1837  -3.579 0.000361 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.313 on 1053 degrees of freedom
    ## Multiple R-squared:  0.616,  Adjusted R-squared:  0.6072 
    ## F-statistic: 70.37 on 24 and 1053 DF,  p-value: < 2.2e-16

``` r
model51 = lm(log_sales~BOPS+Nov+Dec+year+treatment+BOPS*treatment+bridal)
summary(model51) ## interaction btw BOPS*treatment w/bridal
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ BOPS + Nov + Dec + year + treatment + 
    ##     BOPS * treatment + bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.8708 -1.0826  0.2006  1.3443  3.8981 
    ## 
    ## Coefficients:
    ##                  Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        8.3947     0.2580  32.539  < 2e-16 ***
    ## BOPS1              0.3297     0.2576   1.280 0.200824    
    ## Nov1               0.7354     0.2444   3.009 0.002683 ** 
    ## Dec1               1.2281     0.2407   5.102 3.97e-07 ***
    ## year2011           0.2240     0.2082   1.076 0.282268    
    ## year2012           0.5158     0.3030   1.702 0.089046 .  
    ## treatment1         1.9834     0.2070   9.581  < 2e-16 ***
    ## bridal1            0.5429     0.1471   3.690 0.000236 ***
    ## BOPS1:treatment1  -0.5615     0.2701  -2.079 0.037883 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.933 on 1069 degrees of freedom
    ## Multiple R-squared:  0.1556, Adjusted R-squared:  0.1492 
    ## F-statistic: 24.62 on 8 and 1069 DF,  p-value: < 2.2e-16

``` r
model52 = lm(log_sales~BOPS+month+year+treatment+BOPS*treatment+bridal)
summary(model52) ## interaction btw BOPS*treatment w/bridal######################Final Model
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ BOPS + month + year + treatment + BOPS * 
    ##     treatment + bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.7208 -1.0559  0.2125  1.3450  3.7712 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)       8.402221   0.481372  17.455  < 2e-16 ***
    ## BOPS1             0.487720   0.440480   1.107  0.26844    
    ## monthAUG          0.055157   0.363572   0.152  0.87944    
    ## monthDEC          1.220979   0.471803   2.588  0.00979 ** 
    ## monthFEB          0.502194   0.291505   1.723  0.08522 .  
    ## monthJAN          0.106181   0.290712   0.365  0.71500    
    ## monthJUL          0.022026   0.290697   0.076  0.93962    
    ## monthJUN         -0.090184   0.290692  -0.310  0.75644    
    ## monthMAR          0.032582   0.292337   0.111  0.91128    
    ## monthMAY          0.482458   0.292308   1.651  0.09913 .  
    ## monthNOV          0.728282   0.473696   1.537  0.12448    
    ## monthOCT         -0.009788   0.478828  -0.020  0.98369    
    ## monthSEP         -0.066651   0.478833  -0.139  0.88932    
    ## year2011          0.066419   0.413592   0.161  0.87245    
    ## year2012          0.213080   0.745135   0.286  0.77496    
    ## treatment1        1.983370   0.207077   9.578  < 2e-16 ***
    ## bridal1           0.542434   0.147181   3.685  0.00024 ***
    ## BOPS1:treatment1 -0.562966   0.270212  -2.083  0.03745 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.933 on 1060 degrees of freedom
    ## Multiple R-squared:  0.1623, Adjusted R-squared:  0.1488 
    ## F-statistic: 12.08 on 17 and 1060 DF,  p-value: < 2.2e-16

``` r
model61 = lm(log_sales~BOPS+month+year+treatment+bridal+BOPS*treatment*bridal)
summary(model61) ## interaction btw BOPS*treatment*bridal############################Final Model
```

    ## 
    ## Call:
    ## lm(formula = log_sales ~ BOPS + month + year + treatment + bridal + 
    ##     BOPS * treatment * bridal)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.6892 -1.0952  0.2972  1.2684  3.8130 
    ## 
    ## Coefficients:
    ##                           Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)               8.512185   0.489114  17.403  < 2e-16 ***
    ## BOPS1                     0.468095   0.456536   1.025  0.30545    
    ## monthAUG                  0.055120   0.363416   0.152  0.87947    
    ## monthDEC                  1.220662   0.471599   2.588  0.00978 ** 
    ## monthFEB                  0.502913   0.291384   1.726  0.08465 .  
    ## monthJAN                  0.107359   0.290592   0.369  0.71187    
    ## monthJUL                  0.021753   0.290574   0.075  0.94034    
    ## monthJUN                 -0.090575   0.290567  -0.312  0.75532    
    ## monthMAR                  0.034665   0.292216   0.119  0.90559    
    ## monthMAY                  0.482937   0.292182   1.653  0.09866 .  
    ## monthNOV                  0.727909   0.473491   1.537  0.12451    
    ## monthOCT                 -0.009826   0.478621  -0.021  0.98362    
    ## monthSEP                 -0.066833   0.478625  -0.140  0.88897    
    ## year2011                  0.065239   0.413413   0.158  0.87464    
    ## year2012                  0.211379   0.744813   0.284  0.77662    
    ## treatment1                1.842996   0.232210   7.937 5.27e-15 ***
    ## bridal1                   0.048181   0.421483   0.114  0.90901    
    ## BOPS1:treatment1         -0.553304   0.303457  -1.823  0.06854 .  
    ## BOPS1:bridal1             0.085583   0.547811   0.156  0.87588    
    ## treatment1:bridal1        0.654586   0.491818   1.331  0.18349    
    ## BOPS1:treatment1:bridal1 -0.030744   0.650940  -0.047  0.96234    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.933 on 1057 degrees of freedom
    ## Multiple R-squared:  0.1654, Adjusted R-squared:  0.1496 
    ## F-statistic: 10.47 on 20 and 1057 DF,  p-value: < 2.2e-16
