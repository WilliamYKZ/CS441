# Classification 

## Classify

1. A **classifier** is a procedure that accepts a set of features and produces a class label for them. 



2. Two-class classifier example: credit card companies must decide whether a transaction is good or fraudulent.



3. What makes training classifiers interesting is that performance on training data doesn’t really matter. What matters is performance on run-time data, which may be extremely hard to evaluate because one often does not know the correct answer for that data.



## The Error Rate and Other Summaries of Performance 

1. We can summarize the performance of any particular classifier useing the **error** or **total error rate**.(the persentage of classification attempts that gave the wrong answer) and **accuracy** (the percetage of classification attempts that gave the right answer).



2. The minimum expected error rate obtained with the best possible classifier applied to a particular problem is known as the **Bayes risk**. In most case, it is hard to known what the Bayes risk is, because to compute it requires knowning $P(y|x)$, which isn't usually known. 



3. The error rate of a classifier is not that meaningful on its own, because we don't usually known the Bayes risk for a problem. It is more helpful to compare a particular classifier with some natural alternatives, sometimes called **baselines**. 



4. Classifier performance is summarized by either the total error rate or the accuracy. You will very seldom know what the best possible performance for a classifier on a problem is. You should always compare performance to baselines. Chance is one baseline that can be surprisingly strong.





## More Detailed Evaluation

1. **False positive rate:** the percentage of negative test data that was classified positive.
2. **False negative rate:** the percentage of positive test data that was classified negative.
3. **Sensitivity:** the percentage of true positives that are classified positive.
4. **Specificity:** the percentage of true negatives that are classified negative. 



