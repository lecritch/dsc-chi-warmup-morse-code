
# Decode Morse Code

This morning we will be writing a function to translate a poem that has been encoded with morse code.

![](https://media.giphy.com/media/4AUH1t6ccRfhe/giphy.gif)

**Import modules**


```python
# os is used to create file paths
import os
# pickle is used to import data files
import pickle
# test package
from test_scripts.test_class import Test
```

**In the cell below, we import the encoded poem.**


```python
path_to_poem = os.path.join('data', 'morseCode.pkl')
with open(path_to_poem, 'rb') as file:
    data = pickle.load(file)
```

**Let's take a look at the first line of the poem**


```python
data[0]
```

**A dictionary of morse code mapping is imported below.**


```python
# Import decode dictionary
decode_path = os.path.join('data', 'morseMappings.pkl')
with open(decode_path, 'rb') as file:
    decode = pickle.load(file)

print(decode)
```

**The keys of this dictionary are morse code and the values are english characters.**

To translate the poem, we simply have to feed each encoded letter into the dictionary as a key, and we will receive their decoded values.

*Important information:*

>The encoded poem uses a forward slash ```'/'``` to seperate words and a space ```' '``` to seperate each letter.

Using the ```decode``` dictionary, please build a function that can translate the poem from morse code to english sentences.

<u>To do this, the function should:</u>
1. Receive a single encoded string called ```morse_code```.
2. Split the encoded string using ```'/'``` as a seperator.
3. Loop over the list of encoded words.
4. Split a given word using ```' '``` as a seperator.
5. Loop over each letter in a given word.
6. Feed the letter into the ```decode``` dictionary as a key.
7. Append each decoded word to a string with spaces between each word
8. No spaces should be present at the beginning or the end of a decoded sentence. 


```python
# Your code here
def decode_morse(morse_code):
    pass
```

<u><b>Run the cell below to test your function!</b></u>


```python
test = Test()
poem = [decode_morse(line) for line in data]
test.run_test(poem, 'poem')
```

### Now, let's test our function against the entire play ```The Tragedy of Julius Caesar```


```python
# Import encoded data
caesar_path = os.path.join('data', 'juliusCaesarEncoded.pkl')
with open(caesar_path, 'rb') as file:
    caesar = pickle.load(file)
    
# Run our function on every line of the play
caesar_decoded = [decode_morse(line) for line in caesar]

# Test the results!
test.run_test(caesar_decoded, 'caesar')
```

# Enjoy Mod 3 :)

![](https://media.giphy.com/media/vzO0Vc8b2VBLi/giphy.gif)


```python

```
