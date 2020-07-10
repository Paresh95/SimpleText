# SimpleText
---

A package to manage textual data in a simple fashion.

Install with:

```
pip install SimpleText
```

  

SimpleText makes preprocessing simple with the ```preprocess``` function. This function takes a string as an input and outputs a list of tokens. There are several parameters in the function to help quickly pre-process a string. 

**Parameters:**

```text``` (string): a string of text

```n_grams``` (tuple, default = (1,1)): specifies the number of ngrams e.g. (1,2) would be unigrams and bigram, (2,2) would be just bigrams 

```remove_accents``` (boolean, default = False): removes accents 

```lower``` (boolean, default = False): lowercases text 

```remove_less_than``` (int, default = 0): removes words less than X letters 

```remove_more_than``` (int, default = 20): removes words more than X letters

```remove_punct``` (boolean, default = False): removes punctuation

```remove_alpha``` (boolean, default = False): removes non-alphabetic tokens

```remove_stopwords``` (boolean, default = False): removes stopwords

```remove_custom_stopwords``` (list, default = [ ]): removes custom stopwords

```lemma``` (boolean, default = False): lemmantises tokens (via the Word Net Lemmantizer algorithm)

```stem``` (boolean, default = False): stems tokens (via the Porter Stemming algorithm)


In the example below we preprocess the string by:

  - lowercasing letters
  - removing punctuation
  - removing stop words
  - removing words with more than 15 letters and less than 1 letter


```
from SimpleText.preprocessor import preprocess

text = 'Last week, I went to the shops.'

preprocess(text, n_grams=(1, 1), remove_accents=False, lower=True, remove_less_than=1,
           remove_more_than=15, remove_punct=True, remove_alpha=False, remove_stopwords=True,
           remove_custom_stopwords=[], lemma=False, stem=False, remove_url=False)
```

The output would be:

```
['last', 'went', 'shops', 'week']
```

In this second example we process the string by:

- generating unigrams and bigrams
- stemming
- removing the url
- removing accents 
- lowercasing letters

```
from SimpleText.preprocessor import preprocess

text = "I'm loving the weather this year in españa! https://en.tutiempo.net/spain.html"

preprocess(text, n_grams=(1, 2), remove_accents=True, lower=True, remove_less_than=0, 
           remove_more_than=20, remove_punct=False, remove_alpha=False, remove_stopwords=False,remove_custom_stopwords=[], lemma=False, stem=True, remove_url=True)

```

This outputs:

```
["i'm",'love','the','weather','thi','year','in','espana!',("i'm", 'loving'),('loving', 'the'),('the', weather',
 ('weather', 'this'),('this', 'year'),('year', 'in'),('in', 'espana!')]
```