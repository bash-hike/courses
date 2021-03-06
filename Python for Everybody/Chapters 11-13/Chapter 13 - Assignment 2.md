## Extracting Data from JSON

#### In this assignment you will write a Python program that will prompt for a URL, read the JSON data from that URL using **urllib** and then parse and extract the comment counts from the JOSN data, compute the sum of the numbers in the file and enter the sum.

### Data Files

We provide two files for this assignment. One is a sample file where we give you the name for your testing and the other is the actual data you need to process for the assignment

- Sample data: http://py4e-data.dr-chuck.net/comments_42.xml (Sum=2553)
    
- Actual data: http://py4e-data.dr-chuck.net/comments_850240.xml (Sum ends with 36)

You do not need to save these files to your folder since your program will read the data directly from the URL. **Note:** Each student will have a distinct data url for the assignment - so only use your own data url for analysis. 

### Data Format 

The data consists of a number of names and comment counts in XML as follows:

```json
{
  comments: [
    {
      name: "Matthias"
      count: 97
    },
    {
      name: "Geomer"
      count: 97
    }
    ...
  ]
}
```

The closest sample code that shows how to parse JSON and extract a list is [json2.py](https://www.py4e.com/code3/json2.py). You might also want to look at [geoxml.py](https://www.py4e.com/code3/geoxml.py) to see how to prompt for a URL and retrieve data from a URL.  

## 

### Turning in Assignment 

Enter the sum from the actual data and your Python code below:

Sum: *2636* (ends with 36)

Python Code:

```python
import urllib.request, urllib.parse, urllib.error
import json
import ssl

# Ignore SSL certificate errors
ctx = ssl.create_default_context()
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE

total = 0
url = input('Enter url: ')

uhandle = urllib.request.urlopen(url, context=ctx)
data = uhandle.read()
# Parse JSON from the data recieved
info = json.loads(data)
# Comments are stored in the key "comments"
comments = info["comments"]
for comment in comments:
    # Count is an integer
    total += comment["count"]

print("Sum:", total)
```