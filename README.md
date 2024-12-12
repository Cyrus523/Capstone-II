# Capstone-II

## Repo Overview: 
This repository contains my contribution to a group project tasked with participating in the 2018 Home Credit Default Risk challenge on Kaggle. The committed RMarkdown file includes an extensive data cleaning process (credit to my groupmate Joonas Tahvanainen), a neural network model trained on a cleaned dataset, a neural network model trained on an uncleaned dataset, and resulting comparative insights. 

## Summary of business problem and project objective
As exlpained in the Kaggle challenge, Home Credit wants to expand their customer base to unbanked clients. In order to provide loans to this prospective customer base, Home Credit needs a reliable machine learning model that can predict loan default risk for un-banked clients.

Our objective for this project is to build, test, and compare multiple machine learning models, to see which model will predict on Home Credit's customer data the best. 

## Our group's solution to the business problem.
We tested the following four models:
1. PCA+Decision Tree - Kaggle Score: 0.65
2. Random Forest - Kaggle Score: 0.54
3. Neural Network - Kaggle Score: 0.72
4. XGBoost - Kaggle Score: 0.67

Our group centered our solution around which model produced the highest Kaggle score. In theory, the model with the highest Kaggle Score will be the best in practice at predicting loan default. Of the four models we trained, the neural network model performed the best on the hold-out dataset with the highest Kaggle Score of 0.72. We also chose the neural model because it produced a Kaggle Score of 0.69 when trained on an uncleaned dataset. This meant that the model proved intrinsically robust enough to be utilized by a potentially resource-limited data science department. 

## contribution and difficulties to the project
### Disclaimer
I would first like to clarify that the data cleaning portion of the committed code (lines 42-425) was produced by my groupmate Joonas Tahvanainen, who deserves the credit for extensively cleaning the data. This portion of the code was left in the committed file because I needed the cleaned dataset to compare the neural network's performance against itself when trained on cleaned/uncleaned data. 

### My contribution
My contribution to the project was the neural network modeling (lines 425-847). I first wanted to see how the model would perform without any data cleaning. This resulted in a modest 0.69 Kaggle Score. After reviewing my findings with my professor, I was advised that "there are no free hunches" in data science, and that I must test performance of a model trained on the cleaned dataset. As stated above, the cleaned model produced a Kaggle Score of 0.72, showing that refining the data increased model performance. I also wanted to ensure that the model could be deemed a "good" classification model, regardless of it's Kaggle Score. To do this, I generated a receiver operating characteristic ("ROC") curve and calculated the area underneath. As we can see from the output, the area under the curve ("AUC") is 0.68. This is a mediocre AUC, but was deemed sufficient enough for solving the business case.

### Difficulties 
The primary difficulty I faced in this project was predicting on large datasets using the RWeka package. When predicting on large datasets, the predict function from the RWeka package would throw a java.lang.OutOfMemoryError. This is a Java heap space error that indicates the Java application is trying to allocate more memory on the heap than is available. As you will see in lines 718-772, I needed to iteratively predict on subsets of the data, and append them to a larger vector for analysis. This difficulty centered more around difficulties using the chosen tools, rather than theoretical issues with solving the business case. Once the code was debugged, the resulting model(s) were able to satisfy the business requirements.

As a group we all worked quite independenty on the modeling portion of our project. As such we did not share any difficulties besides tailoring Joona's data cleaning code to fit our individual models. 

## The business value of the solution.
We will be able to provide Home Credit with a robust predictive model capable of predicting loan defaults with 72% accuracy. We also leveraged the bureau metadata, which significantly increased the amount of metadata our model is trained on. This means Home Credit will be able to leverage variances in portions of their metadata, without having to focus all of their efforts on ensuring 100% of a customer profile is complete before being modelled. Again, this goes back to the point of robustness, where we wanted to provide a model that was easy to implement. This came at the cost of reduced accuracy, but it was a decision we felt would ultimately provide more operational value within Home Credit.

## Lessons learned.
1. "There are no free Hunches". As stated previously, it is imperative as a data scientist that all angles of an approach be investigated, or at the very least, recognized. Providing a model Home Credit, trained on uncleaned data alone, would have robbed Home Credit of a more accurate model. This edge in performance can equate to significant cost savings for businesses.
2. It is important that datascientists become proficient with the tools needed to perform these analyses. The difficulties faced in predicting with the RWeka packaged showed that theory alone is not enough to solve a business case. You have to understand how to solve the problem both at a high level and down to the syntax.
3. Collaboration is key. In the beginning of our project, we all built our models separately. This resulted in training our models on datasets with various levels of cleaning. This meant we were unable to fairly compare our model's performance. Two things happened when we trained our models on a shared cleaned dataset. One, all of our model performances improved. Two, we were able to confidently make a decision on which model would solve the business case the best. 
