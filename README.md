

```python
import numpy as np

```

# Playfair Cypher

In this notebook, the encoding and decoding techniques of the Playfair Cypher will be utilized to implement it. The end result of this notebook should be a set of functions that can encode and decode messages with a given key under the Playfair Cypher. 


```python
def remove_spaces(str):
    ### This is a function that will remove all of the spaces from a string. 
    return str.replace(' ', '')
```


```python
def remove_spaces_tests():
    ### This is a small number of tests to ensure that the removing of spaces works properly
    assert(remove_spaces(" ") == "")
    assert(remove_spaces("test test") == "testtest")
    assert(remove_spaces("test test test") == "testtesttest")
    assert(remove_spaces(" test ") == "test")
    
    print("All Tests Passed!")
    
    
remove_spaces_tests()
```

    All Tests Passed!


Since spaces aren't relevent to the cyper, we should remove them from the input. The above code is doing this, along with some tests. The Playfair Cyper also only works in pairs, meaning that if the length of a given string is odd, the Playfair Cypher mandates that we add an 'X' to it, in order for the cyper to work. In order to do this, we will introduce a variable called "is_odd". If this variable is true, we will add an "x" to the end of the string and remove the last letter of the deciphered test or vice versa. 


```python

is_odd = False
def check_length(str):
    global is_odd
    is_odd = (len(str) == 1)

```




    True


