# BreastCancerPredict_ML
Purpose:
Aim of this project is to correctly predict whether a sample is normal or cancerous by utilizing genes that might have strong association with either normal or cancerous cells as predictors as well as the age of the patient.

Data Acquisition: 
I got my data set from GEO which is short for “Gene Expression Omnibus” database. It is a public genomics data repository that archives and freely distributes microarray, next-generation sequencing and other high-throughput functional genomics data submitted by the research community. And you can have access to series records that link together a group of related samples with an accession number which for my data set, the accession number was GSE70947.

To get the actual data set into Rstudio, I didn’t download the data file directly from GEO or use any URL since it’s such a large file, but I instead used a package called GEOquery from Bioconductor and directly queried the data in RStudio with the accession number. I also fetched and pieced together the sample names, the gene expression data, and mapped gene IDs with gene names by myself to create the data frame that I used in this project. Where I extracted information from Bioconductor data structures such as the “ExpressionSet” class, which is an S4 object that consist many layers and information in it. Information that are stored in the ExpressionSet includes the gene expression data from the microarray experiment, meta-data describing samples in the experiment, annotations about features on the chip and protocols used for processing each sample.

Machine Learning Models: 
I created a Neural Network, a Support Vector Machine and a Random forest model for each data set –meaning three models for the FCBF data set where I have my 25 original features plus the class variable, and three models for the PC data set with all 25 PCs and the class variable.  So, I have a total of 6 models.

The reasons why I picked SVM is because it is good at handling numeric input data, binary classification and it is very much used in classification of microarray gene expression data and ANN because like SVM it can be applied to any learning task and works with numeric input data as well. It also gained a lot of popularity in recent years within the field of computational biology and bioinformatics, so I am interested in examining how it performs relative to other classifiers. Lastly, I picked Random Forest because it can also be applied to any learning task such as binary classification, it is very flexible and powerful and can work well with numeric input data as well.  

Train/Test Split:
I split my data set into train and test sets with 70% of the data in train and 30 in test and made sure that the class distribution between my train and test sets were even.

Model Evaluation:
I trained all my models with 10-fold cross validation and to evaluate model performance on test sets, I generated confusion matrix and examined the accuracy, sensitivity, specificity, F1 score and kappa coefficients of all models. I also calculated accuracy, precision and recall at the end of each of  the three models that I’ve created for each data set to summarize performance. In addition, I also created ROC curves and AUC for the set of three models that performed best –which are the FCBF models. Though, I have say the PC models were very impressive as well since they were able to achieve similar accuracies around 86- 91% with just 2 PCs.

In terms of how well the models worked:
FCBF-ANN: Accuracy: 93%  Sensitivity: 91% Specificity: 95 F1-Score: 0.93 Kappa: 0.86
FCBF-SVM: Accuracy: 93% Sensitivity: 93% Specificity: 93% F1-Score: 0.93 Kapp: 0.86
FCBF-Random forest: 91% Sensitivity: 91% Specificity: 91% F1-Score: 0.91 Kappa : 0.82

PC-ANN: Accuracy: 90%  Sensitivity: 86% Specificity: 93 F1-Score: 0.89 Kappa: 0.80
PC-SVM: Accuracy: 91% Sensitivity: 91% Specificity: 91% F1-Score: 0.91  Kapp: 0.82
PC-Random forest: 86% Sensitivity: 91% Specificity: 82% F1-Score: 0.87 Kappa : 0.73
