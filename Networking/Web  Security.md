
## Concepts
### Origin
https://test-website.com:443/some-path
|-----|-------------------|----|
Scheme  + Domain     +     Port = Origin

![[Pasted image 20240130104300.png]]


## Security Systems
Burp suite is a tool for penetration testing a website

#### Same-origin Policy (SoP)
Browser enforces a Same Origin Policy that restricts running any javascript not from the source website. This means that your browser will only allow running Javascript from its origin website. 

*In example*
*You visit _malicious.com_, which contains some JavaScript that tries to make a cross domain request to _mybank.com_. It should be up to _mybank.com_, not _malicious.com_, to decide whether or not it sets CORS headers that relax the same-origin policy, allowing the JavaScript from _malicious.com_ to interact with it. If _malicous.com_ could set its own CORS headers allowing its own JavaScript access to _mybank.com_, this would completely nullify the same-origin policy.*

#### CORS (Cross Origin Resource Sharing)

*What*?
Allows loosening the restrictions enforced by SoP by whitelisting websites. It is a whitelist for other web domains.

*Why?*
Occasionally websites might wish to make requests from other domains. 
Helps defend against:

## Security Exploits
- Cross-Site Scripting(XSS)
- Cross-Set Request Forgery(CSRF)

#### HTTP Parameter Pollution
[Google CTF Challenge](https://capturetheflag.withgoogle.com/beginners-quest)
Sending multiple copies of a parameter to a webserver can result in  many different patterns.
i.e. `curl -X POST website.com/signup -d "username=user&tier=GOLD&tier=BLUE`
This results in non deterministic behavior where the first or the last param might be sent

#### SQL Injection
Clients accessing input fields on your website can character escape the input and write raw SQL commands if the backend does not properly handle input fields.