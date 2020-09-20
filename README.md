# Heart Health Predictions

Table of Contents
1. [ Introdcution. ](#intro)
2. [ Implementation. ](#implem)


Using a dataset from Kaggle predictions have been made on patient heart data to determine cardiovascular events and to find any clear indications of heart health.

![Credit: favpng.com](broken_heart.png)

<a name="intro"></a>
## 1. Introduction
classified if patients have heart disease or not according to features in it. We will try to use this data to create a model which tries predict if a patient has this disease or not. We will use logistic regression (classification) algorithm.

After a disaster has occurred millions of communications are exchanged right at the time that disaster response organizations have the least capacity to categorize important messages to let relevant organizations know who needs help.
Different organizations would generally take care of specific parts of the problem, like water, medical supplies, blocked roads. These are some of the categories that Figure Eight has pulled out of the data.
The expectation is that this project could be used in future disaster relief projects to benefit people affected during hard times.

Supervised machine learning is used and is more accurate than a person performing keyword searches, which is an issue in disaster relief. The data has been repaired with an ETL pipeline and then a machine learning pipeline has been used to build a supervised learning model.

## The Data
The columns and their descriptions are as follows:

age - age in years
sex - (1 = male; 0 = female)
cp - chest pain type
trestbps - resting blood pressure (in mm Hg on admission to the hospital)
chol - serum cholestoral in mg/dl
fbs - (fasting blood sugar > 120 mg/dl) (1 = true; 0 = false)
restecg - resting electrocardiographic results
thalach - maximum heart rate achieved
exang - exercise induced angina (1 = yes; 0 = no)
oldpeak - ST depression induced by exercise relative to rest
slope - the slope of the peak exercise ST segment
ca - number of major vessels (0-3) colored by flourosopy
thal - 3 = normal; 6 = fixed defect; 7 = reversable defect
target - have disease or not (1=yes, 0=no)

## Questions
Can the data be analyzed to divide messages so that the right organizations would be of most help to the people who need it?

## Findings
### Building the model
Pipelines are used to take in the data from the database, put it through a tokenizer, tfidf transformer, two custom transformers which find messages related to death and children, and finally through a random forest classifier – to produce a trained model, which can then be used for prediction.

Using Scikit-learn’s FeatureUnion class makes it easy to write complex pipelines. Here smaller pieces (transformers) have been built and then combined horizontally.

Using Pipelines and FeatureUnions helped in the orgainzation of the code for readability, reusability and easier experimentation.

### What happened after adding these features?
Accuracy is low after applying a random forest classifier to the data. An SGD classifier was also used, but since the train-test split produced some labels with just zeros there was no way of moving forward with this model.
Other classifers which support multi-labels will be tried in future versions of the app.

* sklearn.tree.DecisionTreeClassifier
* sklearn.tree.ExtraTreeClassifier
* sklearn.ensemble.ExtraTreesClassifier
* sklearn.neighbors.KNeighborsClassifier
* sklearn.neural_network.MLPClassifier
* sklearn.neighbors.RadiusNeighborsClassifier
* sklearn.ensemble.RandomForestClassifier
* sklearn.linear_model.RidgeClassifierCV

Here we see in a message about flooding and missing children, only the flood output is highlighted. We would expect missing people to be a key aspect of the model output, especially since one of the custom transformers is dedicated to this.

![Example results](lost_in_flood.png)

Here we see a chart of the number of messages sent for key survival items.
Water is the only one which is used solely on social media to ask for help; we may assume that due the urgency of it's need, people ask for help on Facebook/ Twitter rather than tell a journalist they need water desparately. Maybe due to a lack of knowledge/availability of a direct water authority, people in-need have not used direct contact either.

![Example results](chart_vital.png)

## Conclusion
Accuracy is in the twenty percentages after applying a combination of parameters using a pipeline.
By adding in more features, and doing hyperparameter tuning, the accuracy still only reached less than 30%.

This may be expected due to the number of messages/tokens versus variables, though other classifiers are worth trying to increase the current accuracy.


------------------------------------------------------------------------------------------------------------------

<a name="implem"></a>
## 2. Implementation
## Technical Information

##### Pip Install
1. sklearn
1. nltk
1. plotly
1. flask
1. joblib

##### Libraries:
1. sys
1. re
1. numpy
1. pandas
1. pickle
1. sqlalchemy
1. nltk
1. sklearn
1. plotly
1. flask
1. joblib
1. json
1. sqlalchemy
1. sqlite3


### File Descriptions
1. process_data.py: cleans the data before adding it to a database
1. train_classifier.py: builds and evaluates a model for the data in the database and saves a dataframe to a pickle file, where the pickle library is used for serializing and deserializing objects.
1. transformation.py: creates the custom transformers to find specific terms in the messages.
1. run.py: runs the app in a web browser untilizing the database and model.
1. master.html: main html page for layout and styling of the web app.
1. go.html: outputs the model results to the web app.


1. messages.csv: messages created by thepublic in the native language, converted into english.
1. categories.csv: categories into which messages fall; water, medical, etc.
1. empty_shelves.jpg: a picture of empty shelves in a supermarket.


### Instructions:

### How To Interact With The Project
Install the files into a folder on your computer

1. Run the following commands in the project's root directory to set up your database and model.

    - To run ETL pipeline that cleans data and stores in database
        `python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db`
    - To run ML pipeline that trains classifier and saves
        `python models/train_classifier.py data/DisasterResponse.db models/classifier.pkl`

2. Run the following command to view the web app.
    `python app/run.py`

3. Go to http://0.0.0.0:3001/ to run the web app.


### Licensing, Authors, Acknowledgements

The data files were retrieved from [Kaggle]https://www.kaggle.com/nareshbhat/health-care-data-set-on-heart-attack-possibility.
Thanks to my mentors at [Udacity]https://www.udacity.com/ for supporting this project.
