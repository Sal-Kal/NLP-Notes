#Pre-Processing
- Regex can be used to filter out necessary phrases from the dataset for the training process.
- Regex Cheat Sheet for Python - [Cheat Sheet](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)
- Website to test your regexes - [Regex101](https://regex101.com)
- Example:
```python
import re

# A regular expression to check for a word that starts with ab and ends with cd and can have any number of any characters in between apart from white spaces
regexp = re.compile(r"^ab[^\s]*cd$")

phrases = ["abcd", "xxx", "abxxxcd", "ab cd"]

matches = []
for phrase in phrases:
    if re.match(regexp, phrase):
        matches.append(phrase)
print(matches)
```
Output:
```
['abcd', 'abxxxcd']
```