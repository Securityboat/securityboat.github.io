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

# **Response manipulation**

### **Vulnerability Name**

Response manipulation at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

A client-side resource manipulation vulnerability is an input validation flaw. It occurs when an application accepts user-controlled input that specifies the path of a resource such as the source of an iframe, JavaScript, applet, or the handler of an XMLHttpRequest.&#x20;

This vulnerability consists of the ability to control the URLs that link to some resources present in a web page. The impact of this vulnerability varies, and it is usually adopted to conduct XSS attacks. This vulnerability makes it is possible to interfere with the expected application’s behavior by causing it to load and render malicious objects.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Log in the application.
2. Intercept the request in burp suite.
3. Select the option: Do Intercept -> Response to this request.
4. Alter the value of _\[Vulnerable Parameter]_ and send the request.
5. Alter the value of _\[Vulnerable Parameter]_ and in the incoming response.
6. Turn off the intercept and observe the change in application.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

Attacker can interfere with the expected application’s behavior by causing it to load and render malicious objects. It enables them to potentially deliver misleading, unauthorized, or malicious content to end-users.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Do not use static response for validating authentication.
* Always place server-side validation on each request and validate users.
* Choose the appropriate token for the level of risk of the transaction.
* Where possible, implement multi-factor authentication to prevent automated, credential stuffing, brute force, and stolen credential re-use attacks.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/11-Client-side\_Testing/06-Testing\_for\_Client-side\_Resource\_Manipulation](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/11-Client-side\_Testing/06-Testing\_for\_Client-side\_Resource\_Manipulation)
