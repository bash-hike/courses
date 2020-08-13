##  Exploring the HyperText Transport Protocol 

#### In this assignment you write a Python program to retrieve a web page over a socket and display the headers from the web server.

You are to retrieve the following document using the HTTP protocol in a way that you can examine the HTTP Response headers. 

> http://data.pr4e.org/intro-short.txt

There are multiple ways that you might retrieve this web page and look at the response headers: 

- **Preferred:** Modify the [socket1.py](https://www.py4e.com/code3/socket1.py) program to retrieve the above URL and print out the headers and data. Make sure to **change** the code to retrieve the above URL - the values are different for each URL. 

- Open the URL in a web browser with a developer console or FireBug and manually examine the headers that are returned.

- Use terminal to connect to the *data.pr4e.org* server at port 80, and send a GET request to retrieve the webpage and headers.

## 

Enter the header values in each of the fields below.

```
telnet data.pr4e.org 80
Trying 192.241.136.170...
Connected to data.pr4e.org.
Escape character is '^]'.
GET http://data.pr4e.org/intro-short.txt HTTP/1.0

HTTP/1.1 200 OK
Date: Tue, 11 Aug 2020 19:25:43 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Sat, 13 May 2017 11:22:22 GMT
ETag: "1d3-54f6609240717"
Accept-Ranges: bytes
Content-Length: 467
Cache-Control: max-age=0, no-cache, no-store, must-revalidate
Pragma: no-cache
Expires: Wed, 11 Jan 1984 05:00:00 GMT
Connection: close
Content-Type: text/plain

Why should you learn to write programs?

Writing programs (or programming) is a very creative 
and rewarding activity.  You can write programs for 
many reasons, ranging from making your living to solving
a difficult data analysis problem to having fun to helping
someone else solve a problem.  This book assumes that 
everyone needs to know how to program, and that once 
you know how to program you will figure out what you want 
to do with your newfound skills.  
Connection closed by foreign host.
```

Last-Modified: *Mon, 10 Aug 2020 04:41:05 GMT*

ETag: *1d3-54f6609240717*

Content-Length: *467*

Cache-Control:*max-age=0, no-cache, no-store, must-revalidate*

Content-Type: *text/plain*