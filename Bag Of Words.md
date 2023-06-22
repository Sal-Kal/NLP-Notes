#Approaches
- Visit sklearn's website for examples on Bag of Words [here](https://scikit-learn.org/stable/modules/feature_extraction.html).
- Text is not a numerical vector. The Bag of Words approach is used to convert these texts into a numerical representation.
- We use `CountVectorizer` from `sklearn` library as shown below
```python
from sklearn.feature_extraction.text import CountVectorizer 

train_x = ["i love the book", 
		   "this is a great book", 
		   "the fit is great", 
		   "i love the shoes"]

vectorizer = CountVectorizer()

vectors = vectorizer.fit_transform(train_x)

print(vectorizer.get_feature_names_out())

print(vectors.toarray())
```
Output:
```
['book' 'fit' 'great' 'is' 'love' 'shoes' 'the' 'this'] 
[[1 0 0 0 1 0 1 0] 
 [1 0 1 1 0 0 0 1] 
 [0 1 1 1 0 0 1 0] 
 [0 0 0 0 1 1 1 0]]
```
- We have essentially created a vector for the count of each unique word.
- The `get_feature_names_out()` function gives us the unique words from our list of sentences.
- The `vectors.toarray()` gives us a vector showing the occurences of each unique word in the list.
- We can give `CountVectorize(binary = true)` when we don't want the count of each unique word but to check if those words have occured at least once. The value in the vector will be `1` if the word occurs and `0` if it doesn't.
- We can now train our model from this vector as shown below.
```python
class Category:
    BOOKS = "BOOKS"
    CLOTHING = "CLOTHING"
train_y = [Category.BOOKS, Category.BOOKS, Category.CLOTHING, Category.CLOTHING]

from sklearn import svm
clf_svm = svm.SVC(kernel='linear')
clf_svm.fit(vectors,train_y)
```
Prediction:
```python
test_x = vectorizer.transform(['i adore the shoes'])
clf_svm.predict(test_x)
```
Output:
```
array(['CLOTHING'], dtype='<U8')
```
- This is unigram approach where a single word is it's own unique utterance. We can also have a bigram approach where a combination of two words make one unique utterance. This can be done as shown below.
```python
vectorizer = CountVectorizer(ngram_range=(1,2))
vectors = vectorizer.fit_transform(train_x)
print(vectorizer.get_feature_names_out())
print(vectors.toarray())
```
Output:
```
['book' 'fit' 'fit is' 'great' 'great book' 'is' 'is great' 'love' 'love the' 'shoes' 'the' 'the book' 'the fit' 'the shoes' 'this' 'this is'] 
[[1 0 0 0 0 0 0 1 1 0 1 1 0 0 0 0] 
 [1 0 0 1 1 1 1 0 0 0 0 0 0 0 1 1] 
 [0 1 1 1 0 1 1 0 0 0 1 0 1 0 0 0] 
 [0 0 0 0 0 0 0 1 1 1 1 0 0 1 0 0]]
```

- <b>The problem with Bag of Words approach is that it doesn't work well when the test data has words which are not present in the bag of words.</b>