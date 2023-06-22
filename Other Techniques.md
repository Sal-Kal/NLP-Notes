#Pre-Processing
## Spell Check
```python
from textblob import TextBlob

phrase = "this is an examle"

tb_phrase = TextBlob(phrase)

tb_phrase.correct()
```
Output:
```
TextBlob("this is an example")
```
## Part to speech tagging
Understand part to speech [here](https://towardsdatascience.com/part-of-speech-tagging-for-beginners-3a0754b2ebba) and [here](https://www.learntek.org/blog/categorizing-pos-tagging-nltk-python/)
```python
# Installing necessary libaries
nltk.download("averaged_perceptron_tagger")
from textblob import TextBlob

phrase = "i read the book"

tb_phrase = TextBlob(phrase)

tb_phrase.tags
```
Output:
```
[('i', 'NN'), ('read', 'VBD'), ('the', 'DT'), ('book', 'NN')]
```
In case of ssl errors run the snippet present [[Stemming & Lemmatization|here]].
## Sentiment
```python
phrase = "the book sucked, it was horrible"

tb_phrase = TextBlob(phrase)

tb_phrase.sentiment
```
Output:
```
Sentiment(polarity=-1.0, subjectivity=1.0)

```
Another example
```python
phrase = "the book was great"

tb_phrase = TextBlob(phrase)

tb_phrase.sentiment
```
Output:
```
Sentiment(polarity=0.8, subjectivity=0.75)
```