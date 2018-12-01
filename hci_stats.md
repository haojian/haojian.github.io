# Haojian's Stats Wiki



### factor analysis
[Factor analysis for likert survey data](https://www.promptcloud.com/blog/exploratory-factor-analysis-in-r/)


```
####### Example code
> library(GPArotation)
> library(psych)
> df47 <- read.table("/Users/haojian/projects/privacy_expectation_empirical/notebook/data_p47.csv", header = TRUE, sep = ",")
> sel47 = subset(df47,  select = c(6, 7, 9, 10, 13, 14, 15, 16, 17, 5, 12, 2, 3, 19))
> threefactor <- fa(sel47,nfactors = 5,rotate = "varimax",fm="minres")
> print(threefactor$loadings,cutoff = 0.3)
> library(GPArotation)
> corrplot(cor(sel47), method="ellipse")
> KMO(cor(sel47))
> print(threefactor)
```

[Correlation figure](http://www.karlin.mff.cuni.cz/~maciak/NMST539/cvicenie8.html)

