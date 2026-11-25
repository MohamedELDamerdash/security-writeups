# JWT Attacks

Six PortSwigger labs on breaking JSON Web Token authentication: accepting unverified signatures, flawed signature verification, cracking a weak signing key, and header injection through jwk, jku and kid (including path traversal).

Tools: Burp Suite, PortSwigger Web Security Academy labs. Each lab below is documented with screenshots of the working exploit.

---

## Lab walkthroughs

**JWT Attacks – Definition for a Penetration Testing Report**

**JSON Web Token (JWT) is an open standard used for authentication and
secure information exchange between parties. However, several attacks
target JWT vulnerabilities, which can lead to security breaches if not
properly mitigated.**

**Types of JWT Attacks:**

1.  **Signature Manipulation – Occurs when weak or incorrect algorithms,
    such as none, are used, allowing an attacker to forge a token
    without a valid signature.**

2.  **Algorithm Confusion Attack – Exploits applications that accept
    tokens signed with unexpected algorithms due to improper
    validation.**

3.  **Secret Key Leakage – If the secret key is weak or exposed, an
    attacker can extract it and forge JWTs.**

4.  **Token Replay Attack – If mechanisms like jti (JWT ID) or exp
    (Expiration Time) are not implemented, an attacker can reuse a
    stolen JWT even after session termination.**

5.  **Brute Force Attack – When weak secret keys are used, attackers can
    attempt to crack JWT signatures through brute-force techniques.**

6.  **JWT Injection – Exploits vulnerabilities in JWT parsing to inject
    malicious code or modify payload data.**

**<span dir="rtl">  
</span>**

**Lab: JWT authentication bypass via unverified signature**

**Log in with a normal user
account(wiener:peter)**![Lab screenshot](image1.png)

**Open burp suite and capture login request**![Lab screenshot](image2.png)

**Send request to repeater and open the json web token**

![Lab screenshot](image3.png)

**Change sub to administrator**![Lab screenshot](image4.png)

**Send request and open the render , and here is show admin panel**
![Lab screenshot](image5.png)

**Forward request after change the JWT**![Lab screenshot](image6.png)

**Click on the admin panel**![Lab screenshot](image7.png)

**Here we can delete the carlos account**

![Lab screenshot](image8.png)

**Mitigation Strategies**

**Enforce Signature Verification:**

  - The application must always validate the JWT signature before
    processing the token.

**Lab: JWT authentication bypass via flawed signature verification**

**Log in with a normal user account(wiener:peter)**![Lab screenshot](image1.png)

**Open burp suite and capture login request**![Lab screenshot](image2.png)

**Send request to repeater and open the json web token**

![Lab screenshot](image3.png)

**Change sub to administrator and alg to none**

![Lab screenshot](image4.png)

**And delete the signature from JWT without dot ,and Send the request
and open the render , and here is show admin panel, and change the path
to /admin**

![Lab screenshot](image9.png)

**Forward request after change the JWT**

![Lab screenshot](image10.png)

**Here we can deleted the carlos account**

![Lab screenshot](image11.png)

**Mitigation Strategies**

**Enforce Signature Verification:**

  - The application must always validate the JWT signature before
    processing the token.

**Disallow the none Algorithm:**

  - **Implement strict validation to reject any token using the none
    algorithm or unexpected values.**

**Lab: JWT authentication bypass via weak signing key**

![Lab screenshot](image1.png)

![Lab screenshot](image12.png)

![Lab screenshot](image13.png)![Lab screenshot](image14.png)![Lab screenshot](image15.png)![Lab screenshot](image16.png)

![Lab screenshot](image17.png)![Lab screenshot](image18.png)

**Lab: JWT authentication bypass via jwk header injection**

![Lab screenshot](image19.png)![Lab screenshot](image20.png)![Lab screenshot](image18.png)

**Lab: JWT authentication bypass via jku header injection**

![Lab screenshot](image21.png)![Lab screenshot](image22.png)![Lab screenshot](image23.png)![Lab screenshot](image24.png)

**Lab: JWT authentication bypass via kid header path traversal**

![Lab screenshot](image25.png)![Lab screenshot](image26.png)![Lab screenshot](image27.png)![Lab screenshot](image28.png)![Lab screenshot](image29.png)
