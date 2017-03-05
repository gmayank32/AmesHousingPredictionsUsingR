# AmesHousingPredictionsUsingR
Different Linear Regression Models have been used to make predictions on Ames Housing Data

Following Errors were encountered and how it was resolved:
1) using best subset selection
NA because there are 76 predictors and observations are more than 60
and this method is applicable when no of observations are less than 21 or p>n

2) if there is a categorical variable that has only one level then lasso model will not work and it will throw this error
Since you know that the error will only occur with factor/character, you can focus only on those and see whether the length of levels of those factor variables is 1 (DROP) or greater than 1 (NODROP).
l<-sapply(iris,function(x)is.factor(x))
m<-iris[,names(which(l=="TRUE"))]
ifelse(n<-sapply(m,function(x)length(levels(x)))==1,"DROP","NODROP")

3) it is possible that one categorical variable in training data has more levels than in test data. In that case, using model.matrix inside predict will throw this error
Cholmod error 'X and/or Y have wrong dimensions' at file ../MatrixOps/cholmod_sdmult.c, line 90
Remove all those predictors where levels for test and train is different


4) sapply(colnames(Housing),function(x)hetcor(Housing[,x],Housing[,!(colnames(Housing) %in% x)],method ="pearson",use="pairwise"))

