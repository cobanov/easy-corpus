# easy-corpus

Prepare corpus for text embeddings or any particular NLP project easily.

## Requirements
```
nltk
```

### Stop Words 

```python
import nltk
nltk.download('stopwords')
```
For the command line

`python -m nltk.downloader stopwords`

## Code
```python
import re
from nltk.corpus import stopwords


stop_words = set(stopwords.words('english'))

def read_file(filename):
    """
    Reads a file and returns the text
    
    :param filename: the name of the file to be read
    :return: A string object.
    """
    with open(filename, 'r') as f:
        text = f.read()
    return text

def clean_text(text):
    """
    The function takes in a string of text and does four things:
    
    1. Removes punctuation
    2. Removes stopwords
    3. Splits the string into a list of words
    4. Joins the list of words back into a single string
    
    :param text: The text to be cleaned
    :return: A list of words.
    """
    text = re.sub(r'[^\w\s]', '', text)
    text = re.sub(r'\s+', ' ', text)
    text = re.sub(r'[0-9]+.', ' ', text) # This one is optional for specific cases
    text = text.lower()
    text = text.split()
    text = [w for w in text if not w in stop_words]
    text = ' '.join(text)
    return text

def write_file(filename, text):
    """
    Write a file with the given filename and text
    
    :param filename: the name of the file to write to
    :param text: The text to be written to the file
    """
    with open(filename, 'w') as f:
        f.write(text)

def count_words(text):
    """
    Counts the number of words in a text
    
    :param text: The text you want to count the words in
    :return: The number of words in the text.
    """
    text = text.split()
    return len(text)

def main():
    text = read_file('./data/text.txt')
    cleaned_text = clean_text(text)
    write_file('./data/clean_text.txt', cleaned_text)
    print('Word count:', count_words(cleaned_text))

if __name__ == '__main__':
    main()
    
```
