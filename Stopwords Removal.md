#Pre-Processing 
```python 
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords

stop_words = stopwords.words('english')
print(stop_words)
```
- The above snippet prints all the common stop words in English such as _i, me, myself, the,_ etc.
- Example for removing stopwords from a sentence:
```python
phrase = "Here is an example sentence demonstrating the removal of stop words"

words = word_tokenize(phrase)
stripped_phrase = []

for word in words:
    if word not in stop_words:
        stripped_phrase.append(word)

print(stripped_phrase)
```
Output:
```
['Here', 'example', 'sentence', 'demonstrating', 'removal', 'stop', 'words']
```