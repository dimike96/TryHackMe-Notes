# THM - HTTP in Detail

[TryHackMe | HTTP in Detail](https://tryhackme.com/room/httpindetail)

> Michael Jack | 06/2022

---

## Task 1 - What is HTTP(S)?

**HTTP** (Hypertext transfer protocol) and **HTTPS** (Hypertext transfer protocol secure) are the network protocols used whenever you view a website.

HTTP was developed by Tim Berners-Lee and his team between 1989-1991 and provides rules for communicating with web servers for transmitting data.

HTTPS is a secure version of that that adds encryption to the process so that data isn't snooped upon as well as making it easier to validate that you are connecting and communicating with the servers you think you are.

### Questions

> What does HTTP stand for?

```
Hypertext transfer protocol
```

> What does the S in HTTPS stand for?

```
Secure
```

> On the mock webpage on the right there is an issue, once you've found it, click on it. What is the challenge flag?

```
THM{INVALID_HTTP_CERT}
```

---

## Task 2 - Requests and Responses

When using the internet our computer's browser (the client) will make requests to a web server to retieve the content of the webpage.

There needs to be a standardized way of communicated how to get these resources and this is what the **URL** is for.

### What is a URL? (Uniform Resource Locator)

> A URL is predominantly an instruction on how to access a resource on the internet.

Example URL with all features:

```
https://user:password@tryhackme.com:80/view-room?id=1#task3
```

### URL Features

- Scheme
	- This defines the protocol to be used
	- HTTP, HTTPS, FTP, etc.
	- ```https://```
- User
	- Sometimes services require authentication and this can be passed through the URL
	- ```user:password
- Host
	- Domain name or IP address of the server to be accessed
	- ```tryhackme.com```
- Port
	- What port to connect to on the host (where the desired service is running)
	- Usually 80 for HTTP and 443 for HTTPS, but anything 1-65535
	- ```:80```
- Path
	- Filename or location of resource to be accessed
	- ```/view-room```
- Query String
	- Information being sent to the desired path
	- ```?id=1```
- Fragment
	- Reference to location on page that is requested
	- Usually to direct to a specific part of a page with lots of content
	- ```#task3```

### Making a Request

> It's possible to make a request to a web server with just one line "**GET / HTTP/1.1**"

To get more out of the internet though we send more data in what are called *headers*.

**Example request**:

```
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

**Line 1:** This request is sending the GET method ( more on this in the HTTP Methods task ), request the home page with / and telling the web server we are using HTTP protocol version 1.1.

**Line 2:** We tell the web server we want the website tryhackme.com  

**Line 3:** We tell the web server we are using the Firefox version 87 Browser  

**Line 4:** We are telling the web server that the web page that referred us to this one is [https://tryhackme.com](https://tryhackme.com)

**Line 5:** HTTP requests always end with a blank line to inform the web server that the request has finished.

**Example Response**:

```HTML

HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>

```

**Line 1:** HTTP 1.1 is the version of the HTTP protocol the server is using and then followed by the HTTP Status Code in this case "200 Ok" which tells us the request has completed successfully.  

**Line 2:** This tells us the web server software and version number.  

**Line 3:** The current date, time and timezone of the web server.

**Line 4:** The Content-Type header tells the client what sort of information is going to be sent, such as HTML, images, videos, pdf, XML.  

**Line 5:** Content-Length tells the client how long the response is, this way we can confirm no data is missing.  

**Line 6:** HTTP response contains a blank line to confirm the end of the HTTP response.  

**Lines 7-14:** The information that has been requested, in this instance the homepage.

### Questions

> What HTTP protocol is being used in the above example?

```
http/1.1
```

> What response header tells the browser how much data to expect?

```
Content-Length
```

---

## Task 3 - HTTP Methods

HTTP methods are the actions a client wants to perform on or with a server.

### Common HTTP Request Methods

- GET
	- Used to get information from a web server
- POST
	- Submitting data to a web server
- PUT
	- Submitting data, to update information on a web server
- DELETE
	- Deleting information or records from a web server

### Questions

> What method would be used to create a new user account?

```
POST
```

> What method would be used to update your email address?

```
PUT
```

> What method would be used to remove a picture you've uploaded to your account?

```
DELETE
```

> What method would be used to view a news article?

```
GET
```

---

## Task 4 - HTTP Status Codes

When an HTTP server responds the first line always contains the **response code**, informing the client the outcome of their request.

### Response Code Ranges

- 100-199 : **Information Responmse**
	- These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are no longer very common.
- 200-299 : **Success**
	- Indicates the request was successful
- 300-399 : **Redirection**
	- Redirects a clients request to another resource. Could be different page or domain all together.
- 400-499 : **Client Errors**
	- Indicates ther was an error with the request
- 500-599 : **Server Errors**
	- Indicates an error server-side and usually indicate a severe problem with the server handling the request.

### Common Status Codes:

- 200 - **OK**
	- Request was completed successfully
- 201 - **Created**
	- A resource was created
- 301 - **Permanent Redirect**
	-  This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead.
- 302 - **Temporary Redirect**
	- Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future.
- 400 - **Bad Request**
	- This tells the browser that something was either wrong or missing in their request. This could sometimes be used if the web server resource that is being requested expected a certain parameter that the client didn't send.
- 401 - **Not Authorized**
	- You are not currently allowed to view this resource until you have authorised with the web application, most commonly with a username and password.
- 403 - **Forbidden**
	- You do not have permission to view this resource whether you are logged in or not.
- 404 - **Page Not Found**
	- The page/resource you requested does not exist.
- 405 - **Method Not Allowed**
	- The resource does not allow this method request, for example, you send a GET request to the resource /create-account when it was expecting a POST request instead.
- 500 - **Internal Service Error**
	- The server has encountered some kind of error with your request that it doesn't know how to handle properly.
- 503 - **Service Unavailable**
	- This server cannot handle your request as it's either overloaded or down for maintenance.

### Questions

> What response code might you receive if you've created a new user or blog post article?

```
201
```

> What response code might you receive if you've tried to access a page that doesn't exist?

```
404
```

> What response code might you receive if the web server cannot access its database and the application crashes?

```
503
```

> What response code might you receive if you try to edit your profile without logging in first?

```
401
```

---

## Task 5 - Headers

> Headers are additional bits of data you can send to the web server when making requests.

### Common Request Headers

- Host
	- If some web server hosts multiple sites this can tell the service which the client wants
- User-Agent
	- This is the clients browser and version so the server can respond in a way that browser can work with and is formatted properly
- Content-Length
	- Tells the server how much data to expect in a request when filling a form or something so that I knows if data is lost or missing.
- Accept-Encoding
	-  Tells the serve what compression methods the client supports 

### Common Response Headers

- Set-Cookie
	- Information to store and send to the server on each request
- Cache-Control
	- How long to store the contents of the response in the clients cache before it requests it again
- Content-Type
	- Indicates to the client what type of data the server is returning whether it be HTML, CSS, JavaScript, a picture, or whatever else.
- Content-Encoding
	- Indicates how the content ha been compressed to the client can parse it

### Questions

> What header tells the web server what browser is being used?

```
User-Agent
```

> What header tells the browser what type of data is being returned?

```
Content-Type
```

> What header tells the web server which website is being requested?

```
Host
```

---

## Task 6 - Cookies

Cookies are small pieces of data that are stored on your computer when you recieve a "Set-Cookie" header from a web server. 

Every subsequent will send the cookie back to the server.

HTTP is stateless so this is how web servers remember who you are.

> Cookies can be used for many purposes but are most commonly used for website authentication. 
> The cookie value won't usually be a clear-text string where you can see the password, but a token (unique secret code that isn't easily humanly guessable).

We can view cookies in the developer tools of our browser in the cookies tab!

### Questions

> Which header is used to save cookies to your computer?

```
Set-Cookie
```

---

## Task 7 - Making Requests

Using what you've learnt from the above tasks you can use the web emulator to complete the below questions.

### Questions

> Make a GET request to /room

```
THM{YOU'RE_IN_THE_ROOM}
```

> Make a GET request to /blog and using the gear icon set the id parameter to 1 in the URL field

```
THM{YOU_FOUND_THE_BLOG}
```

> Make a DELETE request to /user/1

```
THM{USER_IS_DELETED}
```

> Make a PUT request to /user/2 with the username parameter set to admin

```
THM{USER_HAS_UPDATED}
```

> POST the username of thm and a password of letmein to /login

```
THM{HTTP_REQUEST_MASTER}
```

---
