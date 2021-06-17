[Back](https://zenjen-devs.github.io)

# Statistical Data Analysis
<br>
<b>Navigate to:</b> <a href="#publications">Publications</a> | <a href="#currentprojects">Current Projects</a>

---

<h2 id="currentprojects">Current Projects</h2>


#### Working with *SAS* and *R*: Modeling outcomes with wide-format or clustered data (common violation of heteroskedasticity for linear regression)

Mixed-effects models offer a solution for modeling outcomes when faced with the common violation of the assumptions needed for linear regression--heteroskedasticity by group membership. Both **SAS** and **R** can accomodate this setting with `proc mixed` and `nlme` library, respectively.

This data comes from a real-based example of vitamin D supplementation of juice. Four suppliers claimed that their juice provided 100 IU of vitamin B. The null hypothesis is that the suppliers deliver this accurately, but there is a question as to whether the variance was the same between the juice suppliers. Hence, we need to explore allowing different variances by group.

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
100              3
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
value = c(78,88,92,89,94,103,124,101,100,89,107,83,97,81,93,88)
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

[View Programs in Github](https//github.com/jenarriaz/mixed-models)
###### Credits: [Ben Bolker/Rpubs](https://rpubs.com/bbolker/66298), [Ken Kleinmen/SASandR](https://www.amazon.com/gp/product/1466584491/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=1466584491&linkCode=as2&tag=sasandrblog-20)

<br>
<b>Navigate back to:</b> <a href="#currentprojects">Current Projects</a> ⤴️
<br>

---

<h2 id="publications">Co-Authorship on Academic Papers for Publication</h2>

### Efficacy Of Sulforaphane In Treatment Of Children With Autism Spectrum Disorder With and Without Severe Cognitive Impairment: A Randomized Double-Blind Placebo-Controlled Multi-Center Trial *(Manuscript Submitted)* 

<span style="float: right; color: rebeccapurple;"><h4>Synopsis of Statistical Data Analysis Methods:</span></h4>
This study included a number of observations within individual subjects, so that each indivudal is a cluster. We utilized mixed model analysis using SAS `proc mixed` to handle missing data, from drop-outs or other causes, in the analysis. The main analysis included baseline scores as covariate. Effect size for the overall mixed model treatment effect was computed for variables with statistically significant treatment effects or strong trends, using additionally developed SAS syntax based on the suggestions of [Tippey & Longnecker](http://www.scsug.org/wp-content/uPBOads/2016/11/Ad-Hoc-Method-for-Computing-Effect-Size-for-Mixed-Models_PROCEEDINGS-UPDATE-1.pdf). Corrected significance levels across scales or subscales for a specific variable was assessed by Benjamini-Hochberg (BH) protected significance level (at α=.05). Effect size at individual time points were analyzed by computation in an Excel program for treatment and control groups with Cohen’s *d* and Hedges correction.
<br><br>
<sup>
  <b>Authors:</b> <br>
JianJun Ou M.D., Ph.D, Robert C. Smith M.D. Ph.D, Russel Tobe M.D., Jingjing Lin M.M, Jen Arriaza, et al.
</sup>
<br>

---

<br>

### Sulforaphane Effects on Cognition and Symptoms in First-Episode Schizophrenia: A Randomized Double-Blind Trial *(Manuscript Submitted)* 
<img align="right" src="images/distributionicon.png?raw=true"/>
<span style="float: right; color: rebeccapurple;"><h4>Synopsis of Statistical Data Analysis Methods:</span></h4>

The analysis of symptom and cognitive variables used mixed model analysis using SAS `proc mixed` proecdure to handle missing data, from drop-outs or other causes, in the analysis. If variables deviated markedly from the normal distribution, transformations (log, square root) were attempted before analysis to achieve a better approximation to normal distribution; where distributions were still very skewed, we developed syntax for mixed model with non-normal distributions using `proc glimmix` and appropriate transformations.

<br>
<sup>
  <b>Authors:</b><br> 
Renrong Wu M.D. Ph.D, Robert C. Smith M.D. Ph.D, Gangrui Hei M.D., Ranran Li M.D. Ph.D，
Jianjun Ou, M.D. Ph.D, Xueqing Song M.D. Ph.D, Yinjun Zheng M.D. Ph.D，Yiqun He M.D. Ph.D，Jen Arriaza, et al.
</sup>
<br>

---
