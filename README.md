# week7-research-hassanelnajjar

## Research topics

### HTTP vs HTTPS
+ How does HTTPS work? What are TLS/SSL certificates?

#### TLS
> Transport Layer Security is a protocol that establishes an encrypted session between two computers on the Internet. It verifies the identity of the server and prevents hackers 
from intercepting any data.
#### SSL
> SSL is the Secure Socket Layer protocol which is responsible for creating secure communication between client and server. This is done by both server and client authentication and the negotiation of an encryption algorithm and cryptographic keys.


#### What does TLS do?
> There are three main components to what the TLS protocol accomplishes: Encryption, Authentication, and Integrity.

> - Encryption: hides the data being transferred from third parties.
> - Authentication: ensures that the parties exchanging information are who they claim to be.
> - Integrity: verifies that the data has not been forged or tampered with.

#### How does HTTPS work
> HTTPS is an implementation of TLS encryption on top of the HTTP protocol, which is used by all websites as well as some other web services. Any website that uses HTTPS is therefore employing TLS encryption..




#### TLS/SSL Certificate
>  Digital certificates, also known as identity certificates or public key certificates, are digital files that are used to certify the ownership of a public key. TLS certificates are a type of digital certificate, issued by a Certificate Authority (CA). The CA signs the certificate, certifying that they have verified that it belongs to the owners of the domain name which is the subject of the certificate.

> TLS/SSL Certificates are domain-specific. When renaming the main domain please be aware that the SSL Certificate for the old main domain will not work after the rename process. The new main domain name will require a new SSL Certificate.

+ Why is this important to implement in your projects?

>  TLS helps provide an enhanced layer of protection by encrypting the otherwise readable data, making it difficult for hackers to obtain private information.


+ Demo how to generate certificates and use them in a node project  

>  - A TLS certificate is issued by a certificate authority to the person or business that owns a domain. The certificate contains important information about who owns the domain, along with the server's public key, both of which are important for validating the server's identity.
#### Certificate Types :-
> - Self-Signed Certificate : Such a certificate also won't be trusted by browsers. And you would need to ask all users to add that certificate in a trusted list in your browser's settings. It might work only for internal users

> - Generate a Certificate Signed by a Certificate Authority

#### How To Create one :-
- You need to log in into your ssl provides and do these :-
- Generate a private key (key.pem)
- Create the Certificate Signing Request (cert.pem)
- assign that keys to server using http.createServer()
```js
// we will pass our 'app' to 'https' server
https.createServer({
    key: fs.readFileSync('./key.pem'),
    cert: fs.readFileSync('./cert.pem'),
    passphrase: 'YOUR PASSPHRASE HERE'
}, app)
.listen(3000);
```

### Stateless vs stateful authentication
+ What is session based authentication (stateful) vs token based authentication (stateless)?

> - Stateful: You can revoke the authentication session on the IdP anytime.
> - Stateless: The session expiration time is set when the authentication token is released. You cannot revoke the session on the IdP.
#### Stateful session 
> - Stateful session is created on the backend side, and the corespondent session reference Id is sent to the client. Each time the client makes a request to the server, the server locates the session memory using the reference Id from the client and finds the authentication information.

#### Stateless sessions
> - Stateless authentication is used to solve the disadvantages of stateful authentication. They are quite different and are used in different scenarios.


+ Draw flow diagrams to show the steps involved in each process
#### Stateful session diagrams
![Stateful session diagrams](https://miro.medium.com/max/579/1*B6NRLiXwOn64YSnfpKuQjw.png)


#### Stateless session diagrams
![Stateless session diagrams](https://miro.medium.com/max/577/1*bPI6orOxLsgz4Ue18dxmFw.png)

+ What are the advantages and disadvantages of each?

#### Stateful session 
> Advantages
- Revoke the session anytime
- Easy to implement and manage for one-session-sever scenario
- Session data can be changed later (assume that for a one-session-sever, no inconsistent problem)

> Disadvantages
- Increasing server overhead: As the number of logged-in users increases, the more server resources are occupied.
- Fail to scale: If the sessions are distributed in different servers, we need to implement a tracking algorithm to link a specific user session and the specific session sever. 
- Difficult for 3rd party applications to use your credentials

#### Stateless session 
> Advantages
- Lower server overhead
- Easy to scale
- Good to integrate with 3rd party application
> Disadvantages
- Cannot revoke the session anytime
- Relatively complex to implement for one-session-server scenario
- Session data cannot be changed until its expiration time

#### Improved stateless authentication: sliding session
- Assign clients the permission (send the clients a unique refresh token) to request an extension lifetime of session data.
- Set the expiration time of user data to 24 hours (instead of one month).
- Each time the session data is expired, the client issues a request (attached with a valid refresh token) to the server to renew the session data.

> With this improvement, we can have the scalability and performance advantages of stateless authentication. Though we still cannot revoke the session data immediately, while we can forbid its lifetime extension by revoking the refresh token.


### Session-management in Express
+ What are sessions?
> A session can be defined as a server-side storage of information that is desired to persist throughout the user's interaction with the web site or web application. 


+ What are the different ways of managing sessions in express?

- [express-session](https://github.com/expressjs/session)
- [client-sessions](https://www.npmjs.com/package/cookie-session)
- [cookie session](https://github.com/mozilla/node-client-sessions)

+ Create a minimal example of how to set up a session (FYI: pseudo code is
  fine)
```js
- npm i express-session
- define sessionOptions {secret,saveUninitialized,cookie}
- app.use(express-session(sessionOptions))
- using req.session in adding variables and data as you want
- the server will use connected.sid from cookies "internally"
```
### Attacks
+ What are the following types of attack and How can you defend against each of them?
  + Man In The Middle (MITM)
> - A man in the middle (MITM) attack is a general term for when a perpetrator positions himself in a conversation between a user and an application—either to eavesdrop or to impersonate one of the parties, making it appear as if a normal exchange of information is underway.

> - The goal of an attack is to steal personal information, such as login credentials, account details and credit card numbers. Targets are typically the users of financial applications, SaaS businesses, e-commerce sites and other websites where logging in is required.

![Man In The Middle (MITM) attack image](https://www.imperva.com/learn/wp-content/uploads/sites/13/2017/09/man-in-the-middle-mitm-attack.png)

#### 7 types of man-in-the-middle attacks
- IP spoofing
- DNS spoofing
- HTTPS spoofing
- SSL hijacking
- Email hijacking
- Wi-Fi eavesdropping
- Stealing browser cookies

#### Avoid MITM Attack :-
- Avoiding WiFi connections that aren’t password protected.
- Paying attention to browser notifications reporting a website as being unsecured.
- Immediately logging out of a secure application when it’s not in use.
- Not using public networks (e.g., coffee shops, hotels) when conducting sensitive transactions.

- For website operators, secure communication protocols, including TLS and HTTPS and use SSL/TLS to secure every page of their site and not just the pages that require users to log in

  + Cross Site Scripting (XSS)
> Cross-site Scripting (XSS) is a client-side code injection attack.

> Cross-site scripting (also known as XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. It allows an attacker to circumvent the same origin policy, which is designed to segregate different websites from each other. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might be able to gain full control over all of the application's functionality and data.

> The attacker aims to execute malicious scripts in a web browser of the victim by including malicious code in a legitimate web page or web application

#### Cross Site Scripting descriptive images:-

![Cross Site Scripting image](https://www.acunetix.com/wp-content/uploads/2012/10/how-xss-works-910x404.png)


![Cross Site Scripting image](https://portswigger.net/web-security/images/cross-site-scripting.svg)

#### Cross Site Scripting Types
- **Reflected XSS** : where the malicious script comes from the current HTTP request.
- **Stored XSS** : where the malicious script comes from the website's database.
- **DOM-based XSS** : where the vulnerability exists in client-side code rather than server-side code.

#### How to prevent XSS attacks

- **Filter input on arrival** : At the point where user input is received, filter as strictly as possible based on what is expected or valid input.
- **Encode data on output** : At the point where user-controllable data is output in HTTP responses, encode the output to prevent it from being interpreted as active content. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
- **Use appropriate response headers**: To prevent XSS in HTTP responses that aren't intended to contain any HTML or JavaScript, you can use the Content-Type and X-Content-Type-Options headers to ensure that browsers interpret the responses in the way you intend.
- **Content Security Policy**: As a last line of defense, you can use Content Security Policy (CSP) to reduce the severity of any XSS vulnerabilities that still occur.
  + Cross Site Request Forgery (CSRF)

> **Cross-Site Request Forgery (CSRF)** is an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker’s choosing. If the victim is a normal user, a successful CSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, CSRF can compromise the entire web application.
#### Cross-Site Request Forgery (CSRF) image:-
![Cross-Site Request Forgery (CSRF) image](https://portswigger.net/web-security/images/cross-site%20request%20forgery.svg)

![Cross-Site Request Forgery (CSRF) image](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/csrf-cross-site-request-forgery.png)

#### Best practices to avoid CSRF:

- Logging off web applications when not in use
- Securing usernames and passwords
- Not allowing browsers to remember passwords
- Avoiding simultaneously browsing while logged into an application

> For web applications, multiple solutions exist to block malicious traffic and prevent attacks. Among the most common mitigation methods is to generate unique random tokens for every session request or ID. These are subsequently checked and verified by the server. Session requests having either duplicate tokens or missing values are blocked. Alternatively, a request that doesn’t match its session ID token is prevented from reaching an application.

> Double submission of cookies is another well-known method to block CSRF. Similar to using unique tokens, random tokens are assigned to both a cookie and a request parameter. The server then verifies that the tokens match before granting access to the application.

> While effective, tokens can be exposed at a number of points, including in browser history, HTTP log files, network appliances logging the first line of an HTTP request and referrer headers, if the protected site links to an external URL. These potential weak spots make tokens a less than full-proof solution.


#### Explain CSRF Token 

> To defeat a CSRF attack, applications need a way to determine if the HTTP request is legitimately generated via the application’s user interface. The best way to achieve this is through a CSRF token. A CSRF token is a secure random token (e.g., synchronizer token or challenge token) that is used to prevent CSRF attacks. The token needs to be unique per user session and should be of large random value to make it difficult to guess.

> A CSRF secure application assigns a unique CSRF token for every user session. These tokens are inserted within hidden parameters of HTML forms related to critical server-side operations. They are then sent to client browsers.

> It is the application team’s responsibility to identify which server-side operations are sensitive in nature. The CSRF tokens must be a part of the HTML form—not stored in session cookies. The easiest way to add a non-predictable parameter is to use a secure hash function (e.g., SHA-2) to hash the user’s session ID. To ensure randomness, the tokens must be generated by a cryptographically secure random number generator.

> Whenever a user invokes these critical operations, a request generated by the browser must include the associated CSRF token. This will be used by the application server to verify the legitimacy of the end-user request. The application server rejects the request if the CSRF token fails to match the test.

#### [How to set CSRF Token at express !](https://levelup.gitconnected.com/how-to-implement-csrf-tokens-in-express-f867c9e95af0)