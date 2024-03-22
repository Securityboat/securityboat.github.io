---
description: SQL injection, also known as SQLI
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# **SQL Injection**

### **Vulnerability Name**

SQL Injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

SQL injection, also known as SQLI, is a common attack vector that uses malicious SQL code for backend database manipulation to access information that was not intended to be displayed. This information may include any number of items, including sensitive company data, user lists or private customer details.

In some situations, an attacker can escalate a SQL injection attack to compromise the underlying server or other back-end infrastructure. It can also enable them to perform denial-of-service attacks.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Payload**

```
Add your payload here
```

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Intercept the request in burp suite and send it to repeater.
3. Change the value of _\[Vulnerable Parameter]_ to the above payload and send the request.
4. Observe as the payload executes in the response.

### **&#x20;**POC****

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

There are a number of things an attacker can do when exploiting an SQL injection on a vulnerable website. Usually, it depends on the privileges of the user the web application uses to connect to the database server. By exploiting an SQL injection vulnerability, an attacker can:

* Add, delete, edit or read content in the database
* Read source code from files on the database server
* Write files to the database server

It all depends on the capabilities of the attacker.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Ensure that when a user’s input is added to a backend SQL query, it is not string appended but placed into the specific SQL parameter.&#x20;
* Create character ranges (i.e., Numeric, alpha, alphanumeric, alphanumeric with specific characters) and ensure that each input is restricted to the minimum length whitelist necessary.&#x20;
* Disallow common injection characters and unnecessary or bad encoding schemas.&#x20;
* Ensure that proper logging is taking place and is being reviewed, and any malicious traffic which generates an alert is promptly throttled and eventually blacklisted.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/SQL\_Injection\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/SQL\_Injection\_Prevention\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)
