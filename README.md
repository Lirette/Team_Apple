# Data Mining and Machine Learning 2021 - Team Apple 

### HEC Lausanne - Prof. Michalis Vlachos, Diana Korka, Ahmad Ajalloeian

![](documents/1.png)

---
# Project: Detecting the difficulty level of French texts

The goal of the project is to detect Difficulty Level of French Texts. the different level possible are: A1, A2, B1, B2, C1, C2.

## Strucuture of the Github 

## Table of Contents 
0. Team Presentation
1. Introduction 
2. Methodology
3. Results
4. Video
---
# 0. Team: Diverse yet united
The team is composed of three people, which all are of different masters' program and different backgrounds. 

### **Marine Renaudineau**

*Github username*: Mrenaudi

*Kaggle username*: Maarine rrr

*E-mail*: marine.renaudineau@unil.ch

Marine is in the [Legal Issues, Crime and Security of Information Technologies](https://www.unil.ch/formations/en/home/menuinst/masters/droit-criminalite-et-securit.html) Master program. Even though she has no prior experience in data mining, she decided to take on the challenge face on. She's also attending another Data Science course. She is wanting to understand data analysis as a whole and be able have a broad view of the subject, from the programming problems to the policy problems this field brings. 

### **Marco Soto Novoa**

*Github username*: msn08

*Kaggle username*: marcoantoniounil

*E-mail*: marco.sotonovoa@unil.ch 

Marco Antonio is in the [Economics](https://www.unil.ch/hec/en/home/menuinst/etudes/master/economie-politique.html) Master programs. He is speciallizing in Quantitative Economics, which is the study mathematical and computational tools in the context of economics and economic policy. While he has some experience with programming, he is eager to learn more and this class was the perfect opportunity for him to learn about machine learning and how it could impact his future study of economics. 


### **Lirette Teiffouet Noumbo Epse Keumedjio**

*Github username*: Lirette2

*Kaggle username*: Lirette_Teiffouet

*E-mail*: Lirette.TeiffouetNoumboEpseKeumedjio@unil.ch 

Lirette is in the [Information Systems](https://www.unil.ch/formations/en/home/menuinst/masters/systemes-dinformation.html) Master program . She decided to to take the Data Mining and Machine Learning class because she has strong interests in the field and she wants to work in the data mining field. This class and project is the perfect opportunity for her to learn and master the skills the needs. 

---
# 1. Introduction

Natural Language Processing (NLP) and Text Analytics has become a big research field in the past years. This is of course a natural devleopment of our society, which has created tools for communication that through the internet can reach million if not billions. All the data generated needs treatment. It also needs analysis, as some of it can be dangerous. 

One area of text analytics and NLP that has being gaining traction in the machine learning research community is the topic of claffiying a text automatically according to its complexicity. There are many ways to achieve this goal. 
In this project, we implement various models to try and classify french texts according to it difficulty following the Common European Framework of Reference for Languages (CEFR) difficulties. 

The github repo is structured as follows:


```Code```
The folder that contains various notebooks where we explore different technics and strategies to achieve the best classification. The final notebook is named ```final_notebook_dmml2021_apple```

```Documents```
This folder most important contribution is the Literature Review which explores briefly what has been done in the past. Then, it includes a file which documents how we have implemented what we have learned from the literature. Finally, this folder also contains some files needed such images.

```Data```
This folder contains the orginal training dataset as well as the unlabled dataset. We have also included a dictionary of french words that was made by a researcher. This has helped implement a regressor and enrich our models. 

---

## table comparing differents methods used
| Classifier      | Accuracy | Precision     | Recall | F1_Score |
| :---        |    :----:   |    ---: |    :----:   |    ---: |
| Logistic Regression      | 0.4604      | 0.4577   |  0.4595  | 0.4554      | 
| KNN   | 0.3438      | 0.3712      |   0.3422    |  0.3260    |
| Decision Tree   |    0.3115      | 0.3100      |   0.3107    |  0.3094  |
| Random Forest   |   0.4021  | 0.4061      |   0.400  |   0.3905  |
| RidgeClassifier      | 0.3156      | 0.3823   |   0.3137  |  0.2913   |
| autres...   |        |      |       |       |

## Logs

### Patch 2.4
**MODEL**: LR
**ACCURACY SCORE**:0.4823
**SUBMISSION SCORE**: 0.3900

**MODEL**: RF
**ACCURACY SCORE**:0.4688
**SUBMISSION SCORE**: 0.3600

**MODEL**: LSCV
**ACCURACY SCORE**:0.4865
**SUBMISSION SCORE**: 0.4233

**CHANGES**
Function that counts words NOT in the list, counted the words ACTUALLY in the list. Changed it to be correct
Optimized some functions to run faster
Tested with token only, with words only, with everything and added the scores each time
Added LinearSCV model
Added submission 
Code needs heavy cleaning

**Notes**
I think we suffer overfitting. The most promessing model is LSCV for now. By adding all the regressors and things seen in class we should get at least up to the UNIL_TEST score. 

### Patch 2
**MODEL**: LR
**ACCURACY SCORE**:
0.4802

**MODEL**: RF
**ACCURACY SCORE**:
0.4708

**CHANGES**:
Added a list of the 1500 most frequents French words. The source is the following the government (https://eduscol.education.fr/186/liste-de-frequence-lexicale)
Added regressors. The ones that have been added can be seen in the document “Regressors_Summary”
Transformed regressors to be in same scale with MinMaxScaler
Added Column Transformer to allow tfidf to be applied only to correct column(sentence)
Quickly added RF model, as per the literature review, it is the most accurate

**NOTES**:
For clarity, I decided to have one function per regressors. This is extremely inefficient as the the token split happens many times and is time consuming.
It should be done in one function that then extract the features and puts them nicely.
The function that check the words in the frequency list takes also some time and should be re written.

Each time I computed the regressors for raw words as well as tokens. We should investigate if this is truly needed(I don't think so) and if using only one is more beneficial.
I think that specially the RF model is underperforming due to this. While using less regressors I achieved an accuary score of 0.48(similar to LR with all the regressors)

### Patch 1.1
**MODEL**: LR
**ACCURACY SCORE**:
0.4062

**CHANGES**:
Changed *en_core_web_sm* to *fr_core_news_sm.* (required download using *!python -m spacy download fr_core_news_sm*)

### Patch 1
**MODEL**: LR
**ACCURACY SCORE**:
0.4208

**CHANGES**:
Add graph of sentences per difficulty
Add *average=None* and *average=“macro”* to def accuracy
