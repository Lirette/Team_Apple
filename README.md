# DMML2021 Apple
Datamining project

## Team members
Marine Renaudineau
Marco Soto Novoa
Lirette Teiffouet Noumbo Epse Keumedjio

## project description 
the goal of the project is to detect Difficulty Level of French Texts. the different level possible are: A1, A2, B1, B2, C1, C2

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
