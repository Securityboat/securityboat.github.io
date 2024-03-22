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

# **Insecure Deserialization**

### **Vulnerability Name**

Insecure deserialization at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Insecure deserialization is when user-controllable data is deserialized by a website. This potentially enables an attacker to manipulate serialized objects in order to pass harmful data into the application code.

It is even possible to replace a serialized object with an object of an entirely different class. Alarmingly, objects of any class that is available to the website will be deserialized and instantiated, regardless of which class was expected. For this reason, insecure deserialization is sometimes known as an "object injection" vulnerability.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Intercept the request in burp suite and send it to repeater.
3. Alter the value of _\[Vulnerable Parameter]_ and send the request.
4. Observe the changes in the response.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability can provides an entry point to a massively increased attack surface. It allows an attacker to reuse existing application code in harmful ways, resulting in numerous other vulnerabilities, often remote code execution.

Even in cases where remote code execution is not possible, insecure deserialization can lead to privilege escalation, arbitrary file access, and denial-of-service attacks.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Generally speaking, deserialization of user input should be avoided unless absolutely necessary.&#x20;
* If you do need to deserialize data from untrusted sources, incorporate robust measures to make sure that the data has not been tampered with.&#x20;
* If possible, you should avoid using generic deserialization features altogether. Serialized data from these methods contains all attributes of the original object, including private fields that potentially contain sensitive information. Instead, you could create your own class-specific serialization methods so that you can at least control which fields are exposed.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Deserialization\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Deserialization\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/deserialization#how-to-prevent-insecure-deserialization-vulnerabilities](https://portswigger.net/web-security/deserialization#how-to-prevent-insecure-deserialization-vulnerabilities)
