## Summary of the relevent regressors
These are the relevant possible regressors we could use. These are all taken from the literature review. When possible,
I tried to quickly how to compute them (it's in parenthesis).
If I was able to implement them in the code, the corresponding function are in *italic*

### RAW TEXT
- Words per sentence
-> *Implemented by count_words()*

- Tokens per sentence
-> *Implemented by count_tokens()*


- Word length (***)
- Characters per token
-> *Implemented by count_avg_word_character/count_avg_token_character*


### LEXICAL FEATURES
- Unique token per sentence (unique token/total token in sentence) 

- Unique token per text (unique tokens/total token in text) 
-> *This is implemented by tfidf_vector*

- Lexical diversity: Ratio total words to number of different unique words (unique words/total words)
-> *Implemented by lex_div_words()*

- Lexical diversity fair: Ratio between number of unique token and number of token computed within 100 random token (unique token/100 random token)

- Lexical density: Ratio content words to total words (content words/total words)
-> *Implemented by lex_den_words()/lex_den_tokens()*

- NBIV: 1)% lemmas in reference list that are in text (lemma on list/total lemmas) , 2) %lemmas in fundamental list (lemma on shorter list/total lemmas)
- Lexical variation: 1) lexical density, 2) distribution of content words among each one of the 4 pos content categories (% of tags over the 4 content tags)
- Lexical sophistication: statistics of lexical frequency
- Orthographic neighbourhood: pas sûr
- Concretness: pas sûr


### SYNTATIC FEATURES
- Token/Words per sentence (***)
-> Implemented by count_otken()/count_words()


- Verbs
- POS distribution (% of each tag over all the existing tags)

*** 3rd reference put them in one category, while two others put them in Raw Text Features
