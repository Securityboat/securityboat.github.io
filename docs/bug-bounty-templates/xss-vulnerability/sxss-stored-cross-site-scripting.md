---
description: Also known as Persistent XSS
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

# **SXSS (Stored cross-site scripting)**

### **Vulnerability Name**

Stored XSS at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

A Persistent XSS attack is possible when a website or web application stores user input and later serves it to other users. Stored XSS allows potential attackers to inject client-side scripts directly onto target servers. This is not just a single user issue, however, it affects everyone who has access to these servers. Once attackers find a vulnerability in the web application, they can inject their script and wait for an unsuspecting target to fall into their trap.

The injected script is permanently stored on the now infected servers and allows the attacker to set their targets up to receive the malicious script from the servers when they make a request.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Payload**

```
Add your payload here
```

### **Steps to Reproduce**

1. Go to _\[Affected URL]_ from account one.
2. Add the above payload in _\[Vulnerable Parameter]_ value.
3. Go to the vulnerable location from account two.
4. Observe as you get an alert.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

* Gain access to users cookies, session IDs, passwords, private messages, etc
* Read and access the content of a page for any attacked user and therefore all the information displayed to the user
* Compromise the content shown to the user

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

To keep yourself safe from RXSS, you must sanitize your input. Your application code should never output data received as input directly to the browser without checking it for malicious code.

* Filter input on arrival.
* Encode data on output.
* Use appropriate response headers.
* Content Security Policy.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/cross-site-scripting/stored](https://portswigger.net/web-security/cross-site-scripting/stored)
* [https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html)
