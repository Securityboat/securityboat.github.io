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

# **SSI Injection**

### **Vulnerability Name**

SSI Injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

SSI (Server Side Include) Injection is a attack technique where the web application fails to validate and sanitize the user-supplied input data before they are included into the server side. It allows an attacker to send any arbitrary code into the web application which will be executed locally by the server.

The Server-Side Includes attack allows the exploitation of a web application by injecting scripts in HTML pages or executing arbitrary codes remotely

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

By leveraging this attack vector, the attacker can get the access to sensitive information such as credentials, API keys, etc. and attacker can execute shell commands on server as well. The SSI injection payloads (directives) are injected in the input field of the web application and they are sent to the web server. The web server parses and executes those directives. then, the attack result will be shown on the web application when the user visits that page.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Disable the SSI execution wherever not required only enable specific directives that are required for a specific page and disable others&#x20;
* HTML entity encoding should be applied on all user input before passing to a page.
* Only short alphanumeric strings should be accepted. Input containing any other data, including any conceivable SSI metacharacter, should be rejected

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://owasp.org/www-community/attacks/Server-Side\_Includes\_(SSI)\_Injection](https://owasp.org/www-community/attacks/Server-Side\_Includes\_\(SSI\)\_Injection)
* [https://portswigger.net/kb/issues/00101100\_ssi-injection](https://portswigger.net/kb/issues/00101100\_ssi-injection)
