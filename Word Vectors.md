#Approaches
- Similar to Bag of words, texts are converted into numerical vectors.
- The aim is to capture the semantic meaning of a word in a vector.
- Relations between words are identified if those words often occur together in multiple sentences. This is often done by a neural network architecture.
- More info about word vectors and using them with the `spacy` library can be found [here](https://spacy.io/api/vectors)
- [Word Embedding](https://machinelearningmastery.com/what-are-word-embeddings/)
- Below is an example of to create a word vector representation of a list of sentences.
```python
import spacy
nlp = spacy.load("en_core_web_md")

train_x = ["i love the book", 
		   "this is a great book", 
		   "the fit is great", 
		   "i love the shoes"]

docs = [nlp(text) for text in train_x]
print(docs[0].vector)
```
- Each sentence in the list gets word embedded.
- We can fit a model with these vectors as training data.
```python
train_x_wv = [x.vector for x in docs]
classifier_wv = svm.SVC()
# here train_y is the same one used in Bag of Words approach
classifier_wv.fit(train_x_wv, train_y)
```
- Prediction:
```python
test_x = ["these earings hurt"]
test_docs = [nlp(text) for text in test_x]
test_x_wv = [x.vector for x in test_docs]
classifier_wv.predict(test_x_wv)
```
- Output:
```
array(['CLOTHING'], dtype='<U8')
```
- <b>The drawback of using Word Vectors is when the data is too big, due to the word embeddings some words may start losing their meaning.</b>

