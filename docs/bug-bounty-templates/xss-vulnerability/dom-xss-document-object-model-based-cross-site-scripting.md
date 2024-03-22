---
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

# **DOM-XSS (Document Object Model-based cross-site scripting)**

### **Vulnerability Name**

DOM-XSS at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

DOM-based XSS vulnerabilities usually arise when JavaScript takes data from an attacker-controllable source, such as the URL, and passes it to a sink that supports dynamic code execution, such as `eval()` or `innerHTML`. This enables attackers to execute malicious JavaScript, which typically allows them to hijack other users' accounts.

The targeted page itself (the HTTP response that is) does not change, but the client side code contained in the page executes differently due to the malicious modifications that have occurred in the DOM environment.

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

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

To keep yourself safe from XSS, you must sanitize your input. Your application code should never output data received as input directly to the browser without checking it for malicious code.

* Filter input on arrival.
* Encode data on output.
* Use appropriate response headers.
* Content Security Policy.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/cross-site-scripting/dom-based](https://portswigger.net/web-security/cross-site-scripting/dom-based)
* [https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross\_Site\_Scripting\_Prevention\_Cheat\_Sheet.html)

