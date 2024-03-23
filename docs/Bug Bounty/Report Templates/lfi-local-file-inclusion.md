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

# **LFI (Local File Inclusion)**

### **Vulnerability Name**

Local File Inclusion on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

An attacker can use local file inclusion to trick the web application into exposing or running files on the web server. Typically, LFI occurs when an application uses the path to a file as input. If the application treats this input as trusted, a local file may be used in the include statement.

This vulnerability allows an attacker to include a file, usually exploiting “dynamic file inclusion” mechanisms implemented in the target application. The vulnerability occurs due to the use of user-supplied input without proper validation.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Payload**

```
Add your payload here
```

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Change the value of _\[Vulnerable Parameter]_ to the above payload.
3. Check the response, and you will see the content of the mentioned file.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability can enable an attacker to read arbitrary files on the server that is running an application. This might include:

* Application code and data.
* Credentials for back-end systems.
* Sensitive operating system files.

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior, and ultimately take full control of the server.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values. If that isn't possible, verify that the input contains only permitted content, such as alphanumeric characters.
* After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.
* If you need to include local files in your website or web application code, use a whitelist of allowed file names and locations. Make sure that none of these files can be replaced by the attacker using file upload functions.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/file-path-traversal#how-to-prevent-a-path-traversal-attack](https://portswigger.net/web-security/file-path-traversal#how-to-prevent-a-path-traversal-attack)
* [https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html)
