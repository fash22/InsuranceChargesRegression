# Identifying the Key Drivers affecting Premium Charges on the US Health Insurance Dataset
![Photo by [Vlad Deep](https://unsplash.com/@vladdeep)](images/vlad-deep-mCqi3MljC4E-unsplash.jpg)

In the context of rising healthcare costs in the United States, there is a pressing need to understand the factors that influence health insurance premiums. Despite the availability of extensive data, there remains a gap in predictive models that can accurately estimate insurance charges based on individual demographics and health profiles. This project aims to bridge this gap by examining the US Health Insurance Dataset to identify key determinants of insurance costs. The outcome will not only provide valuable insights for policyholders but also assist insurance companies in creating fair and equitable pricing strategies.

## Key Insights:

### Exploratory Data Analysis
This dataset is comprehensive, featuring **1338 rows** and **7 columns**, encapsulating a robust **9366 data points**. Impressively, it maintains complete integrity with no missing values and only a single instance of duplication.

When examining the distribution patterns, we find that `age`, `bmi`, and `charges` are continuous variables. `Age` displays a uniform distribution, `bmi` follows a normal curve, and `charges` diverge with a skewed distribution. The `children` variable stands out as an unbalanced ordinal variable, predominantly representing insured individuals without children. The `charges` variable is a continuous variable with a large amount of outlier on the right side of its distribution.

Delving into class balance, `gender` and `region` showcase an equitable distribution across their respective classes. In contrast, the `smoker` variable reveals a pronounced skewness, with a higher prevalence of non-smokers in the dataset.

Correlation analysis unveils that `age` and `bmi` are the top influencers on `charges`, with Pearson correlation coefficients of $0.3$ and $0.2$, respectively. Although these figures suggest a weak correlation, a deeper look through the Spearman rank correlation coefficient indicates a strong relationship between `age` and `charges`. This suggests that `charges` tend to rise with age, albeit in a non-linear fashion.

When examining the distribution of premium charges, non-smokers shows a much lower premium charges regardless of gender and their number of children, and which region they live.

### Hypothesis Testing
Through rigorous inferential statistical analysis, we have substantiated our exploratory data analysis observations. Our methodical approach commenced with a power analysis to ascertain the minimal sample size necessary for detecting a substantial effect. Utilizing an effect size of $0.8$, an alpha (type-1 error rate) of $5\%$, and a statistical power of $80\%$, we determined a requisite sample size of at least 26 to discern large effects.

Subsequently, we employed a quantile-quantile plot for a preliminary visual assessment of sample distribution, focusing on the log-transformed charges. This graphical analysis was augmented with hypothesis testing to evaluate the normality of the distribution. The outcomes affirmatively indicated that our samples originate from a normal distribution.

A t-test analysis enabled us to confirm the absence of significant disparities in the mean log-charges between male and female insured individuals. Conversely, a pronounced difference was observed between smokers and non-smokers, with smokers incurring higher charges.

Geographically, we analyzed the mean log-charge discrepancies across regions. The findings revealed no notable differences, with the exception of the northeast and southeast regions. Notably, residents of the southeast region incurred significantly lower charges compared to their northeast counterparts.

### Linear Regression Modelling
In this notebook, we performed machine learning modelling using multiple linear regression using an ML pipeline. In this pipeline, we streamlined the data preprocessing stage, polynomial feature generation, and linear regression modelling. We conducted grid search on our polynomial feature generator stage and found that the optimal degree of features was 4. The model performs optimally when it uses interaction terms and without bias terms.

The linear model's metrics shows that our model's training and cross validation score were close to each other. This indicates that our model's performance generalizes well on unseen data.
However, the mean absolute error of our model shows that for both training and cross validation data, the model's prediction were off by $\$4000.00$. In addition, the model's $R^2$ statistic shows that it can only explain 60% of the variance of our dataset. These two are evidence that our model suffers from a high bias.

Given that the residual plot of our model does not exhibit a normally distributed data centered at $0$, we cannot give an accurate inference about the effects of each predictor on premium charges.

All in all, the linear model do helped us identify the key factos driving premium charges. The top features affecting the premium charges were `smoker`, sum of `age` and `age^2`, `bmi`, and `children`. Since our model's residuals does not exhibit a normally distributed data centered at 0, we cannot make an accurate inference about the data. If we desire to quantify the imact of features on premium charges, it is advisable to use an alternative interpretable ML model like decision tree.

### Decision Tree Modelling
The generated decision tree model's residual plot shows a normally distributed data centered at zero, but still contains long tails on the negative spectrum. The prediction error plot shows a more linear relationship between the predicted values and the actual values.

In terms of variance, the generated decision tree model has an $R^2$ of $0.86$. This means that our model explains 86% of the variance of our data. In terms mean absolute error, the values of the mean absolute error on training and testing data were at $\$2,015.53$ and $\$2,234.00$, respectively. The difference of their scores were only $\$218.47$. This means that our model has little variance problem. However, since the model's prediction on the training and testing data were off by $\$2000.00$ the model still suffers from bias problem.

The generated decision tree plot of the model shows that deciding factor of premium charges for non-smokers was age and number of children. The higher the age, the higher the premium charge. In the case of smokers, the main deciding factor for premium charge were bmi and age. The higher both of these values are, the high was the premium charge.


All in all, our decision tree model performs much better than its linear regression counterpart. Aside from performance, the generated decision tree plot enables us to interpret how the model predicts premium charge using all of the features of our dataset.