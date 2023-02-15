# What is CORS?

CORS stands for "_Cross-Origin Resource Sharing_". In simpler terms, it's a mechanism that allows web browsers to make requests to resources on different domains.

For example, let's say you're browsing a website at _`example.com`_, and that website tries to load an image from a different domain, _`images.com`_. Without CORS, the web browser would block that request because it would be considered a security risk - [an attacker could potentially use that request to steal data from the user](#how-an-attacker-could-potentially-use-that-request-to-steal-data-from-the-user)

To allow the request to go through, images.com needs to explicitly tell the web browser that it's okay to make that request. It does this by including a special HTTP header in its response to the browser, called the "Access-Control-Allow-Origin" header. This header tells the browser which domains are allowed to make requests to images.com. If example.com is on the list of allowed domains, the browser will allow the request to go through and load the image.

In summary, CORS is a security mechanism that controls which domains are allowed to make requests to resources on other domains. It's an important security feature of the web, and it helps to prevent attacks that could steal sensitive user data.

## How an attacker could potentially use that request to steal data from the user?

An attacker could potentially use a cross-origin request to steal data from a user in a few ways. One common attack is called a cross-site request forgery (CSRF) attack. Here's an example of how a CSRF attack could work:

Let's say that the user is logged into their bank's website in one tab of their web browser, and they're also browsing a malicious website in another tab. The malicious website contains some HTML and JavaScript code that, when executed in the user's browser, sends a request to the bank's website to transfer money out of the user's account.

Normally, the bank's website wouldn't allow this request because it's coming from a different domain (the malicious website) than the one the user is logged into. However, if the bank's website doesn't properly implement CORS, it might allow the request to go through, thinking that it's coming from the user's own browser.

So, when the user visits the malicious website and the code is executed, it sends the request to the bank's website and transfers the money out of the user's account, all without the user's knowledge or consent.

This is just one example of how an attacker could use a cross-origin request to steal data or perform other malicious actions. That's why it's important to properly implement CORS to prevent these kinds of attacks.

## Technical Overview

When a web page makes a cross-origin request, the web browser will first send a "preflight" request to the server to check if the server allows the actual request. The preflight request uses the HTTP OPTIONS method, and includes a special "Access-Control-Request-Method" header that specifies the actual method of the request (e.g., GET, POST, PUT, DELETE).

The server can then respond with a set of CORS headers that indicate whether the actual request is allowed or not. Here are some of the most important CORS headers:

Access-Control-Allow-Origin: This header specifies which origins are allowed to make requests to the server. The value can be a single origin (e.g., "http://example.com"), or the wildcard "*" to allow any origin. For example, if a server includes the header "Access-Control-Allow-Origin: http://example.com", then only requests from that domain will be allowed to access the server's resources.

Access-Control-Allow-Methods: This header specifies which HTTP methods are allowed for the actual request. For example, if a server includes the header "Access-Control-Allow-Methods: GET, POST, PUT, DELETE", then only those methods will be allowed for the actual request.

Access-Control-Allow-Headers: This header specifies which headers are allowed for the actual request. This can be useful if the request includes custom headers that are not part of the standard HTTP headers.

Here's an example of how a server might respond to a preflight request:

```html
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: http://example.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Allow-Headers: Authorization, Content-Type
```
This response indicates that requests from http://example.com are allowed, and that the GET, POST, PUT, and DELETE methods are allowed for the actual request. It also allows the "Authorization" and "Content-Type" headers for the actual request.

In summary, CORS is a mechanism that allows web browsers to make cross-origin requests in a secure way. By using preflight requests and a set of HTTP headers, servers can control which origins are allowed to access their resources, which HTTP methods are allowed, and which headers are allowed. This helps to prevent attacks that could steal sensitive user data or perform other malicious actions.
