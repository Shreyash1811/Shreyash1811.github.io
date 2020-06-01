---
title: "Text Mining on News articles, and category prediction"
date: 2020-05-31
categories: [Python]
tags: [Text Mining]
header:
  image: "/images/text_mining_news/header.png"
excerpt: "Text mining on news articles with 20 categories, predicted the category from the attributes extracted from the processed text."
mathjax: "true"
---
<a id = "top"></a>
<p style="font-family: Georgia, serif;
font-size: 30px;
letter-spacing: -1.2px;
word-spacing: 1.6px;
color: #000000;
font-weight: normal;
font-style: normal;
text-align: center;
font-variant: small-caps;
text-transform: none;"> Text Classification:  </p>

## Predicting the Category of an article using Text Classification algorithms.

## Problem Statement:
### Real world is not always about structured data, a lot of the available data in not structured and in the form of text blocks, it can be difficult to analyse these form of datasets.
### In this notebook I have tried to work on data set of BBC news articles.

##  Dataset:
Name:              **20 Newsgroups**

Size:              **18828**

Number of classes: **20**
URL: [http://qwone.com/~jason/20Newsgroups/](http://qwone.com/~jason/20Newsgroups/)

The 20 Newsgroups data set is a collection of approximately 20,000 newsgroup documents, partitioned (nearly) evenly across 20 different newsgroups. To the best of my knowledge, it was originally collected by Ken Lang, probably for his Newsweeder: Learning to filter netnews paper, though he does not explicitly mention this collection. The 20 newsgroups collection has become a popular data set for experiments in text applications of machine learning techniques, such as text classification and text clustering.


```python
import pandas as pd
import numpy as np

import json

import spacy
from spacy import displacy
from collections import Counter
#import en_core_web_lg
nlp= spacy.load('en_core_web_sm')
#nlp = en_core_web_lg.load()
import re
import string

from sklearn.base import TransformerMixin, BaseEstimator
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.calibration import CalibratedClassifierCV
from imblearn.under_sampling import InstanceHardnessThreshold
from sklearn.svm import LinearSVC
from sklearn.preprocessing import MinMaxScaler
from sklearn.feature_selection import SelectFromModel
from sklearn.linear_model import LogisticRegression, SGDClassifier
from sklearn.ensemble import VotingClassifier
from sklearn.naive_bayes import MultinomialNB, ComplementNB
from sklearn.svm import LinearSVC

from sklearn.model_selection import cross_val_score
from sklearn.metrics import classification_report
from sklearn.model_selection import train_test_split
from sklearn.metrics import confusion_matrix
from sklearn.utils.multiclass import unique_labels

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

    Using TensorFlow backend.



```python
# Plotting settings
import matplotlib
import matplotlib.pyplot as plt

%matplotlib inline
import seaborn as sns
sns.set()
from IPython.core.pylabtools import figsize
figsize(20, 20)
```

## Data Extraction and Exploratory Data Analysis :




```python
df = pd.read_csv(r'C:\Users\shrey\OneDrive\Desktop\news_group20.csv\news_group20.csv')
```


```python
# Preview of the dataframe
df.tail()
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
      <th>Unnamed: 0</th>
      <th>id</th>
      <th>category</th>
      <th>text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18823</th>
      <td>18823</td>
      <td>54843</td>
      <td>talk.politics.guns</td>
      <td>Subject: Waco headlines and editorial in Bosto...</td>
    </tr>
    <tr>
      <th>18824</th>
      <td>18824</td>
      <td>54539</td>
      <td>talk.politics.guns</td>
      <td>From: ccdarg@dct.ac.uk (Alan Greig)\nSubject: ...</td>
    </tr>
    <tr>
      <th>18825</th>
      <td>18825</td>
      <td>54353</td>
      <td>talk.politics.guns</td>
      <td>From: gs26@prism.gatech.EDU (Glenn R. Stone)\n...</td>
    </tr>
    <tr>
      <th>18826</th>
      <td>18826</td>
      <td>55240</td>
      <td>talk.politics.guns</td>
      <td>From: 6820230@LMSC5.IS.LMSC.LOCKHEED.COM\nSubj...</td>
    </tr>
    <tr>
      <th>18827</th>
      <td>18827</td>
      <td>55273</td>
      <td>talk.politics.guns</td>
      <td>From: jpsb@NeoSoft.com (Jim Shirreffs)\nSubjec...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Target classes
df.category.unique()
```




    array(['sci.crypt', 'rec.sport.hockey', 'rec.sport.baseball',
           'talk.politics.mideast', 'talk.politics.misc', 'comp.windows.x',
           'comp.os.ms-windows.misc', 'alt.atheism', 'rec.autos',
           'comp.sys.ibm.pc.hardware', 'talk.religion.misc', 'sci.space',
           'misc.forsale', 'sci.med', 'soc.religion.christian',
           'rec.motorcycles', 'sci.electronics', 'comp.sys.mac.hardware',
           'comp.graphics', 'talk.politics.guns'], dtype=object)




```python
# Count of articles
df.count()
```




    Unnamed: 0    18828
    id            18828
    category      18828
    text          18828
    dtype: int64



* Above we can see the preview of the dataframe with  category being the target classes which are categories of the article
* Text is an actual article in its unstructured form

## Labels distribution:
### From the graph below we see that our dataset is unbalanced. For classes talk.religion.misc, talk.politics.misc, alt.atheism we have a lot fewer samples, so that our classifier could be skewed towards bigger balanced labels.

These are the options to solve this issue:

* Undersampling - deleting samples from bigger classes in order to balance dataset. One of the most important points here is to keep the initial sample distribution inside the class group.
* Oversampling - generating new samples inside the minor classes in order to balance dataset. One of the most crucial issues here is that newly generated samples could represent fake-good distribution in the class group, which will not match to its real distribution.
* Balancing between under- and over- sampling


```python
# Counting the distribution of the Target Category
df.category.value_counts()
```




    rec.sport.hockey            999
    soc.religion.christian      997
    rec.motorcycles             994
    rec.sport.baseball          994
    sci.crypt                   991
    rec.autos                   990
    sci.med                     990
    sci.space                   987
    comp.os.ms-windows.misc     985
    comp.sys.ibm.pc.hardware    982
    sci.electronics             981
    comp.windows.x              980
    comp.graphics               973
    misc.forsale                972
    comp.sys.mac.hardware       961
    talk.politics.mideast       940
    talk.politics.guns          910
    alt.atheism                 799
    talk.politics.misc          775
    talk.religion.misc          628
    Name: category, dtype: int64




```python
df.category.value_counts().plot.barh()
```





![png](\images\text_mining_news\output_13_1.png)


## Dataset preprocessing and feature extraction
### Text preprocessing
In order to extract features from raw text, we have to somehow preprocess it. Typical simplified text preprocessing workflow:

<img src="https://i.ibb.co/Prrpgxg/nlp-preproc.png" />

1) **Tokenization** - inteligent splitting text into some kind of tokens (sentences, words, etc.)

2) **Cleaning** - cleaning text from all undesirable symbols or tokens or lines or whatever, it could be for example stop words or punctuation.

3) **Steaming** - rocess of reducing inflection in words to their root forms such as mapping a group of words to the same stem even if the stem itself is not a valid word in the Language. refference

4) **Lemmatization** - unlike Stemming, reduces the inflected words properly ensuring that the root word belongs to the language. In Lemmatization root word is called Lemma. A lemma (plural lemmas or lemmata) is the canonical form, dictionary form, or citation form of a set of words. refference

5) **Feature extraction** - vectorization of the ouput stems/lemmas. For example counting for each document or using TF-IDF.

### In our case I have chosen such workflow:

- Tokenization - using spaCy python library
- Cleaning - after investigating the content of raw emails, I have decided the next steps:
- Delete symbols !"#%&\*+,-<=>?[\\]{|}~
    - Delete lines, which begins with From: or end with writes:, autogenerated content by email host.
    - Delete email strings, From:, Re:, Subject:
    - Delete numbers
- Lemmatization - I have chosen lemmatization(spaCy) in favor of steaming(nltk), because it has shown ability to generate more robust results. I've used spaCy python library.
- Feature extraction - TF-IDF


```python
# Building methods to do all the above mentioned tasks

import re
import string

from sklearn.base import TransformerMixin

class TextPreprocessor(TransformerMixin):
    def __init__(self, text_attribute):
        self.text_attribute = text_attribute

    def transform(self, X, *_):
        X_copy = X.copy()
        X_copy[self.text_attribute] = X_copy[self.text_attribute].apply(self._preprocess_text)
        return X_copy

    def _preprocess_text(self, text):
        return self._lemmatize(self._leave_letters_only(self._clean(text)))

    def _clean(self, text):
        bad_symbols = '!"#%&\'*+,-<=>?[\\]^_`{|}~'
        text_without_symbols = text.translate(str.maketrans('', '', bad_symbols))

        text_without_bad_words = ''
        for line in text_without_symbols.split('\n'):
            if not line.lower().startswith('from:') and not line.lower().endswith('writes:'):
                text_without_bad_words += line + '\n'

        clean_text = text_without_bad_words
        email_regex = r'([a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+)'
        regexes_to_remove = [email_regex, r'Subject:', r'Re:']
        for r in regexes_to_remove:
            clean_text = re.sub(r, '', clean_text)

        return clean_text

    def _leave_letters_only(self, text):
        text_without_punctuation = text.translate(str.maketrans('', '', string.punctuation))
        return ' '.join(re.findall("[a-zA-Z]+", text_without_punctuation))

    def _lemmatize(self, text):
        doc = nlp(text)
        words = [x.lemma_ for x in [y for y in doc if not y.is_stop and y.pos_ != 'PUNCT'
                                    and y.pos_ != 'PART' and y.pos_ != 'X']]
        return ' '.join(words)

    def fit(self, *_):
        return self

```


```python
text_preprocessor = TextPreprocessor(text_attribute='text')

```


```python
df_preprocessed = text_preprocessor.transform(df)
```


```python
df_preprocessed.tail()
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
      <th>Unnamed: 0</th>
      <th>id</th>
      <th>category</th>
      <th>text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18823</th>
      <td>18823</td>
      <td>54843</td>
      <td>talk.politics.guns</td>
      <td>Waco headline editorial Boston Globe Boston Gl...</td>
    </tr>
    <tr>
      <th>18824</th>
      <td>18824</td>
      <td>54539</td>
      <td>talk.politics.guns</td>
      <td>atf BURNS dividian ranch SURVIVORS problem FBI...</td>
    </tr>
    <tr>
      <th>18825</th>
      <td>18825</td>
      <td>54353</td>
      <td>talk.politics.guns</td>
      <td>BATFFBI revenge anybody impeachment yeah Slick...</td>
    </tr>
    <tr>
      <th>18826</th>
      <td>18826</td>
      <td>55240</td>
      <td>talk.politics.guns</td>
      <td>original article Colorado Daily recently repri...</td>
    </tr>
    <tr>
      <th>18827</th>
      <td>18827</td>
      <td>55273</td>
      <td>talk.politics.guns</td>
      <td>Waco question Government garrotte neck citizen...</td>
    </tr>
  </tbody>
</table>
</div>



# Data Cleaning Required for some rows:


```python
#df_preprocessed.drop("Unnamed: 0", inplace=True, axis= 1)
```


```python
df_preprocessed.dropna(axis=0, inplace= True)
```


```python
df_preprocessed.to_csv(r'C:\Users\shrey\OneDrive\Desktop\processed_text_data.csv', index= False)
```


```python
df_preprocessed = pd.read_csv(r'C:\Users\shrey\OneDrive\Desktop\processed_text_data.csv')
```


```python
df_preprocessed.dropna(subset = ["text"], inplace=True)
```


```python
df_preprocessed.loc[df_preprocessed["text"].isna()]
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
      <th>Unnamed: 0</th>
      <th>id</th>
      <th>category</th>
      <th>text</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
print("Before text preprocession:\n",df.iloc[0,3])

print("---------------------------------------------------------------------------------------------------------")
print("Post text preprocessing:\n",df_preprocessed.iloc[0,3])
```

    Before text preprocession:
     From: hollasch@kpc.com (Steve Hollasch)
    Subject: Re: Clipper considered harmful

    brad@optilink.COM (Brad Yearwood) writes:
    | If Clipper comes to cellular phones along with legal proscriptions against
    | using other cipher systems on these phones, a new and potentially dangerous
    | class of crime is created.
    |
    | Criminals who very badly want inscrutable tactical communications
    | (specifically the terrorists and drug dealers who proponents of key escrow
    | cite as threats) will be highly motivated to steal the cipher phone of a
    | legitimate user, and to kill this person or hold them hostage so discovery
    | of compromise of the device will be delayed.

        Yow - get some sleep Brad!  You mean that people (i.e. life-is-cheap
    terrorists & drug-dealing warlords) who want to communicate in privacy will
    prefer to break into my house, kill or kidnap me, and steal my telephone,
    rather than:

            - Spending $15 at K-mart to buy a new phone.

            - Purchasing a load of phones from the black market / flea market /
              super market.

            - Talking (*gasp*) face-to-face.

            - Walking down to any one of millions of pay phones.

            - Using messengers.

            - Going to excruciating effort to think of code phrases like "I had
              a blowout on the freeway today".

        Look, this system does nothing to threaten folks who _know_ they're
    being wiretapped, since it's trivial to find other avenues of communication;
    they'd have no reason to resort to extreme measures, since a plethora of
    simple alternatives are easily available to them.

        Among all the legitimate reasons to damn the proposed system, I don't
    think we need to worry about terrorist commie drug warlord assasin thugs
    murdering our families, kicking the dog and leaving the toilet seat up just
    to steal a $15 telephone.  The system is more like urine testing:  it
    catches some small number of very stupid people, has no effect on the "bad
    guys" with at least three neurons working in unison who wish to subvert it,
    and penalizes most heavily those who have no cause to be subject to it.

    ______________________________________________________________________________
    Steve Hollasch                                   Kubota Pacific Computer, Inc.
    hollasch@kpc.com                                 Santa Clara, California

    ---------------------------------------------------------------------------------------------------------
    Post text preprocessing:
     clipper consider harmful Clipper come cellular phone legal proscription cipher
     system phone new potentially dangerous class crime create Criminals badly want
     inscrutable tactical communication specifically terrorist drug dealer proponent
     key escrow cite threat highly motivated steal cipher phone legitimate user kill
     person hold hostage discovery compromise device delay Yow sleep Brad mean people
     ie lifeischeap terrorist drugdeale warlord want communicate privacy prefer break
     house kill kidnap steal telephone spend Kmart buy new phone purchase load phone
     black market flea market super market talk gasp facetoface walk million pay phone
     messenger go excruciating effort think code phrase like blowout freeway today look
     system threaten folk know wiretappe trivial find avenue communication would reason
     resort extreme measure plethora simple alternative easily available legitimate reason
     damn propose system think need worry terrorist commie drug warlord assasin thug murder
     family kick dog leave toilet seat steal telephone system like urine test catch small
     number stupid people effect bad guy neuron work unison wish subvert penalize heavily
     cause subject Steve Hollasch Kubota Pacific Computer Inc Santa Clara California


### Feature extraction
To train TF-IDF vectorizer we have to split our dataset into train/test parts, I have chosen typical 70/30 ratio.


```python
from sklearn.model_selection import train_test_split

train, test = train_test_split(df_preprocessed, test_size=0.3)
```


```python
df_preprocessed.dtypes
```




    Unnamed: 0     int64
    id             int64
    category      object
    text          object
    dtype: object



To make TF-IDF vectorizer efficient, we have to specify rather large vocabulary(max_features). It causes very very large dataset dimensionality. Usually this causes RAM issues or computational time issues on the model training step.
Therefore, sklearn.feature_extraction.text.TfidfVectorizer returns sparse matrix as the output, which is much more memmory efficient and computational time efficient for some classifier models, which are able to deal with sparse matrices. But some of further preprocessing steps, are not able to deal with this, so the next steps will be very memory-consuming. Because of that I have chosen only 10 000 words vocabulary.


```python
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf_vectorizer = TfidfVectorizer(analyzer = "word", max_features=10000)

X_tfidf_train = tfidf_vectorizer.fit_transform(train['text'])
X_tfidf_test = tfidf_vectorizer.transform(test['text'])
```


```python
y = train['category']
y_test = test['category']
```

## Dataset Balancing:
As was afore-mentioned this dataset has to be somehow balanced, to get more robust results. In this case I prefer undersampling techniques, because it is more secure to delete than to generate, because this dataset is big enough to leave enough training samples.

**Here is an implementation of IHT in imbalanced-learn library based on the article above-mentioned. Samples that are classified with a low probability will be removed from the dataset. Afterwards, the model will be built on the undersampled data.**

I have chosen imbalanced-learn python package, which provides many models for balancing purposes.

As the undersampling model imblearn.under_sampling.InstanceHardnessThreshold with sklearn.svm.LinearSVC estimator was chosen. For more information about this undersampling method follow this
- [imbalanced-learn.readthedocs.io](https://imbalanced-learn.readthedocs.io/en/stable/under_sampling.html#instance-hardness-threshold)
- [https://towardsdatascience.com](https://towardsdatascience.com/instance-hardness-threshold-an-undersampling-method-to-tackle-imbalanced-classification-problems-6d80f91f0581)


```python
from sklearn.calibration import CalibratedClassifierCV
from imblearn.under_sampling import InstanceHardnessThreshold
from sklearn.svm import LinearSVC
```

### Encoding target categories:
**This resampling mathos is not very string friendly and our target classes are categories.**
To resolve this:
- Encode the Target classes to numbers.
- Save numbers to the category relation in a dictionary.
- After processing we will map back the string category in place using the dictionary.



```python
# converting to category
c = y.astype('category')

# Creating a dictionary for the relation
d = dict(enumerate(c.cat.categories))
```


```python
# Encoding y here to numbers
y= y.astype('category').cat.codes
```


```python
# Creating object for the InstanceHardnessThreshold
from sklearn.calibration import CalibratedClassifierCV
from imblearn.under_sampling import InstanceHardnessThreshold
from sklearn.svm import LinearSVC

iht = InstanceHardnessThreshold(random_state=0, n_jobs=11,
                                 estimator=CalibratedClassifierCV(
                                     LinearSVC(C=100, penalty='l1', max_iter=500, dual=False)
                                 ))
```


```python
# Fitting the dataset to the model
X_resampled, y_resampled = iht.fit_resample(X_tfidf_train, y)
print(sorted(Counter(y_resampled).items()))
```

    [(0, 439), (1, 439), (2, 439), (3, 439), (4, 439), (5, 439), (6, 439), (7, 439), (8, 439), (9, 439), (10, 439), (11, 439), (12, 439), (13, 439), (14, 439), (15, 439), (16, 439), (17, 439), (18, 439), (19, 439)]



```python
#encoding back to string categories using dictionary d
y_resampled = y_resampled.map(d)
```


```python
y_resampled.head()
```




    0    alt.atheism
    1    alt.atheism
    2    alt.atheism
    3    alt.atheism
    4    alt.atheism
    dtype: object




```python
print("Dataset shape: ", X_resampled.shape)
```

    Dataset shape:  (8780, 10000)



```python
X, y = X_resampled, y_resampled
X_test, y_test = X_tfidf_test, y_test
```

## Features scaling (standartization):

Most models requires features normalization to `(0, 1)` range in order to converge faster, for the rest models this step is optional. I think a good choice is to do that.
- We will use the basic Min Max Scalar here.


```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_norm = scaler.fit_transform(X.toarray())
X_test_norm = scaler.transform(X_test.toarray())
```

## Features selection:

We will select features based on the model `sklearn.svm.LinearSVC`, `sklearn.feature_selection.SelectFromModel` is able to select representative features based on coeficients or feature importances of the trained model.


```python
from sklearn.feature_selection import SelectFromModel

lsvc = LinearSVC(C=100, penalty='l1', max_iter=500, dual=False)
lsvc.fit(X_norm, y)
fs = SelectFromModel(lsvc, prefit=True)
X_selected = fs.transform(X_norm)
X_test_selected = fs.transform(X_test_norm)
```

    C:\Users\shrey\AppData\Local\Continuum\anaconda3\envs\PythonGPU\lib\site-packages\sklearn\svm\_base.py:977: ConvergenceWarning: Liblinear failed to converge, increase the number of iterations.
      "the number of iterations.", ConvergenceWarning)



```python
from IPython.display import Markdown, display

def show_top10_features(classifier, feature_names, categories):
    for i, category in enumerate(categories):
        top10 = np.argsort(classifier.coef_[i])[-10:]
        display(Markdown("**%s**: %s" % (category, ", ".join(feature_names[top10]))))
```


```python
feature_names = np.array(tfidf_vectorizer.get_feature_names())

# Lets check top 10 features for each topics:
show_top10_features(lsvc, feature_names, lsvc.classes_)
```


**alt.atheism**: mathew, doubtful, cobb, claws, quran, keith, rushdie, unicorn, evolve, beauchaine



**comp.graphics**: tiff, pov, spline, image, graphic, raytrace, cview, photoshop, animation, graphics



**comp.os.ms-windows.misc**: win, wfw, doublespace, risc, bnc, ftpcicaindianaedu, microsoft, bj, cica, windows



**comp.sys.ibm.pc.hardware**: xl, nanao, scsi, connector, lj, gateway, bios, ide, vlb, motherboard



**comp.sys.mac.hardware**: powerbook, lc, macs, duo, quadra, mac, pb, apple, iisi, centris



**comp.windows.x**: toolkit, colormap, server, xlib, openwindows, imake, xserver, xterm, widget, motif



**misc.forsale**: ton, wanted, asking, excellent, obo, offer, snes, sale, shipping, forsale



**rec.autos**: sho, wagon, engine, toyota, shift, ford, vx, auto, warningplease, car



**rec.motorcycles**: dwi, helmet, rider, moa, ride, yamaha, motorcycle, biker, dod, bike



**rec.sport.baseball**: giants, sox, career, batter, mets, braves, umpire, jays, pitcher, baseball



**rec.sport.hockey**: espn, cup, leafs, bruins, pens, goalie, penguin, playoff, nhl, hockey



**sci.crypt**: lobby, remailer, escrow, nsa, overreact, tap, cryptography, clipper, encryption, crypto



**sci.electronics**: cellar, assembler, atari, electronic, ic, scope, dial, microcontroller, circuit, voltage



**sci.med**: allergy, disease, krillean, homeopathy, medical, treatment, muscle, methodology, infection, diet



**sci.space**: bursters, smiley, rocket, orbit, scispace, shuttle, moon, launch, space, spacecraft



**soc.religion.christian**: catholic, church, sin, prayer, christ, coming, scripture, arrogance, kiefer, clh



**talk.politics.guns**: rifle, handgun, batffbi, censor, hci, weapon, atf, firearm, gun, dividian



**talk.politics.mideast**: bosnians, racism, israels, israel, arab, turkish, bosnian, uva, armenians, israeli



**talk.politics.misc**: verdict, economic, hypocrisy, liberal, clayton, cramer, gay, mow, sexual, kaldis



**talk.religion.misc**: sword, mormons, beast, tyre, weiss, burden, trm, muhammad, sabin, mithras


This output shows classes and most important features for them. Most of them makes good sence with the corresponding category. Sometimes there are some irrelevantes like `rec.motorcycles: dog`.


```python
print("New dataset shape: ", X_selected.shape)
print("Features reducted: ", X_norm.shape[1] - X_selected.shape[1])
```

    New dataset shape:  (8780, 4774)
    Features reducted:  5226


## Model training and evaluation

I've tried more than 10 different model instances, with a great batch of different hyperparameters. The experimets were held using `sklearn.model_selection.GridSearchCV` with cross validation size 5. These experiments run more than 2 days non stop on my PC, and here I want to show condensed results of 5 models, their evaluation and result selection


```python
from sklearn.linear_model import LogisticRegression, SGDClassifier
from sklearn.ensemble import VotingClassifier
from sklearn.naive_bayes import MultinomialNB, ComplementNB
from sklearn.svm import LinearSVC

from sklearn.model_selection import cross_val_score
from sklearn.metrics import classification_report
```


```python
# this snippet was taken from https://gist.github.com/shaypal5/94c53d765083101efc0240d776a23823

from sklearn.model_selection import train_test_split
from sklearn.metrics import confusion_matrix
from sklearn.utils.multiclass import unique_labels

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Function to build Heatmap using the confusion matrix received from the models
def print_confusion_matrix(confusion_matrix,
                           class_names,
                           figsize = (15,15),
                           fontsize=12,
                           ylabel='True label',
                           xlabel='Predicted label'):

    df_cm = pd.DataFrame(
        confusion_matrix, index=class_names, columns=class_names,
    )
    fig = plt.figure(figsize=figsize)
    try:
        heatmap = sns.heatmap(df_cm, annot=True, fmt="d")
    except ValueError:
        raise ValueError("Confusion matrix values must be integers.")
    heatmap.yaxis.set_ticklabels(heatmap.yaxis.get_ticklabels(), rotation=0, ha='right', fontsize=fontsize)
    heatmap.xaxis.set_ticklabels(heatmap.xaxis.get_ticklabels(), rotation=45, ha='right', fontsize=fontsize)
    plt.ylabel(ylabel)
    plt.xlabel(xlabel)
```


```python
# Function to evaluate models
def evaluate_model(model, X, y, X_test, y_test, target_names=None):
    scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')
    scores_test = cross_val_score(model, X_test, y_test, cv=5, scoring='accuracy')

    print("Accuracy: %0.2f (+/- %0.2f)" % (scores.mean(), scores.std()))
    print("Accuracy test: %0.2f (+/- %0.2f)" % (scores_test.mean(), scores_test.std()))

    print("Test classification report: ")
    if target_names is None:
        target_names = model.classes_
    print(classification_report(y_test, model.predict(X_test), target_names=target_names))
    print("Test confusion matrix: ")
    print_confusion_matrix(confusion_matrix(y_test, model.predict(X_test)), class_names=target_names)
```

### Multinominal Naive Bayes

For `MultinomialNB` we see that the most misclassified groups are `alt.atheism`, `talk.politics.misc` and `talk.religion.misc`. A lot of `talk.religion.misc` were classified into very close group `soc.religion.christian`. And probably in this dataset contains mostly republican mails, if so many `talk.politics.misc` were classified in `talk.politics.guns`.


```python
mb = MultinomialNB()
mb.fit(X_selected, y_resampled)
evaluate_model(mb, X_selected, y, X_test_selected, y_test)
```

    Accuracy: 0.94 (+/- 0.00)
    Accuracy test: 0.78 (+/- 0.00)
    Test classification report:
                              precision    recall  f1-score   support

                 alt.atheism       0.77      0.78      0.77       257
               comp.graphics       0.66      0.77      0.71       290
     comp.os.ms-windows.misc       0.73      0.80      0.76       289
    comp.sys.ibm.pc.hardware       0.74      0.71      0.72       307
       comp.sys.mac.hardware       0.74      0.75      0.74       276
              comp.windows.x       0.79      0.83      0.81       282
                misc.forsale       0.80      0.79      0.80       261
                   rec.autos       0.86      0.84      0.85       271
             rec.motorcycles       0.89      0.90      0.90       328
          rec.sport.baseball       0.95      0.88      0.91       296
            rec.sport.hockey       0.91      0.94      0.92       293
                   sci.crypt       0.91      0.89      0.90       330
             sci.electronics       0.81      0.71      0.76       287
                     sci.med       0.90      0.82      0.86       301
                   sci.space       0.91      0.88      0.89       277
      soc.religion.christian       0.78      0.89      0.83       307
          talk.politics.guns       0.79      0.90      0.84       295
       talk.politics.mideast       0.92      0.91      0.92       281
          talk.politics.misc       0.76      0.77      0.77       233
          talk.religion.misc       0.74      0.48      0.58       188

                    accuracy                           0.82      5649
                   macro avg       0.82      0.81      0.81      5649
                weighted avg       0.82      0.82      0.82      5649

    Test confusion matrix:



![png](\images\text_mining_news\output_57_1.png)


### Complement Naive Bayes

For `ComplementNB` we see that the overall accuracy is better than in previous case, but `alt.atheism`, `talk.politics.misc` and `talk.religion.misc` are misclassified even worse.


```python
cb = ComplementNB()
cb.fit(X_selected, y_resampled)
evaluate_model(cb, X_selected, y, X_test_selected, y_test)
```

    Accuracy: 0.94 (+/- 0.00)
    Accuracy test: 0.80 (+/- 0.00)
    Test classification report:
                              precision    recall  f1-score   support

                 alt.atheism       0.75      0.75      0.75       257
               comp.graphics       0.76      0.74      0.75       290
     comp.os.ms-windows.misc       0.75      0.81      0.78       289
    comp.sys.ibm.pc.hardware       0.74      0.72      0.73       307
       comp.sys.mac.hardware       0.87      0.78      0.82       276
              comp.windows.x       0.78      0.85      0.82       282
                misc.forsale       0.78      0.77      0.77       261
                   rec.autos       0.88      0.88      0.88       271
             rec.motorcycles       0.94      0.92      0.93       328
          rec.sport.baseball       0.95      0.91      0.93       296
            rec.sport.hockey       0.91      0.97      0.94       293
                   sci.crypt       0.90      0.92      0.91       330
             sci.electronics       0.82      0.70      0.75       287
                     sci.med       0.86      0.84      0.85       301
                   sci.space       0.87      0.90      0.88       277
      soc.religion.christian       0.74      0.89      0.81       307
          talk.politics.guns       0.79      0.91      0.85       295
       talk.politics.mideast       0.87      0.95      0.91       281
          talk.politics.misc       0.81      0.72      0.76       233
          talk.religion.misc       0.66      0.39      0.49       188

                    accuracy                           0.83      5649
                   macro avg       0.82      0.82      0.82      5649
                weighted avg       0.83      0.83      0.82      5649

    Test confusion matrix:



![png](\images\text_mining_news\output_59_1.png)


## Logistic regression
For `LogisticRegression` `alt.atheism` is classified much more better, `talk.politics.misc` and `talk.religion.misc` are still misclassified, but looks better than the previous cases. This classifier but has some problems with hardware of different companies.


```python
lr = LogisticRegression(C=10000, penalty='l2', multi_class='ovr')
lr.fit(X_selected, y)
evaluate_model(lr, X_selected, y, X_test_selected, y_test)
```
    Accuracy: 0.97 (+/- 0.00)
    Accuracy test: 0.77 (+/- 0.00)
    Test classification report:
                              precision    recall  f1-score   support

                 alt.atheism       0.77      0.80      0.79       257
               comp.graphics       0.70      0.79      0.74       290
     comp.os.ms-windows.misc       0.77      0.81      0.79       289
    comp.sys.ibm.pc.hardware       0.75      0.67      0.71       307
       comp.sys.mac.hardware       0.79      0.76      0.78       276
              comp.windows.x       0.78      0.84      0.81       282
                misc.forsale       0.76      0.86      0.81       261
                   rec.autos       0.88      0.86      0.87       271
             rec.motorcycles       0.95      0.89      0.92       328
          rec.sport.baseball       0.96      0.89      0.92       296
            rec.sport.hockey       0.96      0.96      0.96       293
                   sci.crypt       0.96      0.88      0.91       330
             sci.electronics       0.79      0.80      0.80       287
                     sci.med       0.88      0.83      0.85       301
                   sci.space       0.93      0.87      0.90       277
      soc.religion.christian       0.87      0.83      0.85       307
          talk.politics.guns       0.91      0.83      0.87       295
       talk.politics.mideast       0.95      0.92      0.93       281
          talk.politics.misc       0.77      0.82      0.80       233
          talk.religion.misc       0.57      0.78      0.66       188

                    accuracy                           0.84      5649
                   macro avg       0.84      0.83      0.83      5649
                weighted avg       0.84      0.84      0.84      5649

    Test confusion matrix:



![png](\images\text_mining_news\output_61_2.png)


## SGD
`SGDClassifier` one of the most robust concerning `alt.atheism`, `talk.politics.misc` and `talk.religion.misc` groups, with good overall test accuracy and other metrics.


```python
%%time
sgd = SGDClassifier(alpha=.0001, max_iter=50, loss='log',
                                       penalty="elasticnet", n_jobs=-1)
sgd.fit(X_selected, y)
evaluate_model(sgd, X_selected, y, X_test_selected, y_test)
```

    Accuracy: 0.97 (+/- 0.00)
    Accuracy test: 0.80 (+/- 0.01)
    Test classification report:
                              precision    recall  f1-score   support

                 alt.atheism       0.83      0.77      0.80       257
               comp.graphics       0.63      0.82      0.71       290
     comp.os.ms-windows.misc       0.80      0.77      0.79       289
    comp.sys.ibm.pc.hardware       0.75      0.71      0.73       307
       comp.sys.mac.hardware       0.82      0.73      0.77       276
              comp.windows.x       0.77      0.80      0.78       282
                misc.forsale       0.77      0.82      0.80       261
                   rec.autos       0.88      0.81      0.84       271
             rec.motorcycles       0.95      0.87      0.91       328
          rec.sport.baseball       0.96      0.86      0.91       296
            rec.sport.hockey       0.98      0.94      0.95       293
                   sci.crypt       0.96      0.85      0.90       330
             sci.electronics       0.65      0.85      0.74       287
                     sci.med       0.89      0.82      0.85       301
                   sci.space       0.93      0.86      0.89       277
      soc.religion.christian       0.89      0.82      0.85       307
          talk.politics.guns       0.88      0.85      0.86       295
       talk.politics.mideast       0.96      0.90      0.93       281
          talk.politics.misc       0.76      0.80      0.78       233
          talk.religion.misc       0.53      0.78      0.63       188

                    accuracy                           0.82      5649
                   macro avg       0.83      0.82      0.82      5649
                weighted avg       0.84      0.82      0.83      5649

    Test confusion matrix:



![png](\images\text_mining_news\output_63_1.png)


If we sum up these results we can see, that `LogisticRegression` and `SGDClassifier` gives us the best results, but sometimes in come cases `MultinominalNB` shows a little bit beter performance. Why not to combine them into soft voting ensemble, that will balance these results.

In contrast to majority voting (hard voting), soft voting returns the class label as argmax of the sum of predicted probabilities. [Full description of soft voting](https://scikit-learn.org/stable/modules/ensemble.html#weighted-average-probabilities-soft-voting)


```python
vclf_sgd = VotingClassifier(estimators=[
         ('lr', LogisticRegression(C=10000, penalty='l2', multi_class='ovr')),
        ('mb', MultinomialNB()),
        ('sgd', SGDClassifier(alpha=.0001, max_iter=50, loss='log',
                                       penalty="elasticnet"))], voting='soft', n_jobs=-1)

```


```python
vclf_sgd.fit(X_selected, y)
evaluate_model(vclf_sgd, X_selected, y, X_test_selected, y_test)

```
    Accuracy: 0.98 (+/- 0.00)
    Accuracy test: 0.81 (+/- 0.00)
    Test classification report:
                              precision    recall  f1-score   support

                 alt.atheism       0.79      0.76      0.78       251
               comp.graphics       0.75      0.82      0.79       317
     comp.os.ms-windows.misc       0.76      0.82      0.79       285
    comp.sys.ibm.pc.hardware       0.72      0.74      0.73       291
       comp.sys.mac.hardware       0.87      0.78      0.83       299
              comp.windows.x       0.84      0.82      0.83       277
                misc.forsale       0.81      0.82      0.82       288
                   rec.autos       0.89      0.88      0.88       304
             rec.motorcycles       0.93      0.91      0.92       316
          rec.sport.baseball       0.96      0.93      0.94       300
            rec.sport.hockey       0.97      0.95      0.96       310
                   sci.crypt       0.95      0.89      0.92       292
             sci.electronics       0.80      0.80      0.80       301
                     sci.med       0.91      0.84      0.87       275
                   sci.space       0.91      0.90      0.91       295
      soc.religion.christian       0.85      0.85      0.85       291
          talk.politics.guns       0.85      0.84      0.85       245
       talk.politics.mideast       0.93      0.90      0.92       276
          talk.politics.misc       0.73      0.82      0.77       236
          talk.religion.misc       0.63      0.72      0.67       200

                   micro avg       0.84      0.84      0.84      5649
                   macro avg       0.84      0.84      0.84      5649
                weighted avg       0.85      0.84      0.84      5649

    Test confusion matrix:

![png](\images\text_mining_news\__results___51_1.png)  


## Comparison

Now we have to compare all these classifiers and select the best match for this task. I'll do it in a way of difference of the overall accuracy, and accuracy on the problematic groups.


```python
clfs = (('ComplementNB', cb),
        ('MultinomialNB', mb),
        ('LinearSVC', lsvc),
        ('LogisticRegression', lr),
        ('SGDClassifier', sgd),
        ('VotingClassifier', vclf_sgd))

for _x, _y in ((0,0), (4,4), (18,18), (19,19)):
    mtx = np.zeros((len(clfs), (len(clfs))), dtype=int)

    for i, (label1, clf1) in enumerate(clfs):
        for j, (label2, clf2) in enumerate(clfs):
            mtx[i][j] = (confusion_matrix(y_test, clf1.predict(X_test_selected))
                            -confusion_matrix(y_test, clf2.predict(X_test_selected)))[_x][_y]
    display(Markdown(f"Differect of correctly classified: **{clf2.classes_[_x]}**"))
    print_confusion_matrix(mtx, class_names=[l for l, _ in clfs], xlabel="", ylabel="", figsize=(5,5))
    plt.show()

mtx = np.zeros((len(clfs), (len(clfs))), dtype=int)
for i, (label1, clf1) in enumerate(clfs):
    for j, (label2, clf2) in enumerate(clfs):
        mtx[i][j] = (confusion_matrix(y_test, clf1.predict(X_test_selected))
                        -confusion_matrix(y_test, clf2.predict(X_test_selected))).diagonal().sum()
display(Markdown(f"**Overall** correctly classified"))
print_confusion_matrix(mtx, class_names=[l for l, _ in clfs], xlabel="", ylabel="", figsize=(5,5))
```
Differect of correctly classified: `alt.atheism`

![png](\images\text_mining_news\results53_1.png)

Differect of correctly classified: `comp.sys.mac.hardware`

![png](\images\text_mining_news\results53_3.png)

Differect of correctly classified: `talk.politics.misc`

![png](\images\text_mining_news\results53_5.png)

Differect of correctly classified: `talk.religion.misc`

![png](\images\text_mining_news\results53_7.png)

**Overall correctly classified**

![png](\images\text_mining_news\results53_9.png)
