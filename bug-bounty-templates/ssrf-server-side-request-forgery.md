---
description: >-
  Server-side request forgery (SSRF) is a web security vulnerability that allows
  an attacker to induce the server-side application to make HTTP requests to an
  arbitrary domain of the attacker's choosing
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

# **SSRF (Server-Side Request Forgery)**

### **Vulnerability Name**

SSRF at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).

As modern web applications provide end-users with convenient features, fetching a URL becomes a common scenario. As a result, the incidence of SSRF is increasing. Also, the severity of SSRF is becoming higher due to cloud services and the complexity of architectures.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Log in to the application.
2. Go to _\[Affected URL]_.
3. Intercept the request in burp suite and send it to repeater.
4. Alter the value of _\[Vulnerable Parameter]_ and send the request.
5. Observe the response.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability can often result in unauthorized actions or access to data within the organization. This can be in the vulnerable application, or on other back-end systems that the application can communicate with. In some situations, the SSRF vulnerability might allow an attacker to perform arbitrary command execution.

An SSRF exploit that causes connections to external third-party systems might result in malicious onward attacks. these can appear to originate from the organization hosting the vulnerable application.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Segment remote resource access functionality in separate networks to reduce the impact of SSRF
* Enforce “deny by default” firewall policies or network access control rules to block all but essential intranet traffic.
* Sanitize and validate all client-supplied input data
* Enforce the URL schema, port, and destination with a positive allow list

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/ssrf](https://portswigger.net/web-security/ssrf)
* [https://cheatsheetseries.owasp.org/cheatsheets/Server\_Side\_Request\_Forgery\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Server\_Side\_Request\_Forgery\_Prevention\_Cheat\_Sheet.html)
