### Currently there are 2 Named Entity Recognition Models:
* Entity Ruler Based
* Machine Learning Based
---
### Entity Ruler Based:
This is the model that is currently pushed to the gitlab.
#### Algorithm:
The following steps are with respect to the `pfm_categorizer.py` file.
1. The narrations are preprocessed in the following manner:
	- All special characters are replaced with spaces. (inbuilt algorithm)
	- Junk terms such as `8904370936` or `20230323MA00010000244` are removed. (inbuilt algorithm)
	- Multiple white spaces within the narration are removed. (inbuilt algorithm)
	- NLTK stopwords and custom stopwords are removed. (custom algorithm)
	- Duplicate terms are removed without distrubing the order of the words in the narration. (custom algorithm)
 2. Now an attempt is made to recognize Entities using the NER model (Entity Ruler Based):
	- The NER model takes the preprocessed string and identifies terms which are present in the look up json file. Entities are identified with their categories if found in the json look up file. (inbuilt algorithm)
	- If multiple categories are found within the same narration then:
		- The category with frequency more than 1 is returned. (custom algorithm)
		- If all categories found have same frequency (i.e. 1) then the first category is returned. (custom algorithm)
 3. If entites were not found:
	- Each term in the narration is split further (only if possible) using the `wordninja` python library. (inbuilt algorithm)
	- Now stop words are removed from this new split up narration. (custom algorithm)
	- Now another attempt is made to find Entities using the NER model is made and the same substeps follow as said in Step 2.
 4. If entities are still not found:
	- Payment modes are identified as either `P2P` or `P2M` and the Rule Engine is invoked.
 ---
### Machine Learning Based:
This model is not pushed to gitlab currently and does not use any json look up file. This model does everything exactly as the Entity Ruler Based NER model except for when it comes to identifying the entities and their categories. Instead of looking up the json file, it uses ML to identify the entities and their corresponding categories.
When entities are not found the Rule Engine is invoked.

---
### The Training Process of the Machine Learning Based NER Model:
- The training of this model requires a dataset which is in the form of json. It requires the narrations with their identified entities and categories along with location of the entities within the narration for training.
- The narrations used while training are preprocessed using the same algorithm as mentioned in the Entity Ruler Based NER Model. This is done because once trained, the model should work on pre processed narrations and not on non pre processed narrations.
- This dataset has been generated using the Entity Ruler Based NER Model. In other words around 3 Lack narrations were feeded to the Entity Ruler Based NER Model (which uses a json file for looking up the entities) and the output has been compiled into a json file for training purposes.
- Out of the 3 Lack narrations the Entity Ruler Based NER Model could find entities and their corresponding categories for only 1 Lack narrations. In a deployed environment the rest 2 Lack narrations would have invoked the Rule Engine.
An example entry in the training dataset:
```json
[
	"ACH BIRLAMF CAMS",
	{
		"entities": [
			[
				0,
				3,
				"Equity Dividend"
			],
			[
				4,
				11,
				"Investment expense"
			]
		]
	}
],
```
In the above example `ACH BIRLAMF CAMS` is obtained after pre processing.
`ACH` is an entity belonging to the category `Equity Dividend` and `BIRLAMF` is an entity belonging to the category `Investment expense`.