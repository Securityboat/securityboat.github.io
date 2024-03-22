---
description: (Carriage Return (ASCII 13, \r) Line Feed (ASCII 10, \n)) %0d%0a
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

# **CRLF Injection**

### **Vulnerability Name**

CRLF Injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

In a CRLF injection vulnerability attack, the attacker inserts both the carriage return and linefeed characters into user input to trick the server, the web application, or the user into thinking that an object is terminated and another one has started.

This attack occurs when a user manages to submit a CRLF into an application. This is most commonly done by modifying an HTTP parameter or URL.

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

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability can lead to a range of security issues, including HTTP response splitting, where an attacker can control the content of the response, potentially delivering malicious content or redirecting users to harmful websites.&#x20;

CRLF injection can also be used in conjunction with other attacks like Cross-Site Scripting (XSS) and Cross-Site Request Forgery (CSRF) to further compromise a web application, steal sensitive data, or manipulate user interactions.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Do not use users input directly inside response headers. If that is not possible, you should always use a function to encode the CRLF special characters.&#x20;
* Validate and sanitize user input, ensuring that no CRLF characters or other special characters can be injected into HTTP headers or request parameters.&#x20;
* Use output encoding when rendering user-generated content to prevent the injection of malicious data into responses.&#x20;
* Server configurations should be set to reject any requests containing CRLF characters, and Intrusion Detection Systems (IDS) or Web Application Firewalls (WAF) can be employed to monitor and filter out potentially malicious traffic.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html)
* [https://owasp.org/www-community/vulnerabilities/CRLF\_Injection](https://owasp.org/www-community/vulnerabilities/CRLF\_Injection)
