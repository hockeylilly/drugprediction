## Description
For this django-server the goal was to create a drug combination classification framework in the process of our 
Software-internship at the FU and it is supposed to serve two main purposes: 
1. input: groundtruth and feature data  output based on the first 3000 rows of the merged file: a pdf with all chosen models trained, a csv per 
each method with the prediction 
2. input: fature data output based on the first 3000 rows : a csv of predictions based on the chosen model
    WARNING: If you want to have a prediction of a certain model, you also have to train it first, 
    and also consider other parameters like scaling, feature_selection etc. 

## Installation Requirements
This server was created with Python 3.12 and Django 5.0.4
To run this server in your environment there are the following libraries required: 

- Django	5.0.4	
- PyPDF2  3.0.1
- Python  3.12
- django-debug-toolbar	4.3.0	(obviously needed only for debugging)
- fonttools	4.51.0	
- imbalanced-learn	0.12.2
- joblib	1.4.0		
- matplotlib	3.8.4		
- numpy	1.26.4	
- packaging	24.0	
- pandas	2.2.2
- reportlab	4.2.0
- scikit-learn	1.4.2	
- scikit-optimize	0.10.1
- scipy	1.13.0
- tqdm	4.66.2	
- wheel	0.41.2	
- xgboost	1.7.6	

## Setup and Installation
For the setup of this server you will need to download the required libraries, most importantly the mentioned 
Django and Python versions, then navigate to the directory "drug_prediction". If it is the first setup of 
the project you need to run "python manage.py makemigrations" and afterward "python manage.py migrate", 
to update the models.py.

To then run the server you need to run "python manage.py runserver" and you will receive a link to 
the website. Usually the server starts on Port 8000, that might cause errors if Port 8000 is already taken.

## Usage
On your website you will first be shown the home page, this simply serves as an interface to have a description of 
the project again. Then with the link "Go To Upload Page" you will be redirected to /predictor/upload/.
This is the actual tool and you will have the following options:

NOTE: For a lot of these user-chosen parameters the models have different requirements or options, if only
one option is available, the user input will be overwritten, so that the model can be trained normally. 
For more information, check out the table overview for models.

1. Upload feature data and/or groundtruth 

You always have to upload feature data, if there is no groundtruth data you will receive a prediction for 
your drug combination in tsv format with "0" meaning a predicted approved and "1" meaning a predicted adverse combination.
BRAUCHE NOCH STANDARD

If there is feature data and groundtruth data, the chosen models will be evaluated and you will receive a prediction 
on X_test as a tsv and a pdf with confusion matrizes and different evluation scores.

2. Hyptuning : BayesSearch(Default) or GridSearch

Except for a XGB, which as a sepcial case uses RandomizedSearch, our methods are hyperparameter trained by 
BayesSearch or GridSearch and then the models will be evaluated with these best parameters and standard parameters
both. 

3. Balancing method: None(Default) or ADASYN

4. Feature Selection None(Default) or rekursive feature elimination or selectkbest 

5. Random State: 42(Default) or any INT 
 
To make the user input reproducable, the user chooses a random state. 

6. Stratify: Yes/No(Default)

This decides if the train test split will be stratified or not.

7. Scaler Yes/No(Default)

This decides if the data will be scaled before hyperparameter tuning and training. 



# Table Overview for models

'rdf', 'Random Forest'
'svm', 'Support Vector Machine'
'knn', 'K-Nearest Neighbors'
'lda', 'Linear Discriminant Analysis'
'nvb', 'Naive Bayes'
'lgr', 'Logistic Regression'
'xgb', 'XGBoosting'

'slc', 'SelectKBest'
'rfe', 'Rekursive Feature Elimination'

'BS', 'BayesSearch'
'GS', 'GridSearch'

If an option is written normal, it is optional, meaning it works when activated yes or no. 
If an option is fat it means it is necessary, meaning if the user input is different it will 
be overwritten with the working concept. 

SELECTKBEST GEHT NOCH NICHT knn,rdf,lda


| rdf        | svm        | knn        | lda        | nvb        | lgr        | xgb        |
|------------|------------|------------|------------|------------|------------|------------|
| stratifier | stratifier | stratifier | stratifier | startifier | stratifier | stratifier |
| scaler     | scaler     | **scaler** | scaler     | **scaler** | scaler     | scaler     |
| ADASYN     | **ADASYN** | ADASYN     | ADASYN     | **ADASYN** | **ADASYN** | ADASYN     |
|            |            | slc        | rfe        | slc        |            |            |
| BS/GS      | **BS**     | **BS**     | BS/GS      | **BS**     | BS/GS      | RS*        |

*XGB is a special case, as it is the only model being trained with RandomizedSearch (only).

## Configuration

Before starting the project, ensure you configure the following:

- **Environment Variables**: Set `DB_HOST`, `DB_USER`, and `DB_PASS` to reflect your database host, username, and password respectively.
- **Dependencies**: Install all necessary dependencies by running `pip install -r requirements.txt`.

## Features

- **Drug prediction**: Users can input feature data to receive a prediction for the drugs based on the given features.
- **Drug prediction evaluation**: Users can input feature and groundtruth data and receive and evaluation on the chosen models
    using different scores in a pdf and csv file(s) that include the predictions.

## Credits and Acknowledgments
- **Thea Steuerwald**
- **Sofya Shorzhina**
- **Lilly Wiesmann**
- **Gesa Röefzaad**


