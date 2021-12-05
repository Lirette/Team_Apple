# Literature Review
### Draft/Quick-and-Dirty version


## Predicting Readability of Texts for Italian L2 Students: A Preliminary Study
### Bolli,Rini & Spina 2017

Two models are considered that measure complexcity:
- Coh-Metrix (cf Graesser et al., 2004): 108 indices os different levels of linguistic analysis. Mainly focus on english
- READ-IT (cf Dell'Orletta et al., 2011): Focuses on lexical and syntactic features (syntatic dependencis or part-of-speech probability). For Italian

However, none of these models are sufficient to *"[...] achieve the goal of developing a computational tool to be used with texts specifically selected in the context of learning and assessing Italian as an L2."* 

#### Process

Complexity of a text is defined by many different factors. The addition of more factors in the analysis also means to increase the computational complexcity of the task. The authors choose 4 categories and tested them:

- **Raw-text features (length features)**: Simple level of computation. They can help to predict text complexicty as higher level texts (c2) are formed by longer sentences and longer words. Sentence length B2: 18.1 words per sentence vs C2: 20.8 words per sentence. Word length B2: 4.8 vs C2: 5 mean word length.

- **Lexical features**: Four metrics are considered:
    - *Lexical diversity* (cf Malvern, Richards, Chipere & Durán, 2004) is the ratio fo total of words to the number of different unique words. Measures the amont of different words used in a text. High score means it includes more different words. Guiraud index was used. Result: B2: 43.2 vs C2: 51.9. 
    - *Lexical density* (cf Ure, 1971) is the ratio of content words (verbs, nouns, adjectives and adverbs) to the total number of words in a text. Dense texts are more difficult to understand. Result: B2: 44.7, C2: 45.8
    - *New Basic Italian Vocabulary* (cf De Mauro & Chiari, forthcoming) is a list of 7'500 most familiar words to native speakers. The authors computed two features: 1) percentage of lemmas on this references list that are used in the texts; 2) internal distribution of the occurring basic italian vocabuluary worlds (in particular the 2000 most frequent or fundamental words). Result complete list: B2: 77.9, C2: 76.4. Result fundamental list: B2: 71.2, C2: 68.8.
    - *Concrete and abstract nouns* is the percentage of concrete and abtract nouns in a text. Result concrete nouns: B2:56.7, C2:48. Result abstract nouns: B2:11.8,C2 48.

- **Morpho-syntatic features** were not significant and did not improve the prediction.

- **Discursive features** measures the features that help a reader understand the different ideas in the text. For example, "I know doctors who have graduated with 110 and honors from whom I would not have even a nail cure. I trust this fake doctor. I wouldn't trade it with any other doctor.". The word doctor is in the three sentences. It helps the reader follow the text and its meaning by connecting the three sentences. This is an example of *referential cohesion*. The other type is *deep cohesion* which measures the connectivees in a text. Result for referential cohesion: overlapping nouns in adjacent senteces are significantly more frequent in B2 (the authors do not give a quantitative measure). Result for deep cohesion: Temporal connectives are significantly more frequent in easier texts (the authors do not give a quantitative measure). 

#### Relevant References
De Mauro, T., & Chiari, I. (forthcoming). Il Nuovo Vocabolario di Base della Lingua Italiana.

Dell’Orletta, F., Montemagni, S., & Venturi, G. (2011). READ–IT: Assessing readability of Italian texts with a view to text simplification. Paper presented at the 2nd Workshop on Speech and Language Processing for Assistive Technologies, Edinburgh.

Graesser, A. C., McNamara, D. S., Louwerse, M. M., & Cai, Z. (2004). Coh-Metrix: Analysis of text on cohesion and language. Behavior Research Methods, Instruments, And Computers, 36, 193–202.

Malvern, D., Richards, B., Chipere, N., & Durán, P. (2004). Lexical diversity and language development. Quantification and assessment. London: Palgrave Macmillan

Ure, J. (1971), Lexical density and register differentiation. In G. Perren & J. L. M. Trim (Eds.), Applications of Linguistics. Selected Papers of the Second World Congress of Applied Linguistics (pp. 443–452). Cambridge: Cambridge University Press.


## Automatic Classification of Text Complexity
### Santucci, Santeralli, Forti & Spina 2020

*"The goal was thus to design a supervised model to predict the CEFR level of any text written using the Italian language."*

In english the most known models are Flesh - Kindcaid [22], Coh-Metrix [21], CTAP [18]. In italian, the main approches are Flesh-Vacca formula [27], GulpEase index [28], and READ-IT [12]. The last one is the most computationally expensive. 

The authors point out that their paper is different from other because it targets CEFR specifically, uses a more extended set of numeric lionguistic features and apply an experimental comparison of different supervised classification models. 

The text is their analysis range from B1 to C2. They have a dataset of texts with the four different classes which is used to train a predictive model. This predicitive model is used to predic the complexcity class of a previpously unseen text. 

#### Process
The first step is to transform the training text into a numeric vector. This allows the authors to use the most common models and algorithms in the ML literature. The numeric vector is then analyzed using the usual methods (tokeenization, part-of-speech tagging and parsing) in a step called "NLP Pipeline". 
The training phase can be decomposed as follows:

Traning Texts + labels (input) -> Features Extractions -> (output) Training Features + Labels
Training Features + Labels (input) -> Machine Learning Algorithm - > (output) Predictive Model

The prediction phase can be decomposed as follows:
Unlabeeled Text (input) - > Features Extraction -> (output) Unlabeled Features
(input) Unlabeled Features -> Predictive Model -> (output) Predicted Label

- **NLP Pipeline**: the authors focus on the most baisc leical, morphological and syntactic elaborations with the following points:
    - *Tokenization* which splits the sentences into a list of tokens (for example words and punctuation marks)
    - *Part-of-Speech(POS) tagging* which marks each token into a POS category (noun, verb, adjective, adverd, etc)
    - *Lemmatization* which produces the lemma of a token. A lemma is the base form of a word. For example the infinite form for a verb, having -> have, had -> have etc. 
    - *Dependency parsing* which produces a denpendency tree for each sentence. This tree is a tree that links the different words and how they interact with each other. The nodes are the tokens and the edges are label regarding the dependency realtions among the words. For example which noun is modified by an adjective or which word is the subject of a verb.
    - *Constituency parsing* which produces a constituency tree with the full sentece and the root and the chunks of the sentences as the inner nodes and the leaf nodes are the single tokens. 

The libraries they use are UPPipe, Spacy and Tint. After an intial testing phase, UPPipe (version 2.5) was used because it results in a better accuary. 

- **Numeric Longuistic Features**: The authors use 6 categories and 139 features:
    - *Raw Text Features*: 
        - *Number of senteces in the text*
        - *Number of token per sentence*
        - *Number of characters per token*
        - *Number of different types in the text* which is the number of different unique token in the entire text
    - *Lexical Features*:
        - *Basic Italian Vocabulary Rate*
        - *Lexical diversity* which is the ratio between the number of unique tokens and the number of token computed within 100 randomly selected tokens. The litature suggests that a randomly selected subset allows for a fairer comparison for texts of different lenghts. 
        - *Lexical variation* which features two things 1) the lexical density (ratio between content words and the total number of words in a text) and 2) distribution of the content words among each one of the 4 POS content categories (verbs, nouns, adjectives and adverbs)
        - *Lexical sophistication* (cf [59]) which is the mean and standard deviation of the COLFIS frequences of the function tokens, function lemmas, lexical token and lexical lemmas observed in the text. 
        - *Nouns abstractness distribution* which is the abstract, semiabstract and concrete categories. 
    - *Morphological Features*: The authors only consided the morphological complexicty index MCI (cf [31]). {PAS SUR DE BIEN COMPRIS ENCORE}
    - *Morpho-Syntatic Features* 
        - *Subordinate ratio* mean and SD of the percentages of subordinate clauses over the total number of clauses
        - *POS tags distribution* 
        - *Verbal moods distribution* which is the percentage of verb tokens belonging to everyone of the 7 verbal moods (indicative, subjunctive, conditional, imperiative, gerung, pariticipative and infinite)
        - *Dependency tags distribution* 
    - *Syntactic Features* 
        - *Depth of the dependency tree*
        - *Length of non-verbal chains* mean and SD of the lengths of the maximal-length path without verbal nodes in all the dependency tree
        - *Verbal roots* the percentage of dependy trees with a verbal root.
        - *Arity of verbal predicates* the distribution of the arity of the verbal nodes in all the dependency trees, where the arity is the number of dependency links involving the verbal node as head. experimentation , the authors decided to maintain a discrete distribution of the arities by registering the percentage of verbal nodes with 1, 2, 3, 4, and ≥5 links.
        - *Length of the dependency links* 
        - *Maximal non-verbal phrase* 
        - *Number of syntatic constituents*
        - *Syntactic complexicity*
        - *Relative suborbinate order*
        - *Length of clauses*
        - *Subordination chains length*
    - *Discursive Features*
        - *Referential cohesion* 
        - *Deep causal cohesion*

#### Classification Models
There are 10 classifications models which are considered. The best models are Random Forest (RF) and Support Vector Machine with radial basis funciton as Kernel (SVM) with 72.5% and 71.7% accuracy respectevily. The worst performaing are the KNN variants and the Bayesian models. For the two best models, the number of selected features are of 58 for RF and 54 for SVM. 
If we consider only the RF, the syntactic features (0.27) are the most important, fallowed by morpho-syntatic tied with lexical (0.23), followed by raw test(0.20), discursive (0.05) and morphological (0.02).

#### Relevant References 
[12] Dell’Orletta, F.; Montemagni, S.; Venturi, G. READ–IT: Assessing Readability of Italian Texts with a View
to Text Simplification. In Proceedings of the Second Workshop on Speech and Language Processing for Assistive Technologies, Edinburgh, Scotland, UK, 30 July 2011; Association for Computational Linguistics: Edinburgh, UK, 2011; pp. 73–83.

[18]  Xia, M.; Kochmar, E.; Briscoe, T. Text Readability Assessment for Second Language Learners. arXiv 2011, arXiv:1906.07580.

[21] Graesser, A.; McNamara, D.; Louwerse, M.; Cai, Z. Coh-Metrix: Analysis of text on cohesion and language. Behav. Res. Methods Instrum. Comput. 2004, 36, 193–202.

[22] François, T.; Fairon, C. An “AI readability” Formula for French as a Foreign Language. In Proceedings of the 2012 Joint Conference on Empirical Methods in Natural Language Processing and Computational Natural Language Learning, Jeju Island, Korea, 12–14 July 2012; pp. 466–477.

[27] Franchina, V.; Vacca, R. Adaptation of Flesh readability index on a bilingual text written by the same author both in Italian and English languages. Linguaggi 1986, 3, 47–49.

[28] Lucisano, P.; Piemontese, M. GULPEASE: Una formula per la predizione della difficoltà dei testi in lingua italiana. Scuola Città 1988, 31, 110–124.

[59] Bertinetto, P.M.; Burani, C.; Laudanna, A.; Marconi, L.; Ratti, D.; Rolando, C.; Thornton, A.M. Corpus e Lessico di Frequenza Dell’italiano Scritto (CoLFIS). Available online: http://linguistica.sns.it/CoLFIS/
Home.htm (accessed on 18 Octoer 2020).
   
## An “AI readability” formula for French as a foreign language
### Francois & Fairon 2012

A new paradigm in readability formulas has emerged recently, which is refered as the "AI readability". The field has been devleoping in many languages but french is still lacking. 
The authors conduct experiments to derived a model that predicts readability level in french. 

#### Model for French
For identifying the readability level of a text in the context of French as a Foreign Language (FFL),ne of the author proposed an new model named the "AI Formula" (François 2009) which is based on logistic regression and ten features. The formula stresses the use of verbal tense information as a way to improve performance. The limitation of this formula is the relatively low number of features (20)

For this work, the features are divided in four categories:

- *Lexical Features*
    - *Statistics of lexical frequencies* are the frequencies of words in a text, usually summarized by the mean, the median, interquartile range and 75th and 90th percentile. The authors used the Lexique3 database (New at al., 2007).
    - *Percentage of words not in a references list* The authors used two lists one that is somewhat dated (Gougenheim et al 1964) and a more recent one named Alter Ego (Berther et al., 2006)
    - *Word lenght*
    - *N-grams models* {PAS SUR D'AVOIR COMPRIS. PLUS D'INFO : https://towardsdatascience.com/introduction-to-language-models-n-gram-e323081503d9}
    - *Lexical Diversity* 
    - *Orthographic neighborhood* 
- *Syntactic features*
    - *Sentence length*
    - *POS Ratios*
    - *Verbs*
- *Semantic features*
    - *Personnalization level* which refers to the informality of the text, computed by the type of personal pronouns found in a text.
    - *Conceptual density* estimation of the mean number of propositions per word 
    - *Lexical cohesion*
- *Features specific to FFL*
    - *Multi-word expressions (MWE)*, where the authors compute their frequency and they use a bigram model
    - *Type of text* which defines if the text is a dialogue.

The authors considered 6 models, multinomial and ordinal logistic regression (MLR and OLR), classification trees, bagging, boosting and SVM. The logistic models and SVM out performed all other, as such only those are reported. 
The best regressors is "Proportion of absent words from a list of easy words" which a spearman correlation of 0.65.
The category with the best prediction power is the lexical family (40.5%) closely followed by the syntatic one(39.3%). 

#### Relevant References
A. Berthet, C. Hugot, V. Kizirian, B. Sampsonis, and M. Waendendries. 2006. Alter Ego 1. Hachette, Paris

T. Franc ̧ois. 2009. Combining a statistical language model with logistic regression to predict the lexical and syntactic difficulty of texts for FFL. In Proceed- ings of the 12th Conference of the EACL : Student Re- search Workshop, pages 19–27.

G. Gougenheim, R. Miche ́a, P. Rivenc, and A. Sauvageot. 1964. L’e ́laboration du franc ̧ais fondamental (1er degre ́). Didier, Paris.

B. New, M. Brysbaert, J. Veronis, and C. Pallier. 2007. The use of film subtitles to estimate word frequencies. Applied Psycholinguistics, 28(04):661–677.
