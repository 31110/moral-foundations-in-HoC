
### Step 3: Analysis

#### Study 1

##### Logistic Regression

First, I create binary variables for either of the two party’s:

``` r
conlab$party1[conlab$party=="Labour Party"]<-1
conlab$party1[conlab$party=="Conservative Party"]<-0
```

Now, using the *g**l**m*2 package, I can run the logistic regression
model:

``` r
care_log <- glm(party1 ~ mean_care_p, data=conlab, family="binomial"(link='logit'))
summary(care_log)
```

I do this for each moral foundation.

#### Checking Assumptions

I check each assumption is met:

-   I visualise Cook’s distance values to check for influential values:

``` r
plot(care_log, which = 4, id.n = 3)
```

-   I use the *c**a**r* package function, *v**i**f*, to check for an
    absence of mlticollinearity:

``` r
car::vif(care_log)
```

-   I use the *c**a**r* package function,
    *b**o**x**T**i**d**w**e**l**l*, to test for linearity of independent
    variables:

``` r
boxTidwell(formula = party1 ~ mean_care_p,
           other.x = ~ mean_fairness_p + mean_authority_p + mean_loyalty_p + mean_sanctity_p,
           data = data)
```

##### ANOVA Tests

To carry out the ANOVA tests on each parties’ mean value for each moral
foundation, I first calculate the mean for each party:

``` r
caremeans <- group_by([dataframe], party) %>%
  summarise(
    count = n(),
    mean = mean(mean_care_p, na.rm = TRUE),
    sd = sd(mean_care_p, na.rm = TRUE)
  )
```

I then use the *a**o**v*() function to conduct the ANOVA test, for
example:

``` r
care.aov <- aov(mean_care_p ~ party, data = [dataframe])
summary(care.aov)
```

I do the same for Tukey’s HSD test:

``` r
TukeyHSD(care.aov)
```

I can visualise these results using the *g**g**p**l**o**t* package to
create bar charts, etc.

#### Study 2

##### Linear Regression

First, I calcuate the average polling for each quarter, for each party.
For example:

``` r
conpoll <-
  data %>% 
  group_by(YearQuarter)  %>% 
  summarise(mean_con_poll = mean(Con, na.rm=TRUE))
```

I then regress the average moral foundation endorsement probabilities on
the next quarter’s polling. For example:

``` r
con<-lm_robust(lag(conpoll)~concare + conauth + conloy +
                 consan + confair + congov + labgov, data=pollmorals, se_type="classical")
summary(con)
```

To check the assumptions of the linear regression hold, foe each model,
I use the following function to observe the appropriate plots:

``` r
autoplot([model])
```
