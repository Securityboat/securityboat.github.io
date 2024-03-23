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

# **Command Injection**

### **Vulnerability Name**

Command injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Command injection vulnerability let an attacker execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.

Any web interface that is not properly sanitized is subject to this exploit. With the ability to execute OS commands, the user can upload malicious programs or even obtain passwords.

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

A potential threat actor can execute unauthorized code on the targeted system, potentially resulting in a total system compromise. This could grant them access to sensitive data residing on the system. The attacker could initiate a Denial of Service (DoS) attack on the target by injecting commands designed to exhaust all available resources.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

The most effective way to prevent OS command injection vulnerabilities is to never call out to OS commands from application-layer code. In almost all cases, there are different ways to implement the required functionality using safer platform APIs.

If you have to call out to OS commands with user-supplied input, then you must perform strong input validation. Some examples of effective validation include:

* Validating against a whitelist of permitted values.
* Validating that the input is a number.
* Validating that the input contains only alphanumeric characters, no other syntax or whitespace.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/OS\_Command\_Injection\_Defense\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/OS\_Command\_Injection\_Defense\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/os-command-injection#how-to-prevent-os-command-injection-attacks](https://portswigger.net/web-security/os-command-injection#how-to-prevent-os-command-injection-attacks)
