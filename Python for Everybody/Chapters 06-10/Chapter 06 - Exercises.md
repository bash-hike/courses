## Assignment 6.5

### Write code using find() and string slicing (see section 6.10) to extract the number at the end of the line below. Convert the extracted value to a floating point number and print it out. 

###### *Desired Output*
````
0.8475  
````
## 

````python
text = "X-DSPAM-Confidence:    0.8475";
ind = text.find(":")
data = text[ind+1:]
num = float(data)
print(num)
````
###### *Your Output*
```
0.8475
```