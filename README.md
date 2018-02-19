

```python
import numpy as np
import string
from collections import OrderedDict
```

# Playfair Cypher

In this notebook, the encoding and decoding techniques of the Playfair Cypher will be utilized to implement it. The end result of this notebook should be a set of functions that can encode and decode messages with a given key under the Playfair Cypher. 


```python
def remove_spaces(str):
    ### This is a function that will remove all of the spaces from a string. 
    return str.replace(' ', '').lower()
```


```python
def remove_spaces_tests():
    ### This is a small number of tests to ensure that the removing of spaces works properly
    assert(remove_spaces(" ") == "")
    assert(remove_spaces("test test") == "testtest")
    assert(remove_spaces("test test test") == "testtesttest")
    assert(remove_spaces(" test ") == "test")
    assert(remove_spaces(" A B c D") == "abcd")
    
    print("All Tests Passed!")
    
    
remove_spaces_tests()
```

    All Tests Passed!


Since spaces aren't relevent to the cyper, we should remove them from the input. The above code is doing this, along with some tests. The Playfair Cyper also only works in pairs, meaning that if the length of a given string is odd, the Playfair Cypher mandates that we add an 'X' to it, in order for the cyper to work. In order to do this, we will introduce a variable called "is_odd". If this variable is true, we will add an "x" to the end of the string and remove the last letter of the deciphered test or vice versa. 


```python
is_odd = False
def check_length(str):
    global is_odd
    is_odd = (len(str) % 2 == 1)
    if is_odd:
        return str + 'x'
    return str
```


```python
def check_length_test():
    global is_odd
    assert(is_odd == False)
    assert(check_length("j") == "jx")
    assert(is_odd == True)
    is_odd = False
    assert(check_length("test") == "test")
    assert(is_odd == False)
    test_str = check_length(remove_spaces("t e s t 1 2 3"))
    assert(test_str == "test123x")
    assert(is_odd == True)
    print("All Tests Passed!")
    
check_length_test()
```

    All Tests Passed!


The key also needs to not have repeats, so let's implement a function that removes the repeats from a string. 


```python
def remove_repeats(str):
    str = str.replace("j", "i")
    return "".join(OrderedDict.fromkeys(str))
```


```python
def remove_repeats_test():
    assert(remove_repeats("test") == "tes")
    print("All Tests Passed!")
remove_repeats_test()
```

    All Tests Passed!


Now that all of our preprocessing tools have been implemented, it's time to begin implementing the encrypt function. Before that, however, it's necessary to set up our key. I'll implement this as a dictionary for both speed and ease of use. 


```python
key_array = []
def define_key(key):
    key = remove_repeats(remove_spaces(key))
    global key_array
    key_array = list(key)
    
    for i in list(string.ascii_lowercase):
        if i not in key and i != ('j'):
            key_array += i
        
        
    return key_array
```


```python
def define_key_tests():
    test1 = define_key(" te s s t a")
    assert(len(test1) == 25)
    test2 = define_key("a b c d e f g h i j k l m n o p q r s t u v")
    assert(len(test2) == 25)
    print("All Tests Passed!")
define_key_tests()
```

    All Tests Passed!

