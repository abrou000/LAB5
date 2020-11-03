# LAB5
> attach(acs2017_ny)
> use_varb <- (AGE >= 25) & (AGE <= 55) & (LABFORCE == 2) & (WKSWORK2 > 4) & (UHRSWORK >= 35) & (AfAm == 1) & (female==1) & ((educ_college == 1) | (educ_advdeg == 1))
> dat_use <- subset(acs2017_ny,use_varb) # 
> detach()
> 
> mod2<- lm((INCWAGE ~ AGE + I(AGE^2) +FAMSIZE +I(FAMSIZE^2)+ I(FAMSIZE^3)))
> 
> summary(mod2)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + FAMSIZE + I(FAMSIZE^2) + 
    I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-69978 -31435 -12135  10909 681784 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -6.053e+04  1.092e+03  -55.43   <2e-16 ***
AGE           4.089e+03  4.093e+01   99.90   <2e-16 ***
I(AGE^2)     -4.264e+01  4.037e-01 -105.61   <2e-16 ***
FAMSIZE       9.753e+03  4.944e+02   19.73   <2e-16 ***
I(FAMSIZE^2) -1.742e+03  9.976e+01  -17.46   <2e-16 ***
I(FAMSIZE^3)  7.001e+01  5.306e+00   13.19   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 63670 on 163152 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.07416,	Adjusted R-squared:  0.07413 
F-statistic:  2614 on 5 and 163152 DF,  p-value: < 2.2e-16

> NNobserv<-length(INCWAGE)
> set.seed(123456)
> graph_observ<-(runif(NNobserv)<0.1)
> data_to_graph<-subset(dat_use,graph_observ)
Length of logical index must be 1 or 1231, not 196585
> plot(INCWAGE ~ jitter(AGE, factor = 2), pch = 16, col = rgb(0.5, 0.5, 0.5, alpha = 0.2), data = dat_use)
> # ^^ that looks like crap since Wages are soooooooo skew!  So try to find some sensible ylim = c(0, ??)
> plot(INCWAGE ~ jitter(AGE, factor = 2), pch = 16, col = rgb(0.5, 0.5, 0.5, alpha = 0.2), ylim = c(0,150000), data = dat_use)
> 
> mod3<- lm((INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + educ_college +educ_advdeg+FAMSIZE +I(FAMSIZE^2)+ I(FAMSIZE^3)))
> 
> mod4<-lm((INCWAGE ~ AGE + I(AGE^2) +I(AGE^3)+I(AGE^4)+ educ_college +educ_advdeg+FAMSIZE +I(FAMSIZE^2)+ I(FAMSIZE^3)))
> 
> mod5<-lm((INCWAGE ~ AGE + I(AGE^2) +I(AGE^3)+I(AGE^4)+ educ_college))
> 
> summary(mod3)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + educ_college + 
    educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-91814 -26754  -6094  11059 646715 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -1.278e+05  2.112e+03  -60.49   <2e-16 ***
AGE           8.719e+03  1.423e+02   61.28   <2e-16 ***
I(AGE^2)     -1.488e+02  2.910e+00  -51.13   <2e-16 ***
I(AGE^3)      7.202e-01  1.826e-02   39.44   <2e-16 ***
educ_college  2.760e+04  3.972e+02   69.48   <2e-16 ***
educ_advdeg   4.949e+04  4.433e+02  111.64   <2e-16 ***
FAMSIZE       7.269e+03  4.700e+02   15.47   <2e-16 ***
I(FAMSIZE^2) -1.192e+03  9.489e+01  -12.56   <2e-16 ***
I(FAMSIZE^3)  4.703e+01  5.046e+00    9.32   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 60470 on 163149 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1648,	Adjusted R-squared:  0.1648 
F-statistic:  4025 on 8 and 163149 DF,  p-value: < 2.2e-16

> summary(mod4)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + I(AGE^4) + 
    educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-94260 -26875  -4963  11177 650499 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)   1.150e+04  4.742e+03   2.425   0.0153 *  
AGE          -5.028e+03  4.427e+02 -11.357   <2e-16 ***
I(AGE^2)      3.075e+02  1.422e+01  21.624   <2e-16 ***
I(AGE^3)     -5.413e+00  1.880e-01 -28.791   <2e-16 ***
I(AGE^4)      2.865e-02  8.742e-04  32.776   <2e-16 ***
educ_college  2.902e+04  3.983e+02  72.862   <2e-16 ***
educ_advdeg   5.060e+04  4.432e+02 114.191   <2e-16 ***
FAMSIZE       6.622e+03  4.688e+02  14.124   <2e-16 ***
I(FAMSIZE^2) -1.123e+03  9.460e+01 -11.871   <2e-16 ***
I(FAMSIZE^3)  4.486e+01  5.030e+00   8.918   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 60270 on 163148 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1703,	Adjusted R-squared:  0.1702 
F-statistic:  3721 on 9 and 163148 DF,  p-value: < 2.2e-16

> summary(mod5)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + I(AGE^4) + 
    educ_college))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-72108 -28918  -8135   6720 644720 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -4.122e+04  4.833e+03  -8.527   <2e-16 ***
AGE           6.036e+02  4.568e+02   1.321    0.186    
I(AGE^2)      1.557e+02  1.469e+01  10.599   <2e-16 ***
I(AGE^3)     -3.693e+00  1.942e-01 -19.012   <2e-16 ***
I(AGE^4)      2.158e-02  9.035e-04  23.884   <2e-16 ***
educ_college  1.899e+04  4.031e+02  47.111   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 62710 on 163152 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1019,	Adjusted R-squared:  0.1019 
F-statistic:  3702 on 5 and 163152 DF,  p-value: < 2.2e-16

> summary(mod3)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + educ_college + 
    educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-91814 -26754  -6094  11059 646715 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -1.278e+05  2.112e+03  -60.49   <2e-16 ***
AGE           8.719e+03  1.423e+02   61.28   <2e-16 ***
I(AGE^2)     -1.488e+02  2.910e+00  -51.13   <2e-16 ***
I(AGE^3)      7.202e-01  1.826e-02   39.44   <2e-16 ***
educ_college  2.760e+04  3.972e+02   69.48   <2e-16 ***
educ_advdeg   4.949e+04  4.433e+02  111.64   <2e-16 ***
FAMSIZE       7.269e+03  4.700e+02   15.47   <2e-16 ***
I(FAMSIZE^2) -1.192e+03  9.489e+01  -12.56   <2e-16 ***
I(FAMSIZE^3)  4.703e+01  5.046e+00    9.32   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 60470 on 163149 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1648,	Adjusted R-squared:  0.1648 
F-statistic:  4025 on 8 and 163149 DF,  p-value: < 2.2e-16

> summary(mod4)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + I(AGE^4) + 
    educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-94260 -26875  -4963  11177 650499 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)   1.150e+04  4.742e+03   2.425   0.0153 *  
AGE          -5.028e+03  4.427e+02 -11.357   <2e-16 ***
I(AGE^2)      3.075e+02  1.422e+01  21.624   <2e-16 ***
I(AGE^3)     -5.413e+00  1.880e-01 -28.791   <2e-16 ***
I(AGE^4)      2.865e-02  8.742e-04  32.776   <2e-16 ***
educ_college  2.902e+04  3.983e+02  72.862   <2e-16 ***
educ_advdeg   5.060e+04  4.432e+02 114.191   <2e-16 ***
FAMSIZE       6.622e+03  4.688e+02  14.124   <2e-16 ***
I(FAMSIZE^2) -1.123e+03  9.460e+01 -11.871   <2e-16 ***
I(FAMSIZE^3)  4.486e+01  5.030e+00   8.918   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 60270 on 163148 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1703,	Adjusted R-squared:  0.1702 
F-statistic:  3721 on 9 and 163148 DF,  p-value: < 2.2e-16

> summary(mod5)

Call:
lm(formula = (INCWAGE ~ AGE + I(AGE^2) + I(AGE^3) + I(AGE^4) + 
    educ_college))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-72108 -28918  -8135   6720 644720 

Labels:

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  -4.122e+04  4.833e+03  -8.527   <2e-16 ***
AGE           6.036e+02  4.568e+02   1.321    0.186    
I(AGE^2)      1.557e+02  1.469e+01  10.599   <2e-16 ***
I(AGE^3)     -3.693e+00  1.942e-01 -19.012   <2e-16 ***
I(AGE^4)      2.158e-02  9.035e-04  23.884   <2e-16 ***
educ_college  1.899e+04  4.031e+02  47.111   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 62710 on 163152 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.1019,	Adjusted R-squared:  0.1019 
F-statistic:  3702 on 5 and 163152 DF,  p-value: < 2.2e-16

> library("AER")
> Im<-lm(INCWAGE ~ log(AGE) + female + I(female*AGE) + I(female*(AGE^2)+I(female*(AGE^3))+educ_college +educ_advdeg+FAMSIZE +I(FAMSIZE^2)+ I(FAMSIZE^3))) 
> Im2<-lm(log1p(INCWAGE) ~ AGE  + female + I(female*AGE) + I(female*(AGE^2)+I(female*(AGE^3))+educ_college +educ_advdeg+FAMSIZE +I(FAMSIZE^2)+ I(FAMSIZE^3)))
> summary(Im)

Call:
lm(formula = INCWAGE ~ log(AGE) + female + I(female * AGE) + 
    I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + 
        educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)))

Residuals:
<Labelled double>: Wage and salary income
   Min     1Q Median     3Q    Max 
-50431 -32697 -15302  12547 636555 

Labels:

Coefficients:
                                                                                                                 Estimate
(Intercept)                                                                                                     1.884e+03
log(AGE)                                                                                                        1.066e+04
female                                                                                                         -3.219e+04
I(female * AGE)                                                                                                 9.232e+02
I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)) -1.629e-01
                                                                                                               Std. Error
(Intercept)                                                                                                     1.950e+03
log(AGE)                                                                                                        5.139e+02
female                                                                                                          1.268e+03
I(female * AGE)                                                                                                 3.578e+01
I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3))  3.440e-03
                                                                                                               t value
(Intercept)                                                                                                      0.966
log(AGE)                                                                                                        20.746
female                                                                                                         -25.381
I(female * AGE)                                                                                                 25.802
I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)) -47.365
                                                                                                               Pr(>|t|)
(Intercept)                                                                                                       0.334
log(AGE)                                                                                                         <2e-16
female                                                                                                           <2e-16
I(female * AGE)                                                                                                  <2e-16
I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3))   <2e-16
                                                                                                                  
(Intercept)                                                                                                       
log(AGE)                                                                                                       ***
female                                                                                                         ***
I(female * AGE)                                                                                                ***
I(female * (AGE^2) + I(female * (AGE^3)) + educ_college + educ_advdeg + FAMSIZE + I(FAMSIZE^2) + I(FAMSIZE^3)) ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 64970 on 163153 degrees of freedom
  (33427 observations deleted due to missingness)
Multiple R-squared:  0.036,	Adjusted R-squared:  0.03598 
F-statistic:  1523 on 4 and 163153 DF,  p-value: < 2.2e-16

> graph_observ<-(runif(NNobserv)<0.1)
> data_to_graph<-subset(dat_use,graph_observ)
Length of logical index must be 1 or 1231, not 196585
> plot(INCWAGE ~ jitter(AGE, factor = 2), pch = 16, col = rgb(0.5, 0.5, 0.5, alpha = 0.2), data = dat_use)
> # ^^ that looks like crap since Wages are soooooooo skew!  So try to find some sensible ylim = c(0, ??)
> plot(INCWAGE ~ jitter(AGE, factor = 2), pch = 16, col = rgb(0.5, 0.5, 0.5, alpha = 0.2), ylim = c(0,150000), data = dat_use)
> modPredict<-data.frame(AGE= 25:55, female = 1, AfAm=1,FAMSIZE=1,educ_nohs=1,educ_college = 0, educ_advdeg= 0)
> modPredict$yhat<- predict(mod4, newdata = modPredict)
> summary(modPredict)
      AGE           female       AfAm      FAMSIZE    educ_nohs  educ_college
 Min.   :25.0   Min.   :1   Min.   :1   Min.   :1   Min.   :1   Min.   :0    
 1st Qu.:32.5   1st Qu.:1   1st Qu.:1   1st Qu.:1   1st Qu.:1   1st Qu.:0    
 Median :40.0   Median :1   Median :1   Median :1   Median :1   Median :0    
 Mean   :40.0   Mean   :1   Mean   :1   Mean   :1   Mean   :1   Mean   :0    
 3rd Qu.:47.5   3rd Qu.:1   3rd Qu.:1   3rd Qu.:1   3rd Qu.:1   3rd Qu.:0    
 Max.   :55.0   Max.   :1   Max.   :1   Max.   :1   Max.   :1   Max.   :0    
  educ_advdeg      yhat      
 Min.   :0    Min.   :10134  
 1st Qu.:0    1st Qu.:24553  
 Median :0    Median :33450  
 Mean   :0    Mean   :29790  
 3rd Qu.:0    3rd Qu.:36605  
 Max.   :0    Max.   :37810  
> lines(yhat~AGE,data= modPredict)
> lines(yhat~FAMSIZE,data= modPredict)
