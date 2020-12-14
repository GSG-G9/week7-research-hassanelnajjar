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
+ What are the following types of attack?
  + Man In The Middle (MITM)
  + Cross Site Scripting (XSS)
  + Cross Site Request Forgery (CSRF)
+ How can you defend against each of them?
