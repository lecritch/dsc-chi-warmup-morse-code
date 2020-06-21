
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


```python
# __SOLUTION__
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


```python
# __SOLUTION__
path_to_poem = os.path.join('data', 'morseCode.pkl')
with open(path_to_poem, 'rb') as file:
    data = pickle.load(file)
```

**Let's take a look at the first line of the poem**


```python
data[0]
```


```python
# __SOLUTION__
data[0]
```




    '- .... ./--.. . -./--- ..-./.--. -.-- - .... --- -. --..--/-... -.--/- .. --/.--. . - . .-. .../'



**A dictionary of morse code mapping is imported below.**


```python
# Import decode dictionary
decode_path = os.path.join('data', 'morseMappings.pkl')
with open(decode_path, 'rb') as file:
    decode = pickle.load(file)

print(decode)
```


```python
# __SOLUTION__
# Import decode dictionary
decode_path = os.path.join('data', 'morseMappings.pkl')
with open(decode_path, 'rb') as file:
    decode = pickle.load(file)

print(decode)
```

    {'.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E', '..-.': 'F', '--.': 'G', '....': 'H', '..': 'I', '.---': 'J', '-.-': 'K', '.-..': 'L', '--': 'M', '-.': 'N', '---': 'O', '.--.': 'P', '--.-': 'Q', '.-.': 'R', '...': 'S', '-': 'T', '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X', '-.--': 'Y', '--..': 'Z', '.----': '1', '..---': '2', '...--': '3', '....-': '4', '.....': '5', '-....': '6', '--...': '7', '---..': '8', '----.': '9', '-----': '0', '--..--': ',', '.-.-.-': '.', '..--..': '?', '-..-.': '/', '-....-': '-', '-.--.': '(', '-.--.-': ')', '-.-.--': '!', '.----.': "'", '---...': ':', '.-...': '&'}


**The keys of this dictionary are morse code and the values are english characters.**

To translate the poem, we simply have to feed each encoded letter into the dictionary as a key, and we will receive its decoded value.

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
7. Append each decoded letter to a string
8. Append each decoded word to a string with spaces between each word
9. No spaces should be present at the beginning or the end of a decoded sentence. 


```python
# Your code here
def decode_morse(morse_code):
    pass
```


```python
# __SOLUTION__
def decode_morse(morse_code):
    decoded = ''
    words = morse_code.split('/')
    for word in words:
        letters = word.split()
        length = len(letters)
        for idx in range(length):
            letter = letters[idx]
            if letter in decode.keys():
                decoded += decode[letter]
            if idx == length - 1:
                decoded += ' '
    decoded = decoded.strip()
    return decoded       
```

<u><b>Run the cell below to test your function!</b></u>


```python
test = Test()
poem = [decode_morse(line) for line in data]
test.run_test(poem, 'poem')
```


```python
# __SOLUTION__
test = Test()
poem = [decode_morse(line) for line in data]
test.run_test(poem, 'poem')
```


✅ **Hey, you did it.  Good job.**


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


```python
# __SOLUTION__
# Import encoded data
with open('data/juliusCaesarEncoded.pkl', 'rb') as file:
    caesar = pickle.load(file)

# Run our function on every line of the play    
decoded_caesar = [decode_morse(line) for line in caesar]

# Test the results!
test.run_test(decoded_caesar, 'caesar')
```


✅ **Hey, you did it.  Good job.**


# Enjoy Mod 3 :)

![](https://media.giphy.com/media/vzO0Vc8b2VBLi/giphy.gif)


```python
# __SOLUTION__
# This cell is used to create the data for this warmup, and is reliant on a data/ subdirectory. 

# Import morse code mappings dictionary
with open('data/morseMappings.pkl', 'rb') as file:
    morse_mappings = pickle.load(file)
    
# The imported dictionary has morse code as keys and 
# uppercase alphabetic, numeric, and punctuation characters as values.
# To encode text to morse code, we must swap the keys and values
morse_encoding = {value: key for key, value in morse_mappings.items()}

def morse(text):
    '''Function to encode text as morse code.
       Each word is seperated using a forward slash "/"
       Each letter is seperated used a single space " "
       
       This function is reliant on a global morse_encoding dictionary
       that has Alpha numeric, uppercase, keys and morse code as values.
       '''
    # Change letters to upper case to match the keys in the morse_encoding dictionary
    # Split string using a single space " " as a seperator
    split = text.upper().split()
    # Create an empty string to append each encoded word to
    sentence = ''
    # Loop over the list of words
    for word in split:
        # Create an empty string to append each encoded letter to
        w = ''
        # Loop over each letter in the word using the index to ensure
        # we do not add a space at the end of the sentence
        ##### This could also be accomplished 
        ##### by using .strip()
        for idx in range(len(word)):
            w += morse_encoding[word[idx]]
            if idx == len(word) - 1:
                pass
            else:
                w += ' '
        # Once every letter has been encoded,
        # append a forward slash at the of the word
        sentence += w + '/'
    return sentence 

poem = ["The Zen of Python, by Tim Peters",
"Beautiful is better than ugly.",
"Explicit is better than implicit.",
"Simple is better than complex.",
"Complex is better than complicated.",
"Flat is better than nested.",
"Sparse is better than dense.",
"Readability counts.",
"Special cases aren't special enough to break the rules.",
"Although practicality beats purity.",
"Errors should never pass silently.",
"Unless explicitly silenced.",
"In the face of ambiguity, refuse the temptation to guess.",
"There should be one-- and preferably only one --obvious way to do it.",
"Although that way may not be obvious at first unless you're Dutch.",
"Now is better than never.",
"Although never is often better than right now.",
"If the implementation is hard to explain, it's a bad idea.",
"If the implementation is easy to explain, it may be a good idea.",
"Namespaces are one honking great idea -- let's do more of those!"]

encoded_poem = [morse(line) for line in poem]

with open('data/morseCode.pkl', 'wb') as file:
    pickle.dump(encoded_poem, file)
```


```python

```
