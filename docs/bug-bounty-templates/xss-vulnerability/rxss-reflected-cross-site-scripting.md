---
description: Also known as non-Persistent XSS
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

# **RXSS (Reflected cross-site scripting)**

### **Vulnerability Name**

Reflected XSS at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Reflected cross-site scripting (or XSS) arises when an application receives data in an HTTP request and includes that data within the immediate response in an unsafe way.

If another user of the application requests the attacker's URL, then the script supplied by the attacker will execute in the victim user's browser, in the context of their session with the application.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Payload**

```
Add your payload here
```

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Add the payload above in _\[Vulnerable Parameter]_ value.
3. Reload the page.
4. Observe as you should get an alert.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

* Gain access to users cookies, session IDs, passwords, private messages, etc.
* Read and access the content of a page for any attacked user and therefore all the information displayed to the user.
* Compromise the content shown to the user.
* Inject Trojan functionality into the website.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

To keep yourself safe from RXSS, you must sanitize your input. Your application code should never output data received as input directly to the browser without checking it for malicious code.

* Filter input on arrival.
* Encode data on output.
* Use appropriate response headers.
* Content Security Policy.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/cross-site-scripting/reflected](https://portswigger.net/web-security/cross-site-scripting/reflected)
* [https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html)
