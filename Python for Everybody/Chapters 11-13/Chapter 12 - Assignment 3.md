## Following Links in HTML Using BeautifulSoup

#### In this assignment you will write a Python program using **urllib** to read the HTML from the data files below, extract the href= values from the anchor tags, scan for a tag that is in a particular position from the top and follow that link, repeat the process a number of times, and report the last name you find.

### Data Files

We provide two files for this assignment. One is a sample file where we give you the name for your testing and the other is the actual data you need to process for the assignment

- Sample problem: Start at http://py4e-data.dr-chuck.net/known_by_Fikret.html

    Find the link at position **3** (the first name is 1). Follow that link. Repeat this process **4** times. The answer is the last name that you retrieve.
    
    Sequence of names: Fikret Montgomery Mhairade Butchi Anayah
    
    Last name in sequence: Anayah

- Actual problem: Start at: http://py4e-data.dr-chuck.net/known_by_Vikki.html
    
    Find the link at position **18** (the first name is 1). Follow that link. Repeat this process **7** times. The answer is the last name that you retrieve.
    
    Hint: The first character of the name of the last page that you will load is: D

### Strategy

The web pages tweak the height between the links and hide the page after a few seconds to make it difficult for you to do the assignment without writing a Python program. But frankly with a little effort and patience you can overcome these attempts to make it a little harder to complete the assignment without writing a Python program. But that is not the point. The point is to write a clever Python program to solve the program. 

### Sample Execution

```
$ python3 solution.py
Enter URL: http://py4e-data.dr-chuck.net/known_by_Fikret.html
Enter count: 4
Enter position: 3
Retrieving: http://py4e-data.dr-chuck.net/known_by_Fikret.html
Retrieving: http://py4e-data.dr-chuck.net/known_by_Montgomery.html
Retrieving: http://py4e-data.dr-chuck.net/known_by_Mhairade.html
Retrieving: http://py4e-data.dr-chuck.net/known_by_Butchi.html
Retrieving: http://py4e-data.dr-chuck.net/known_by_Anayah.html
```

The answer to the assignment for this execution is "Anayah". 

## 

### Turning in Assignment 

Enter the last name retrieved and your Python code below:

Name: *Darah* (name starts with D)

Python Code:

```python
# To run this, download the BeautifulSoup zip file
# http://www.py4e.com/code3/bs4.zip
# and unzip it in the same directory as this file

import urllib.request, urllib.parse, urllib.error
from bs4 import BeautifulSoup
import ssl

# Ignore SSL certificate errors
ctx = ssl.create_default_context()
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE

url = input('Enter - ')
count = int(input('Enter count - '))
# Subtract one from position to get index position
pos = int(input('Enter position - '))-1

def getName(url, count, pos):
    # print('Retrieving:', url)
    html = urllib.request.urlopen(url, context=ctx).read()
    soup = BeautifulSoup(html, 'html.parser')
    # Retrieve all of the anchor tags
    tags = soup('a')
    # Retrieve the next name
    next = tags[pos]
    # if count is 1, next name is the answer
    if count == 1 : return next.text
    # if count is not 1, go to the next link
    nextURL = next.get('href', None)
    return getName(nextURL, count-1, pos)

print("Answer:", getName(url, count, pos))
```