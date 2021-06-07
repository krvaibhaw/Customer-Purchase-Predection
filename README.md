# Customer Purchase Predection

![](https://img.shields.io/badge/Excitement-High-red)
![](https://img.shields.io/badge/Maintained-Yes-indigo)
![](https://img.shields.io/badge/Pull_Requests-Accepting-yellow)
![](https://img.shields.io/github/forks/krvaibhaw/Customer-Purchase-Predection)
![](https://img.shields.io/github/contributors/krvaibhaw/Customer-Purchase-Predection)
![](https://img.shields.io/github/issues/krvaibhaw/Customer-Purchase-Predection)
![](https://img.shields.io/github/stars/krvaibhaw/Customer-Purchase-Predection)

![](https://img.shields.io/badge/Contributions-Accepting-pink)
![](https://img.shields.io/github/license/krvaibhaw/Customer-Purchase-Predection)
[![](https://img.shields.io/badge/By_Me_A_Coffee-Paypal-skyblue)](https://www.paypal.com/paypalme/krvaibhaw/100)

<br>

<p align="center">
<img src="/Preview/preview.png">
</p>


## Installation

1. Make sure [Python 3.6+](https://www.python.org/downloads/) is installed.
2. Install [scikit-learn](https://scikit-learn.org/stable/install.html).
3. Clone this repository  
```
    $ git clone https://github.com/krvaibhaw/Customer-Purchase-Predection.git
```
4. Change Directory
```
    $ cd Customer-Purchase-Predection
``` 
5. Install requirements  
```
    $ pip install requirements.txt
``` 
6. Run the program :
```
    $ python model.py <data folder path>/<file.csv>
```
Example :
```
    $ python model.py data/activity_data.csv
```

<br>

## Introduction

- Customer engagement is very important for any business model.
- In this project I tried to built an purchase prediction model for an online e-commerce platform, which will try to predict whether a customer will make a purchase or not, perhaps displaying different content to the user, like showing the user a discount offer if the website believes the user isn’t planning to complete the purchase.

## Motivation

- When users are shopping online, not all will end up purchasing something. 
- Most visitors to an online shopping website, in fact, likely don’t end up going through with a purchase during that web browsing session. 
- It might be useful, though, for a shopping website to be able to predict whether a user intends to make a purchase or not; perhaps displaying different content to the user, like showing the user a discount offer if the website believes the user isn’t planning to complete the purchase.

## Proposed Method

We began the evaluation by loading the customer activity dataset for a website using the command line argument. For the study, we have utilized customer online activity dataset for a website, involving parameters such as Traffic Type, Region, Product Related Duration, Product Related, Month, etc.

```python
    if len(sys.argv) != 2:
        sys.exit("Usage: python shopping.py data")

    evidence, labels = load_data(sys.argv[1])
```

It is necessary to convert categorical features into numerical because all the machine learning algorithms interprets only numeric values.Next step involves feature selection based on feature importance followed by replacing the string values numerical values. 

```python
    month_index = dict(Jan=0, Feb=1, Mar=2, Apr=3, May=4, June=5,
                       Jul=6, Aug=7, Sep=8, Oct=9, Nov=10, Dec=11)

    ( month_index[row["Month"]],
    1 if row["VisitorType"] == "Returning_Visitor" else 0,
    1 if row["Weekend"] == "TRUE" else 0 )

    labels.append(1 if row["Revenue"] == "TRUE" else 0)
```

The procedure involves taking a dataset and dividing it into two subsets. The first subset is used to fit the model and is referred to as the training dataset. The second subset is not used to train the model; instead, the input element of the dataset is provided to the model, then predictions are made and compared to the expected values. This second dataset is referred to as the test dataset. And then we prepare the training and test data for model using train_test_split( ) function from sklearn module.

* **Train Dataset** : Used to fit the machine learning model.
* **Test Dataset** : Used to evaluate the fit machine learning model


```python
    from sklearn.model_selection import train_test_split
    
    X_train, X_test, y_train, y_test = train_test_split(
        evidence, labels, test_size=TEST_SIZE
    )
```

Then we create aur K-nearest neighbours (KNN) model by using the sklearn model that we have installed in the requirement installation section. The KNN algorithm assumes that similar things exist in close proximity. In other words, similar things are near to each other.

```python
    def train_model(evidence, labels):

        model = KNeighborsClassifier(n_neighbors=1)
        model.fit(evidence, labels)

    return model
```


The training data will be used to train the KNN (k-nearest neighbors) model. And the test data will be used to validate the model. It will predict the labels for the given unseen feature vectors.

```python
    model = train_model(X_train, y_train)
    predictions = model.predict(X_test)
```

Finally, the model is then evaluated. Model evaluation aims to estimate the generalization accuracy of a model on future (unseen/out-of-sample) data.

```python
    sensitivity, specificity = evaluate(y_test, predictions)

    # Displaying the results

    print(f"Correct: {(y_test == predictions).sum()}")
    print(f"Incorrect: {(y_test != predictions).sum()}")
    print(f"True Positive Rate: {100 * sensitivity:.2f}%")
    print(f"True Negative Rate: {100 * specificity:.2f}%")
       
    # Displaying the classification report for model evaluation
    
    print("\nClassification Report\n")
    print(classification_report(y_test,predictions))
    print("Accuracy : ",accuracy_score(y_test,predictions)*100)
```


## Dataset

For the study I have used the customer online activity dataset for a website, involving parameters such as Traffic Type, Region, Product Related Duration, Product Related, Month, etc.

## Market Demand Of The Project

Contributing to the advancement of machine learning technologies, this project may be helpful for the online shopping website which are thriving to increase their customer engagement.

## Future Scope

Future scope of the project includes that it can be implemented at a larger scale in addition to other customer engagement parameters such as messaging system involving price drop in particular interested item, etc.


## Summary

During normal shopping online, the most common occurrence that is observed that not all users will end up purchasing some stuffs. Generally, majority of the visitors likely don't end up going through the purchase during that web session. So it would be beneficial for a e commerce website to predict whether a user intends to make a purchase or not and display different contents and offers accordingly, something like discount offers or coupons, etc, if the website suspects if the user is not intended to complete the purchase.

In order to solve this problem, we proceed by bulding a k-nearest classifier for classifing users in two predefined class i.e, whether they will complete the purchase or not based on features such as whetherthe users are shopping on a weekend, what web browser they’re using, how many pages they’ve visited, etc.
