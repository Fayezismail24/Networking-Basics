# 🔒 Deep Dive: Burp Suite Full Documentation

Burp Suite is an integrated platform for performing security testing of web applications.  
It provides tools for intercepting, modifying, replaying, and automating HTTP(S) traffic.

This document explores **every major component in detail**, including concepts, use cases, workflows, and real examples.

---

## 📋 Table of Contents

- [Introduction](#introduction)
- [Architecture Overview](#architecture-overview)
- [Burp Suite Tabs](#burp-suite-tabs)
  - [1. Target](#1-target)
  - [2. Proxy](#2-proxy)
  - [3. Spider / Crawler](#3-spider--crawler)
  - [4. Scanner](#4-scanner)
  - [5. Intruder](#5-intruder)
  - [6. Repeater](#6-repeater)
  - [7. Sequencer](#7-sequencer)
  - [8. Decoder](#8-decoder)
  - [9. Comparer](#9-comparer)
  - [10. Extender](#10-extender)
- [Workflow Case Study](#workflow-case-study)
- [Burp Certificate Setup](#burp-certificate-setup)
- [Session Handling Rules](#session-handling-rules)
- [Tips and Best Practices](#tips-and-best-practices)
- [Legal & Ethical Use](#legal--ethical-use)

---

# Introduction

Burp Suite is a toolkit used for:

- Web application penetration testing  
- Manual exploitation  
- Automated vulnerability discovery  
- API security testing  
- Authentication and session analysis

Burp is the **standard tool in professional pentesting**, often paired with:

- OWASP Labs (Juice Shop, DVWA, Mutillidae)
- Bug bounty platforms (HackerOne, Bugcrowd)
- CI/CD pipelines

---

# Architecture Overview

Burp Suite operates using a **man-in-the-middle (MITM) proxy**: Browser ⇨ Burp Proxy ⇨ Web Application


It allows you to observe and modify all traffic flowing between a client and server.

---

# Burp Suite Tabs

Below is an **in-depth explanation** of each Burp Suite component.

---

## 1. Target

### Purpose

The Target tab provides a **map of the application**, showing everything Burp has seen.

### Key Features

- **Site Map**
- **Scope Management**
- **Contextual Menu Actions**

### What you can analyze

✔ Directory structure  
/
├─ /login
├─ /register
├─ /products
│   ├─ /1
│   ├─ /2
│   └─ /3
├─ /admin
└─ /api
    ├─ /users
    └─ /orders


Hidden admin page

Parameterized product IDs: /products/1

Both are attack surfaces
  


✔ Parameters  
---
Captured request:

GET /products?category=shoes&page=2 HTTP/1.1
Host: localhost:3000


Parameters detected:

Parameter	Value
category	shoes
page	2

You can test them with:

page=-1
page=9999
page=' OR 1=1 --
category=<script>alert(1)</script>
  



✔ HTTP methods  
---

Burp shows which methods the server accepts:

URL	Method
/login	POST
/products	GET
/api/users	GET, POST
/admin	GET, DELETE ❗

If you see something like:

DELETE /users/23


…that could allow user deletion if not protected.

| Method      | Purpose                      | Example Request                         | Typical Use                       | Security Risk              | What to Check in Burp                  |
| ----------- | ---------------------------- | --------------------------------------- | --------------------------------- | -------------------------- | -------------------------------------- |
| **GET**     | Retrieve data                | `GET /products/1`                       | Viewing pages, fetching info      | Data exposure              | Sensitive info in response, parameters |
| **POST**    | Submit data to server        | `POST /login`                           | Login forms, upload               | Injection, CSRF            | Inspect body, test payloads            |
| **PUT**     | Create or replace a resource | `PUT /api/users/23`                     | Update user profile, replace data | Overwrites entire resource | Is auth required? Validation?          |
| **PATCH**   | Partial update               | `PATCH /api/users/23 {"role": "admin"}` | Edit single field                 | Privilege escalation       | Does app validate fields?              |
| **DELETE**  | Remove resource              | `DELETE /api/users/23`                  | Delete account, remove record     | **Data loss**, IDOR        | Should require admin-only access       |
| **OPTIONS** | Ask what methods are allowed | `OPTIONS /admin`                        | Debugging                         | Reveals attack surface     | Check allowed methods returned         |
| **HEAD**    | GET without body             | `HEAD /page`                            | Testing availability              | Cache tricks               | Does response expose metadata?         |
| **TRACE**   | Echo received request        | `TRACE /`                               | Debugging                         | Rare but can cause XSS     | Should be disabled                     |
| **CONNECT** | Tunnel formation             | `CONNECT example.com:443`               | HTTPS proxying                    | SSRF potential             | Normally blocked                       |


/login     → POST


/products  → GET


/api/users → GET, POST


/admin     → GET, DELETE ❗


✔ Why this matters
---

Each method can be exploited differently.

🔹 GET Example (Information Leak)
GET /api/users?role=admin


If this returns admin data → bad.

🔹 POST Example (Login)
POST /login
username=admin&password=123456


Burp can:

Modify

Repeat

Brute-force

🔹 DELETE Example (High Risk!)
DELETE /users/23


If no authentication:

👉 You can delete anyone.


  


✔ Status codes  
---


Burp history may show:

Path	Status
/login	200 OK
/admin	401 Unauthorized
/secret.txt	404 Not Found
/backup.zip	200 OK ❗
/logout	302 Redirect

Interesting cases:

/backup.zip returning 200 ⇒ Sensitive file exposed

/admin gives 401 ⇒ Authentication exists

Status differences help find vulnerabilities.
  

✔ Server fingerprints
---


Response headers Burp shows:

Server: Apache/2.4.51 (Ubuntu)
X-Powered-By: PHP/7.4.3
Set-Cookie: PHPSESSID=abcd1234


From this we learn:

Using Apache 2.4.51 ⇒ check CVEs

Backend is PHP

Session cookie is PHPSESSID

A tester might search:

"Apache/2.4.51 exploit"
"PHP/7.4.3 vulnerabilities"


### Adding to Scope
---

Scope is important:

- Burp focuses only on chosen host(s)  
- Prevents out-of-scope traffic logging (legal/safety)

---

## 2. Proxy

### Purpose

Intercept and modify all HTTP/HTTPS requests:

- Headers
- Cookies
- Body data
- URL parameters

### Modes

- **Intercept ON/OFF**
- **HTTP History**
- **WebSockets History**

### Example use case

Modify a POST request:


POST /login
username=admin
password=admin123


Test for invalid inputs:



username=admin'--
password=anything


---

## 3. Spider / Crawler

### Purpose

Automatically **discover content** by:

- Following links
- Submitting forms
- Bruteforcing directories (optional)

### Benefits

- Finds hidden functionality
- Helps build **attack surface**
- Reveals **API endpoints**

---

## 4. Scanner (Professional Only)

### Purpose

Automated vulnerability scanning:

- Active scan (attack)
- Passive scan (silent)

### Detection Categories

🛑 SQL Injection  
🛑 XSS (Reflected/Stored/DOM)  
🛑 CSRF  
🛑 Open redirect  
🛑 Insecure cookies  
🛑 Missing headers

### Recommendation Output

Scanner provides:

- Risk rating
- Proof-of-Concept
- Remediation advice

---

## 5. Intruder

### Purpose

Automated **payload-based attacks**.

### Typical Use Cases

- Username brute-force
- Password guessing
- Parameter fuzzing
- Enumeration

### Attack Types

| Type | Description |
|---|---|
| Sniper | One payload position, test values |
| Battering Ram | Same payload in all positions |
| Pitchfork | Multiple lists synchronized |
| Cluster Bomb | Multiple lists, all combinations |

### Example: Login Brute-force

Positions:



username=§admin§
password=§passwords§


Payload Lists:



admin
user
test

password
123456
qwerty


Intruder tests all combinations.

---

## 6. Repeater

### Purpose

Manual control over requests:

- Edit
- Replay
- Compare

### Common Uses

✔ Login bypass  
✔ Parameter tampering  
✔ IDOR (Insecure Direct Object Reference)  
✔ XSS testing

### Example Workflow

1. Capture login request
2. Send to Repeater
3. Modify:



isAdmin=true


4. Send
5. Observe response

---

## 7. Sequencer

### Purpose

Check **randomness of session tokens**.

### Tokens Analyzed

- Session cookies
- JWTs
- CSRF tokens

### Output

- Entropy analysis
- Bias detection
- Predictability

Weak tokens ⇒ **session hijacking risk**

---

## 8. Decoder

### Purpose

Convert data:

- Encode
- Decode
- Hash
- Beautify

### Supported Formats

- Base64
- URL
- HTML
- Hex
- JWT

### Example



SGVsbG8gV29ybGQ= → Hello World


---

## 9. Comparer

### Purpose

Highlight differences between responses.

### Use Cases

- Login success vs failure
- Error messages
- Output variations

---

## 10. Extender

### Purpose

Install plugins for advanced functionality.

### Extension Sources

- Burp BApp Store
- Custom scripts

### Popular Extensions

| Extension | Feature |
|---|---|
| ActiveScan++ | Improved scanner |
| DNS Resolver | Advanced DNS |
| Jython Support | Python scripting |
| Logger++ | Detailed logging |
| Hackvertor | Encode/Decode utilities |

---

# Workflow Case Study

Example: Testing an OWASP Juice Shop login.

### Step-by-Step

1. Target → Add to scope
2. Proxy → Capture login request
3. Send to Repeater
4. Modify parameters

Try typical bypasses:



admin'--
" OR "1"="1


5. Response analysis
6. Intruder → automated attack on username/password
7. Sequencer → analyze session token
8. Report findings

---

# Burp Certificate Setup

For HTTPS interception:

1. Open Burp browser
2. Go to: `http://burp`
3. Download CA certificate
4. Import into browser
5. Trust for web traffic

Now you can see decrypted HTTPS.

---

# Session Handling Rules

Advanced handling:

- Session token refresh
- CSRF token auto-update
- Conditional logic

Great for:

- Login tests
- Multi-step workflows

---

# Tips and Best Practices

✔ Always define **scope**

✔ Use **Repeater first**, then **Intruder**

✔ Avoid crashing systems — throttle attacks

✔ Use **proxy history** to spot sensitive information:

- Cookies
- Tokens
- API keys

✔ Look for response differences:

- Status codes
- Content-Length changes

---

# Legal & Ethical Use

Burp Suite is powerful.

Use only on:

- Systems you own
- Labs
- Explicit permission

Unauthorized testing = illegal.

---

# Final Notes

Burp Suite is a cornerstone tool for:

- Penetration testing
- Vulnerability research
- Bug bounties
- Education

Mastering Burp means mastering web application security.
