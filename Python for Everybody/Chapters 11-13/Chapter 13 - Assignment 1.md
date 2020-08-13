## Extracting Data from XML

#### In this assignment you will write a Python program that will prompt for a URL, read the XML data from that URL using **urllib** and then parse and extract the comment counts from the XML data, compute the sum of the numbers in the file and enter the sum.

### Data Files

We provide two files for this assignment. One is a sample file where we give you the name for your testing and the other is the actual data you need to process for the assignment

- Sample data: http://py4e-data.dr-chuck.net/comments_42.xml (Sum=2553)
    
- Actual data: http://py4e-data.dr-chuck.net/comments_850239.xml (Sum ends with 28)

You do not need to save these files to your folder since your program will read the data directly from the URL. **Note:** Each student will have a distinct data url for the assignment - so only use your own data url for analysis. 

### Data Format and Approach 

The data consists of a number of names and comment counts in XML as follows:

````xml
<comment>
  <name>Matthias</name>
  <count>97</count>
</comment>
````

You are to look through all the &lt;comment&gt; tags and find the &lt;count&gt; values sum the numbers. The closest sample code that shows how to parse XML is [geoxml.py](https://www.py4e.com/code3/geoxml.py). But since the nesting of the elements in our data is different than the data we are parsing in that sample code you will have to make real changes to the code.

To make the code a little simpler, you can use an XPath selector string to look through the entire tree of XML for any tag named 'count' with the following line of code:

```
counts = tree.findall('.//count')
```

Take a look at the Python ElementTree documentation and look for the supported XPath syntax for details. You could also work from the top of the XML down to the comments node and then loop through the child nodes of the comments node. 

## 

### Turning in Assignment 

Enter the sum from the actual data and your Python code below:

Sum: *2128* (ends with 28)

Python Code:

```python
import urllib.request, urllib.parse, urllib.error
import xml.etree.ElementTree as ET
import ssl

# Ignore SSL certificate errors
ctx = ssl.create_default_context()
ctx.check_hostname = False
ctx.verify_mode = ssl.CERT_NONE

total = 0
url = input('Enter url: ')

uhandle = urllib.request.urlopen(url, context=ctx)
data = uhandle.read()
# Parse XML from the data recieved
tree = ET.fromstring(data)
# Retrieve all the count tags
counts = tree.findall('.//count')
for count in counts:
    # Typecaste the text string to int, and add to the total
    total += int(count.text)

print("Sum:", total)
```