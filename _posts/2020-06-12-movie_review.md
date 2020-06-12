---
title: "Introduction to sklearn NLTK, Logistic Regression classification on Movie Reviews to predict ratings"
date: 2020-05-31
categories: [Python]
tags: [Text Mining]
header:
  image: "/images/movie_review/header.jpg"
excerpt: "The objective of this post was to successfully work with NLTK library to Preprocessor, Extract Features from Text reviews and use it on Logistic Regression with cross validation to predict the ratings"
mathjax: "true"
---


 <h2 align="center">Logistic Regression: A Sentiment Analysis Case Study</h2>



### Introduction
___

**About DataSet:**
- IMDB movie reviews dataset
- http://ai.stanford.edu/~amaas/data/sentiment
- Contains 25000 positive and 25000 negative reviews
<img src="https://i.imgur.com/lQNnqgi.png" align="center">
- Contains at most reviews per movie
- At least 7 stars out of 10 $\rightarrow$ positive (label = 1)
- At most 4 stars out of 10 $\rightarrow$ negative (label = 0)
- 50/50 train/test split



<b>Features: bag of 1-grams with TF-IDF values</b>:
- Extremely sparse feature matrix - close to 97% are zeros

 <b>Model: Logistic regression</b>
- $p(y = 1|x) = \sigma(w^{T}x)$
- Linear classification model
- Can handle sparse data
- Fast to train
- Weights can be interpreted
<img src="https://i.imgur.com/VieM41f.png" align="center" width=500 height=500>

### Task 1: Loading the dataset
---


```python
import pandas as pd
```


```python
df = pd.read_csv(r'C:\Users\shrey\OneDrive\Desktop\dataset_posts\movie_data.csv')
```


```python
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>review</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>In 1974, the teenager Martha Moxley (Maggie Gr...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>OK... so... I really like Kris Kristofferson a...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>***SPOILER*** Do not read this, if you think a...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>hi for all the people who have seen this wonde...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>I recently bought the DVD, forgetting just how...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Leave it to Braik to put on a good show. Final...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Nathan Detroit (Frank Sinatra) is the manager ...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>To understand "Crash Course" in the right cont...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>I've been impressed with Chavez's stance again...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>This movie is directed by Renny Harlin the fin...</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['review'][0]
```




    'In 1974, the teenager Martha Moxley (Maggie Grace) moves to the high-class area of Belle Haven, Greenwich, Connecticut. On the Mischief Night, eve of Halloween, she was murdered in the backyard of her house and her murder remained unsolved. Twenty-two years later, the writer Mark Fuhrman (Christopher Meloni), who is a former LA detective that has fallen in disgrace for perjury in O.J. Simpson trial and moved to Idaho, decides to investigate the case with his partner Stephen Weeks (Andrew Mitchell) with the purpose of writing a book. The locals squirm and do not welcome them, but with the support of the retired detective Steve Carroll (Robert Forster) that was in charge of the investigation in the 70\'s, they discover the criminal and a net of power and money to cover the murder.<br /><br />"Murder in Greenwich" is a good TV movie, with the true story of a murder of a fifteen years old girl that was committed by a wealthy teenager whose mother was a Kennedy. The powerful and rich family used their influence to cover the murder for more than twenty years. However, a snoopy detective and convicted perjurer in disgrace was able to disclose how the hideous crime was committed. The screenplay shows the investigation of Mark and the last days of Martha in parallel, but there is a lack of the emotion in the dramatization. My vote is seven.<br /><br />Title (Brazil): Not Available'



## <h2 align="center">Bag of words / Bag of N-grams model</h2>

### Task 2: Transforming documents into feature vectors

Below, we will call the fit_transform method on CountVectorizer. This will construct the vocabulary of the bag-of-words model and transform the following three sentences into sparse feature vectors:
1. The sun is shining
2. The weather is sweet
3. The sun is shining, the weather is sweet, and one and one is two

**Lets understand the concept over a small paragraph before we apply it to all the reviews..**


```python
import numpy as np
docs = np.array(['The sun is shining',
'The weather is sweet',
'The sun is shining, the weather is sweet, and one and one is two'])
```


```python
from sklearn.feature_extraction.text import CountVectorizer
```


```python
count = CountVectorizer()
bag = count.fit_transform(docs)
```


```python
print(count.vocabulary_)
```

    {'the': 6, 'sun': 4, 'is': 1, 'shining': 3, 'weather': 8, 'sweet': 5, 'and': 0, 'one': 2, 'two': 7}



```python
print(bag.toarray())
```

    [[0 1 0 1 1 0 1 0 0]
     [0 1 0 0 0 1 1 0 1]
     [2 3 2 1 1 1 2 1 1]]


Raw term frequencies: *tf (t,d)*—the number of times a term t occurs in a document *d*

### Task 3: Word relevancy using term frequency-inverse document frequency

$$\text{tf-idf}(t,d)=\text{tf (t,d)}\times \text{idf}(t,d)$$

$$\text{idf}(t,d) = \text{log}\frac{n_d}{1+\text{df}(d, t)},$$

where $n_d$ is the total number of documents, and df(d, t) is the number of documents d that contain the term t.


```python
from sklearn.feature_extraction.text import TfidfTransformer
np.set_printoptions(precision= 2)
```


```python
tfidf = TfidfTransformer(use_idf= True, norm='l2', smooth_idf = True)
print(tfidf.fit_transform(bag).toarray())
```

    [[0.   0.43 0.   0.56 0.56 0.   0.43 0.   0.  ]
     [0.   0.43 0.   0.   0.   0.56 0.43 0.   0.56]
     [0.5  0.45 0.5  0.19 0.19 0.19 0.3  0.25 0.19]]


The equations for the idf and tf-idf that are implemented in scikit-learn are:

$$\text{idf} (t,d) = log\frac{1 + n_d}{1 + \text{df}(d, t)}$$
The tf-idf equation that is implemented in scikit-learn is as follows:

$$\text{tf-idf}(t,d) = \text{tf}(t,d) \times (\text{idf}(t,d)+1)$$

### Task 4: Data Preparation
These reviews have a lot going on in them which needs to be taken care of before proceeding any further.
- Emoticons like :)
- Characters like <[^>]*>
- As well same words written differently like cat and CAT


```python
df.loc[0,'review'][-50:]
```




    'is seven.<br /><br />Title (Brazil): Not Available'




```python
import re
def preprocessor(text):
    text = re.sub('<[^>]*>', '', text)
    emoticons = re.findall('(?::|;|=)(?:-)?(?:\)|\(|D|P)', text)
    text = re.sub('[\W]+', ' ', text.lower()) +\
        ' '.join(emoticons).replace('-', '')
    return text
```


```python
preprocessor(df.loc[0,'review'][-50:])
```




    'is seven title brazil not available'




```python
df['review'] = df['review'].apply(preprocessor)
```


```python
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>review</th>
      <th>sentiment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>in 1974 the teenager martha moxley maggie grac...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ok so i really like kris kristofferson and his...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>spoiler do not read this if you think about w...</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>hi for all the people who have seen this wonde...</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>i recently bought the dvd forgetting just how ...</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>







### Task 5: Tokenization of documents


```python
from nltk.stem.porter import PorterStemmer
```


```python
porter = PorterStemmer()
```


```python
def tokenizer(text):
    return text.split()
```


```python
def tokenizer_porter(text):
    return [porter.stem(word) for word in text.split()]
```

**Here is how words within each sentence is stemmed..**
### Stemming vs Lemmatization
stemming — need not be a dictionary word, removes prefix and affix based on few rules
lemmatization — will be a dictionary word. reduces to a root synonym.

For example:

|Word|Lemmatization|Stemming|
|--|--|--|
|was|be|wa|
|studies|study|studi|


```python
tokenizer('runners like running and they run')
```




    ['runners', 'like', 'running', 'and', 'they', 'run']




```python
tokenizer_porter('runners like running and they run')
```




    ['runner', 'like', 'run', 'and', 'they', 'run']



### Stop Words
**The most common words such as “is, are” will have very high values, giving those words a very high importance. But using these words to compute the relevance produces bad results. These kind of common words are called `stop-words.`**

We will use nltk library to remove these stop words.


```python
import nltk
nltk.download('stopwords')
```

    [nltk_data] Downloading package stopwords to
    [nltk_data]     C:\Users\shrey\AppData\Roaming\nltk_data...
    [nltk_data]   Package stopwords is already up-to-date!





    True




```python
from nltk.corpus import stopwords
```


```python
stop = stopwords.words('english')
[w for w in tokenizer_porter('a running like running and runs a lot')[-10:] if w not in stop]
```




    ['run', 'like', 'run', 'run', 'lot']







### Task 6: Transform Text Data into TF-IDF Vectors
**Term Frequency (TF) * Inverse Document Frequency (IDF)**

**Term Frequency:** This measures the frequency of a word in a document.

**Document Frequency:** TF is frequency counter for a term t in document d, where as DF is the count of occurrences of term t in the document set N. In other words, DF is the number of documents in which the word is present.

**Inverse Document Frequency:** IDF is the inverse of the document frequency which measures the informativeness of term t.





```python
from sklearn.feature_extraction.text import TfidfVectorizer
tfidf = TfidfVectorizer(strip_accents= None,
                       lowercase= False,
                       preprocessor= None,
                       tokenizer= tokenizer_porter,
                       use_idf=True,
                       norm='l2',
                       smooth_idf=True)
y = df.sentiment.values
X = tfidf.fit_transform(df.review)
```

### Task 7: Document Classification using Logistic Regression
I am using logistic regression and RandomForest for classification here, you can use any other classification to practice.


```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test =  train_test_split(X,y, random_state = 1, test_size= 0.5,
                                                    shuffle =False)
```


```python
import pickle
from sklearn.linear_model import LogisticRegressionCV
clf = LogisticRegressionCV(cv=5,
                          scoring ='accuracy',
                          random_state = 0,
                          n_jobs = -1,
                          verbose =3,
                          max_iter= 300).fit(X_train,y_train)
saved_model = open('save_model.sav','wb')
pickle.dump(clf,saved_model)
saved_model.close()
```

    [Parallel(n_jobs=-1)]: Using backend LokyBackend with 8 concurrent workers.
    [Parallel(n_jobs=-1)]: Done   2 out of   5 | elapsed:  1.1min remaining:  1.7min
    [Parallel(n_jobs=-1)]: Done   5 out of   5 | elapsed:  1.2min finished



```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100, criterion= 'entropy', random_state= 1)
model.fit(X_train,y_train)
```




    RandomForestClassifier(bootstrap=True, ccp_alpha=0.0, class_weight=None,
                           criterion='entropy', max_depth=None, max_features='auto',
                           max_leaf_nodes=None, max_samples=None,
                           min_impurity_decrease=0.0, min_impurity_split=None,
                           min_samples_leaf=1, min_samples_split=2,
                           min_weight_fraction_leaf=0.0, n_estimators=100,
                           n_jobs=None, oob_score=False, random_state=1, verbose=0,
                           warm_start=False)



### Task 8: Model Evaluation
It is important to know if your model performs the same way on Data it has not seen in training.
We will practice some basic `Evaluation methods` to compare the performance of our model.


```python
#save your model
filename ='save_model.sav'
saved_clf = pickle.load(open(filename,'rb'))
```


```python
print("Accuracy for the Logistic Regression is :",saved_clf.score(X_test,y_test))
```

    Accuracy for the Logistic Regression is : 0.89608



```python
from sklearn.metrics import classification_report
```


```python
y_pred = saved_clf.predict(X_test)
```


```python
print(classification_report(y_test,y_pred))
```

                  precision    recall  f1-score   support

               0       0.90      0.89      0.90     12527
               1       0.89      0.90      0.90     12473

        accuracy                           0.90     25000
       macro avg       0.90      0.90      0.90     25000
    weighted avg       0.90      0.90      0.90     25000




```python
print("Accuracy for the Random Forest is :", model.score(X_test,y_test))
```

    Accuracy for the Random Forest is : 0.84244



```python
print(classification_report(y_test,model.predict(X_test)))
```

                  precision    recall  f1-score   support

               0       0.84      0.84      0.84     12527
               1       0.84      0.84      0.84     12473

        accuracy                           0.84     25000
       macro avg       0.84      0.84      0.84     25000
    weighted avg       0.84      0.84      0.84     25000



**LogisticRegression seems to be doing a better job for this problem statement.**

I hope you learned some concepts of Text analysis from this simple tutorial
