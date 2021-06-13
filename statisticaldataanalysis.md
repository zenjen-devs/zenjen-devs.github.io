[Back](https://zenjen-devs.github.io)

### Statistical Data Analysis
#### Current Project: Mixed-Effects Models


Mixed-effects models offer a solution for modeling outcomes when faced with the common violation of the assumptions needed for linear regression--heterscedasticity by group membership. Both **SAS** and **R** can accomodate this setting with `proc mixed` and `nlme` library, respectively.

This data comes from a real example of vitamin D supplementation of juice. Four suppliers claimed that their juice provided 100 IU of vitamin B. The null hypothesis is that the suppliers deliver this accurately, but there is a question as to whether the variance was the same between the juice suppliers. Hence, we need to explore allowing different variances by group.

There exists four observations for each supplier, as observed in the data below--this command inputs the data into SAS.

```sas
data juice;
input value juice_cat;
cards;
78               1
88               1
92               1
89               1
94               2
103              2
124              2
101              2
101              3
89               3
107              3
83               3
97               4
81               4
93               4
88               4
;;
run;
```

##### Fitting the Model: SAS

The `group` option in the `repeated` statement in `proc mixed` is specifically designed to allow different values for groups sharing the same covariance structure. Alternatively, if we were analyzing repeated measures of individual units of juice (clustered) we'd use the `subject` option instead of group. For this data, the covariance structure is `simple`: no constant value on the diagnal and no correlation. The function will use REML by default, but it's better to use maximum likelihood when assessing variance terms.

```sas
ods select covparms lrt;
proc mixed data = juice method = ml;
class juice_cat;
model value = juice_cat/solution;
repeated/group=juice_cat type = simple;
title 'Modeling Juice suppliers Vitamin B UI Levels'; 
run;
```

Output:

```
  Covariance Parameter Estimates

Cov Parm     Group         Estimate

Residual     juice_cat 1     27.1915
Residual     juice_cat 2      150.59
Residual     juice_cat 3      100.79
Residual     juice_cat 4     22.1915


  Null Model Likelihood Ratio Test

    DF    Chi-Square      Pr > ChiSq

     3          5.02          0.1598

```

The output indicates there's little to support difference variances, but the statistical power is likely to be minimal, so this model can be retained when assessing the null hypothesis of equal means. `proc mixed` will not determine the accurate degrees of freedom remaining automatically, so we need to directly specificy the denominator degrees of freedom by including a `ddf` option in the `model` statement. 

```sas
ods select solutionf tests3;
proc mixed data = milk method = ml;
class milk_cat;
model value = milk_cat/solution ddf=8;
repeated/group=milk_cat type = simple;
run;
```

Output:

```
        Type 3 Tests of Fixed Effects

              Num     Den
Effect         DF      DF    F Value    Pr > F

juice_cat        3       8       3.83    0.0523

```

The results indicate that there may be reason to suspect that the juice suppliers may be different.


##### Fitting the Model: R

In R, we'll do the same by inputting the data like so and assigning the group labels manually.

```r
value = c(77,85,91,88,93,101,126,103,103,88,109,85,95,83,91,86)
mc = as.factor(rep(1:4, each=4))
milk= data.frame(value, mc)
```
To fit the model with unequal variances as I did previously in SAS, we'll use the `gls()` function in the `nlme` library.


```r
library(nlme)
mod = gls(value~mc, data=juice, weights = varIdent(form = ~1|mc), 
   method="ML")
```

Here we use the `anova()` function to assess the hypothesis of equal variances and compare to our previous homoscedasticity model.

```r
mod2 = gls(value~mc, data=juice, method="ML")
anova(mod,mod2)
```

The results output are identifical to SAS, although the programs use different test statistics (likelihood ratio vs. Wald's). But to assess whether suppliers are different, one must compare to the model wit just an intercept and keeping the maximum likelihood methodology for consistency.

```r
mod3  = gls(value~1,data=juice, weights = varIdent(form = ~1|mc), method="ML")
anova(mod3,mod)
```
Output:

```
     Model df  ...  p-value
mod3     1  5                         
mod      2  8       0.0523

```
Conclusively, both programs achieve the same results--there may be some evidence that the juice suppliers are different. 

---
###### Credits: [Ben Bolker/Rpubs](https://rpubs.com/bbolker/66298), [Ken Kleinmen/SASandR](https://www.amazon.com/gp/product/1466584491/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=1466584491&linkCode=as2&tag=sasandrblog-20)
