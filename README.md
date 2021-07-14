# Classification-on-Diabetes-1999-2008-Dataset

Diabetes 1999-2008 Dataset
Dataset Description
The dataset represents 10 years (1999-2008) of clinical care at 130 US hospitals and integrated delivery networks. It includes over 50 features representing patient and hospital outcomes. Information was extracted from the database for encounters that satisfied the following criteria.
(1) It is an inpatient encounter (a hospital admission).
(2) It is a diabetic encounter, that is, one during which any kind of diabetes was entered to the system as a diagnosis.
(3) The length of stay was at least 1 day and at most 14 days.
(4) Laboratory tests were performed during the encounter.
(5) Medications were administered during the encounter.
The data contains such attributes as patient number, race, gender, age, admission type, time in hospital, medical specialty of admitting physician, number of lab test performed, HbA1c test result, diagnosis, number of medications, diabetic medications, number of outpatients, inpatient, and emergency visits in the year before the hospitalization, etc." The target class is called readmitted which refers to the number of readmissions for the patients whither it is more than 30 days or less than30 days value [1]. In this database, you have 3 different outputs: No readmission; A readmission in less than 30 days (this situation is not good, because maybe your treatment was not appropriate); A readmission in more than 30 days (this one is not so good as well the last one, however, the reason can be the state of the patient. The attributes of the data are described in the table below.
Table. 1 Dataset attribute description and missing value rate [1]
Exploratory Data Analysis
After reading the dataset into a dataframe, EDA were performed on the dataset. Firstly, discovered the shape of the data and the types of the attributes in the dataset; after seeing the types it turned out that there is a lot of categorical data and data that should be numerical but is stored in a non-numerical way. Then the balance of the dataset was reviewed, and it turns out that the dataset is heavily imbalanced with the not readmitted patients covering most of the data. then, the missing values were reviewed using the missing value matrix and bar plot below.
By looking at the plots we see that the missing values are in the columns: weight, medical_speciality, payer_code, race, and diag_1,2,3 while the rest of the attributes have no missing values. The correlation between the attributes to see which are the impacting the class attribute the most were reviewed using the heatmap below.
After looking at the coorelation map, we notice that the coorelations between the feature and the target class are low. Then, there were some plots that gives insights about the dataset and about which people are most readmitted and not readmitted. Discovering the impact of each of 'gender', 'age', 'race' on the target class was done using visualizing the attributes using barplots.
And by Looking at the figures above we see that females that are between 80-90 years old and their race is Caucasian are the most readmitted among all the types of people. Also, Visualizing the impact of insulin intake on the target class was important to get more understanding of the dataset.
The figure above indicates that the people who does not take insulin are the most readmitted. Then, the age rate is a key aspect in defining the patients that were readmitted and it was visualized using barplots.
The figure indicates that the people who does not take insulin and their age is between 70-80 are the most readmitted, and people with age between 70-80 are the most readmitted in all types of insulin intake. Finally, a function called missing values was made in order to give a detailed insight about the missing values and its percentage and unique values in the dataset.
Data Wrangling & Preprocessing
Cleaning:
By looking at the EDA done on the dataset, there found that the dataset contains a lot of missing values, and wrong inputs. So, the first thing was done is converting the target class into numerical by making the value <30 days equals 0 and values >30 equal 1. Then, some of the columns were useless and not impactful so dropping them was essential. In order to refine the non-numerical data, there were 2 lists made: one for the categorical column and one for the numerical columns. Some of the NULL variables were input as a string not a NULL, so they had to be changed into the NULL variable in order to be able to deal with them as missing value. The diagnosis columns 'diag_1', 'diag_2', 'diag_3' were so messy, so it had to be cleaned up using the helper functions called transformFunc and transformCategory that creates the right categorization for the values inside the diagnosis columns; and after cleaning these columns, a barplot was made to see the new right categories for the diagnosis to gain more knowledge about the dataset.
Looking at the bar plots, it is obvious that the people diagnosed with Circulatory are the most readmitted. All the drugs columns were input as a non-numerical value so it had to be changed to numerical value which is by replacing the values 'No', 'Steady', 'Up', 'Down' to 0, 1, 1, 1. Also all the column that has bigger than (>) or smaller than (<) signs were cleaned to have numerical data that can be preprocessed and trained on. The columns 'change', 'diabetesMed', 'gender' were also due to encoding because they held non-numerical data and these columns are important so they had to be encoded.
Dealing with Outliers
As mentioned above, the dataset contained outliers so they had to be removed, DBSCAN clustering technique were used in order to find and deal with the outliers in the most efficient way possible. The result yield to removing 0.03% of the dataset as they were considered outliers.
Resampling Techniques
As noticed in the EDA phase the dataset was heavily imbalanced, so two resampling techniques were used: undersampling and downsampling in order to balance the dataset as much as possible. The undersampling technique was implemented using the near miss method and results that the
dataset was not entirely balanced but the amount of the data lost was not as much as the downsampling; as the downsampling removed huge number of data in the dataset but the it was perfectly balanced.
Finally, after resampling the dataset, a standard scaler was applied to the new datasets and they were split into train and validation sub-datasets.
Applied Machine Learning Models
In this section, different machine learning models were implemented to see which is the best model. Below are the models implemented: Logistic Regression, Support Vector Machin, Random Forest, Ensemble Model 1: (SVM, Logistic Regression), Ensemble Model 2: (SVM, Random Forest), Ensemble Model 3: (SVM, Logistic Regression, Logistic Regression). There was a helper function that was created to help generating the model evaluation report called print_report which prints the metrics used to evaluate the models which are: AUC, acc, recall, precision, f-score.
Logistic Regression
The logistic regression was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Logistic Regression Undersample Validation: AUC: 0.779 Accuracy: 0.780 Recall: 0.776 Precision: 0.553 F-Score: 0.645
Logistic Regression Downsample Validation: AUC: 0.617 Accuracy: 0.616 Recall: 0.627 Precision: 0.551 F-Score: 0.587
Comparing the two models the model trained on the undersampled dataset achieved better performance.
Support Vector Machine
The Support Vector Machine was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Support Vector Machine Undersample Validation:
AUC: 0.805 Accuracy: 0.789 Recall: 0.834 Precision: 0.520 F-Score: 0.641
Support Vector Machine Downsample Validation: AUC: 0.625 Accuracy: 0.624 Recall: 0.636 Precision: 0.563 F-Score: 0.597
Comparing the two models the model trained on the undersampled dataset achieved better performance.
Random Forest
The random forest was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Random Forest Undersample Validation: AUC: 0.819 Accuracy: 0.711 Recall: 0.947 Precision: 0.214 F-Score: 0.349
Random Forest Downsample Validation: AUC: 0.614 Accuracy: 0.613 Recall: 0.603 Precision: 0.639 F-Score: 0.621
Comparing the two models the model trained on the undersampled dataset achieved better performance.
Ensemble Model 1
The Ensemble Model 1 was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Ensmble Model1 Undersample Validation: AUC: 0.798 Accuracy: 0.794 Recall: 0.807 Precision: 0.565 F-Score: 0.664
Ensmble Model1 Undersample Validation: AUC: 0.626 Accuracy: 0.625 Recall: 0.632 Precision: 0.583 F-Score: 0.606
Comparing the two models the model trained on the undersampled dataset achieved better performance.
Ensemble Model 2
The Ensemble Model 2 was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Ensmble Model2 Undersample Validation: AUC: 0.812 Accuracy: 0.790 Recall: 0.850 Precision: 0.508 F-Score: 0.636
Ensmble Model2 Undersample Validation: AUC: 0.625 Accuracy: 0.625 Recall: 0.631
Precision: 0.583 F-Score: 0.606
Comparing the two models the model trained on the undersampled dataset achieved better performance.
Ensemble Model 3
The Ensemble Model 3 was applied on both the under sampled dataset and the down sampled dataset. And after using the evaluation function these were the results: Ensmble Model3 Undersample Validation: AUC: 0.808 Accuracy: 0.791 Recall: 0.838 Precision: 0.524 F-Score: 0.645
Ensmble Model3 Undersample Validation: AUC: 0.626 Accuracy: 0.625 Recall: 0.631 Precision: 0.584 F-Score: 0.607
Comparing the two models the model trained on the undersampled dataset achieved better performance.
So, after comparing all the models using both datasets, it is obvious that the under-sampling technique performs much better on this dataset than the down sampling technique.
ROC Curves
In this section we plot the ROC Curves to give us better intuition about the models and to have more insights about the behaviour and the performance of the models; also, we compared all the models to each other in the form of the ROC curves and these were the results:
Conclusion
Through this project, we created a binary classifier to predict the probability that a patient with diabetes would be readmitted to the hospital within 30 days. We compared between the datasets created with different resampling techniques (upsampling and downsampling) using 6 different
models which are: logistic regresstion, support vector machine, random forest, Ensmble Model 1: (SVM, Logistic Regression), Ensmble Model 2: (SVM, Random Forest), Ensmble Model 3: (SVM, Logistic Regression, Logistic Regression). The results based on the confusion matrices and different evaulation metrics showed that the dataset created using upsampling technique produced more accurate model implementation than the dataset created using downsampling technique. The overall best model which scored the highest AUC = 0.819 was the Random forest implemented on the upsampled dataset.
References:
[1]B. Strack et al., “Impact of HbA1c measurement on hospital readmission rates: analysis of 70,000 clinical database patient records,” Biomed Res. Int., vol. 2014, p. 781670, 2014.
