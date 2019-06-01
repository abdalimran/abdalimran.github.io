---
layout: post
title: Drawing multiple ROC-Curve in a single plot
category: 
  - "Visualization"
  - "Machine Learning"
mathjax: true
---

# What is AUC-ROC Curve?

AUC-ROC curve is a performance metric for binary classification problem at different thresholds. 
ROC is a probability curve and AUC represents the degree or measure of separability. 
It tells how much model is capable of distinguishing between classes. 
Higher the AUC, better the model is at predicting 0s as 0s and 1s as 1s.

The ROC curve is plotted with **False Positive Rate** in the **x-axis** against the **True Positive Rate** in the **y-axis**.

You may face such situations where you run multiple models and try to plot the ROC-Curves for each model in a single plot. 
Plotting multiple ROC-Curves in a single figure makes it easier to analyze model performances and find out the best performing model.

Let's begin. We'll use *Pandas, Numpy, Matplotlib, Seaborn and Scikit-learn* to accomplish this task.

# Importing the necessary libraries
{% highlight python %}
import pandas as pd
import numpy as np
%matplotlib inline
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

import warnings
warnings.filterwarnings('ignore')
{% endhighlight %}

# Making a toy Dataset
{% highlight python %}
from sklearn import datasets
from sklearn.model_selection import train_test_split

data = datasets.load_breast_cancer()

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, 
                                                    test_size=.25,
                                                    random_state=1234)
{% endhighlight %}

# Training multiple classifiers and recording the results
In this phase we'll perform a few steps:
1. Instantiate the classifiers and make a list
2. Define a result table as a DataFrame
3. Train the models and record the results

Here, we'll train the models on the **training set** and *predict the probabilities* on the **test set**. 
After predicting the probabilities, we'll calculate the **False positive rates, True positive rate, and AUC scores**.

{% highlight python %}
# Import the classifiers
from sklearn.linear_model import LogisticRegression
from sklearn.naive_bayes import GaussianNB
from sklearn.neighbors import KNeighborsClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier

# Instantiate the classfiers and make a list
classifiers = [LogisticRegression(random_state=1234), 
               GaussianNB(), 
               KNeighborsClassifier(), 
               DecisionTreeClassifier(random_state=1234),
               RandomForestClassifier(random_state=1234)]

# Define a result table as a DataFrame
result_table = pd.DataFrame(columns=['classifiers', 'fpr','tpr','auc'])

# Train the models and record the results
for cls in classifiers:
    model = cls.fit(X_train, y_train)
    yproba = model.predict_proba(X_test)[::,1]
    
    fpr, tpr, _ = roc_curve(y_test,  yproba)
    auc = roc_auc_score(y_test, yproba)
    
    result_table = result_table.append({'classifiers':cls.__class__.__name__,
                                        'fpr':fpr, 
                                        'tpr':tpr, 
                                        'auc':auc}, ignore_index=True)

# Set name of the classifiers as index labels
result_table.set_index('classifiers', inplace=True)
{% endhighlight %}

# Plot the figure
{% highlight python %}
fig = plt.figure(figsize=(8,6))

for i in result_table.index:
    plt.plot(result_table.loc[i]['fpr'], 
             result_table.loc[i]['tpr'], 
             label="{}, AUC={:.3f}".format(i, result_table.loc[i]['auc']))
    
plt.plot([0,1], [0,1], color='orange', linestyle='--')

plt.xticks(np.arange(0.0, 1.1, step=0.1))
plt.xlabel("Flase Positive Rate")

plt.yticks(np.arange(0.0, 1.1, step=0.1))
plt.ylabel("True Positive Rate")

plt.legend(loc=4)
plt.show()
{% endhighlight %}

**Output:**
![alt text](/images/multiple_roc_curve.png "Multiple ROC Curve.png")


Use the following code to export the figure.
{% highlight python %}
fig.savefig('multiple_roc_curve.png')
{% endhighlight %}
