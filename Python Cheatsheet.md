# Python

## STRINGS

my_string = 'cow'

### SPECIFIC INDEX

```
my_string[0] => 'c'
```

### EACH CHARACTER

```
for x in my_string:
    print x
```

### SLICING

```
my_string[0:2] => 'co'
my_string[:-1] (everything but last) => 'co'
my_string[-1:] (last character) => 'w'
```

### STRIP (REMOVE WHITE SPACES FROM BEGINNING AND END)

```
my_string.strip()
```

### REPLACE A CHARACTER

```
my_string.replace('c', 'abc') => 'abcow'
```

### SPLIT

```
my_string.split('o') => ['c', 'w']
```

### EXISTS
```
'co' in my_string => True
```

### CONCAT
```
my_string + 'boy' => 'cowboy'
```

### FIND INDEX OF SUBSTRING
```
my_string.find('o') => 1
for c in "test"
    print c
```

## FOR LOOPs

nums = [1, 2, 3]

### JUST THE ITEM
```
for item in nums:
    print item
```

### JUST THE INDEX (JAVA WAY)
```
for index in range(len(nums)):
    print nums[index]
```

### BOTH INDEX AND ITEM
```
for index, item in enumerate(nums):
    print index, item
```

### DICTS

my_dict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

## GET
```
my_dict.get('brand')
```

## SET
```
my_dict['name'] = 'nuts'
```

## KEYS
```
my_dict.keys()
```

## VALUES
```
my_dict.values()
```

## LOOP
```
for key, value in my_dict.items():
    print key, value
```

## EXIST
```
'brand' in my_dict => True
'test' in my_dict => False
```

## LENGTH
```
len(my_dict)
```

## CLEAR
```
my_dict.clear()
```

## SETS
```
my_set = set()
```

### ADD
```
my_set.add('orange')
```

### REMOVE
```
my_set.remove('orange')
```

### LENGTH
```
len(my_set)
```

### EXIST
```
'test' in my_set
```

## TUPLES

my_tuple = ('apple', 'orange')
- ordered
- immutable

## OPERATORS

IDENTITY OPERATOR: is, is not

MEMBERSHIP OPERATORS: in, not in

BITWISE OPERATORS: and, or, not, xor

## CLASSES

```
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def public_function():
        ...
    def _private_function():
        ...
```

```
p1 = Person("John", 36)
p1.public_function()
```

### INSTANCE, CLASS, STATIC

INSTANCE:
```
    def method(self):
        return 'instance method called', self
```

CLASS:
```
    @classmethod
    def classmethod(cls):
        return 'class method called', cls
```

STATIC:
```
    @staticmethod
    def staticmethod():
        return 'static method called'
```

## REQUESTS

import requests

GET
```
    response = requests.get('https://api.github.com', params={}, headers={})
    response.status_code => '200', '404'
    response.text => raw str of everything...
    response.json => json as a dict
    response.headers['content-type'] => 'application/json'
```

POST
```
    response = requests.post('https://httpbin.org/post', data={'key':'value'})
```

## JSON

import json

### Convert JSON to dict:

some JSON:

`x =  '{ "name":"John", "age":30, "city":"New York"}'`

parse x:

`y = json.loads(x)`

the result is a Python dictionary:

`print y["age"]`

### Convert object (dict) to JSON:

a Python object (dict, list, type, string, int, and more)

`x = {"name": "John", "age": 30, "city": "New York"}`

convert into JSON:

`y = json.dumps(x)`

the result is a JSON string:

`print y`

## OTHER

`max_num = float('inf')`

`min_num = float('-inf')`