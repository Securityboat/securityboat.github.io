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

# **Use of Default Credentials**

### **Vulnerability Name**

Default Credentials working at _\[Login Portal]_

### **Vulnerability Description**

Many web applications and hardware devices have default passwords for the built-in administrative account. Although in some cases these can be randomly generated, they are often static, meaning that they can be easily guessed or obtained by an attacker.

Additionally, when new users are created on the applications, these may have predefined passwords set. These could either be generated automatically by the application, or manually created by staff. In both cases, if they are not generated in a secure manner, the passwords may be possible for an attacker to guess.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Enter these default credentials to log in: `Username Password`.
3. Observe as the default credentials are allowing log in into the application.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability allows unauthorized individuals to gain easy access to a system, device, or application with minimal effort. This security flaw poses a significant risk, potentially resulting in data breaches, unauthorized system control, and compromised user privacy.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* By eliminating commonly known or easily guessable username and password combinations, organizations bolster their defenses against potential attacks, such as brute force and credential stuffing.&#x20;
* Additionally, the adoption of strong, unique credentials underscores a commitment to security, fostering a culture of best practices and diligence among both users and administrators.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cwe.mitre.org/data/definitions/1392.html](https://cwe.mitre.org/data/definitions/1392.html)
* [https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/04-Authentication\_Testing/02-Testing\_for\_Default\_Credentials](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/04-Authentication\_Testing/02-Testing\_for\_Default\_Credentials)
