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

# **HTML Injection**

### **Vulnerability Name**

HTML Injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

HTML injection attack allows the injection of certain HTML tags into the web application. When an application does not properly handle user supplied data, an attacker can supply valid HTML code, typically via a parameter value, and inject their own content into the page.

This attack is typically used in conjunction with some form of social engineering, as the attack is exploiting a code-based vulnerability and a user's trust.

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

Malicious HTML can lead to the delivery of malware, infecting users' devices with viruses, ransomware, or other harmful software. Attackers may modify the appearance and content of a website, potentially damaging its reputation and integrity.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Encoding should be applied directly before user-controllable data is written to a page, because the context you're writing into determines what kind of encoding you need to use.
* Validate input as strictly as possible at the point when it is first received from a user. Input validation should ideally work by blocking invalid input.
* Allowing users to post HTML markup should be avoided wherever possible, but sometimes it's a business requirement. The classic approach is to try to filter out potentially harmful tags and HTML. You can try to implement this using a whitelist of safe tags and attributes.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html)
* [https://www.acunetix.com/vulnerabilities/web/html-injection/](https://www.acunetix.com/vulnerabilities/web/html-injection/)
