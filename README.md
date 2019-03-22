# Starbucks_Capstone_DSND
Starbucks capstone project for Data Scientist Nanodegree

**Table Of Contents**

1. [Installation](#installation)
2. [Project Overview](#project)
3. [Data Sets](#data)
4. [File Descripton](#file)
5. [Results](#results)
6. [Licensing](#licensing)
7. [Acknowledge](#ackowledge)

## Installation<a id="installation"></a>

The project is supported by Python 3.x libraries and packages:

- Numpy
- Pandas
- Seaborn
- Matplotlib
- Sci-kit tool

## Project Overview<a id="project"></a>

This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks. 

Not all users receive the same offer, and that is the challenge to solve with this data set.

Your task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products.

Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. You'll see in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

You'll be given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer. 

Keep in mind as well that someone using the app might make a purchase through the app without having received an offer or

## Data Sets<a id="data"></a>
he data is contained in three files:

* portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
* profile.json - demographic data for each customer
* transcript.json - records for transactions, offers received, offers viewed, and offers completed

Here is the schema and explanation of each variable in the files:

**portfolio.json**
* id (string) - offer id
* offer_type (string) - type of offer ie BOGO, discount, informational
* difficulty (int) - minimum required spend to complete an offer
* reward (int) - reward given for completing an offer
* duration (int) - time for offer to be open, in days
* channels (list of strings)

**profile.json**
* age (int) - age of the customer 
* became_member_on (int) - date when customer created an app account
* gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
* id (str) - customer id
* income (float) - customer's income

**transcript.json**
* event (str) - record description (ie transaction, offer received, offer viewed, etc.)
* person (str) - customer id
* time (int) - time in hours since start of test. The data begins at time t=0
* value - (dict of strings) - either an offer id or transaction amount depending on the record


## File Description<a id="file"></a>

* [Starbucks_Capstone_notebook.ipynb](./Starbucks_Capstone_notebook.ipynb)

  The notebook is used to run code, which contains data wrangling, data exploration, and model build
  

* [Starbucks_Capstone_Project_Analysis](https://machinelearntolearn.home.blog/starbucks-capstone-challenge-udacity-dsnd-project/)

  The final report site
  
  
## Results<a id="results"></a>
  
10 types of offers based on different of offer_id are categroized. Based on the distribution of "offer recived", "offer viewd", and "offer completed", those offers has been enrolled into three divisions.

1. For informational offer (type 3 and 5), obviously, they don’t have offer completed due to they don’t target needed to be complete.
2. Regarding offer types 0,2 and 6, the number of completion is higher or close to the number of views. It inferred those types of offer are not very effective to motivate customers to purchase. Even though in type 2 the offer_completed is slightly higher than the offer viewed, but the offer viewed is much less than the offer received, which indicate this offer has less responsive for customers.
3. Types 1,4,7,8, and 9 are highly possible to be more effective offers.

![Screenshot](https://github.com/tahe0203/Starbucks_Capstone_DSND/blob/master/Pics/bar%20charg%20offers.png?raw=true)


The **effectiveness** of offer for the targeted customer is defined as such: in one offer type, this offer’s effective equals one if a customer’s view_conv_rate is 1 and complete_conv_rate is 1. Otherwise, the effective is zero.

**Grid Search method** is used to get optimal parameters by using **roc_auc** as the scoring metric. **AdaBoost** method as the classifier of the offer effective. 


The results of model for type offer 1,4,7,8,9 are shown by using F1_Sore and ROC_AUC_Score

| Offer Type | F1_Score  | ROC_AUC_Score  |
| :--------: | :-------: | :------------: |
|     1      |   0.6597  |     0.4894     |
|     4      |   0.3581  |     0.4761     |
|     7      |   0.3944  |     0.5103     |
|     8      |   0.4848  |     0.4711     |
|     9      |   0.6727  |     0.5090     |


## Licensing<a id="licensing"></a>

It is available below under MIT license. 

## Acknowledge <a id="ackowledge"></a>

This project is under the [Udacity Data Science Nanodegree](https://www.udacity.com/course/data-scientist-nanodegree--nd025).
