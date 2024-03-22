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

# **RFI (Remote File Inclusion)**

### **Vulnerability Name**

Remote File Inclusion on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Remote file inclusion attacks usually occur when an application receives a path to a file as input for a web page and does not properly sanitize it. This allows an external URL to be supplied to the include function.

This vulnerability targets web applications that dynamically reference external scripts. The perpetrator’s goal is to exploit the referencing function in an application to upload malware (e.g., backdoor shells) from a remote URL located within a different domain.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Payload**

```
Add your payload here
```

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Change the value of _\[Vulnerable Parameter]_ to the above payload.
3. Reload the page.
4. Observe as the payload executes.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

Using remote file inclusion (RFI), an attacker can cause the web application to include a remote file. This is possible for web applications that dynamically include external files or scripts. Potential web security consequences of a successful RFI attack range from sensitive information disclosure and cross-site scripting (XSS) to remote code execution and, as a final result, full system compromise.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values. If that isn't possible, verify that the input contains only permitted content, such as alphanumeric characters.
* After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.
* If you need to include local files in your website or web application code, use a whitelist of allowed file names and locations. Make sure that none of these files can be replaced by the attacker using file upload functions.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/file-path-traversal#how-to-prevent-a-path-traversal-attack](https://portswigger.net/web-security/file-path-traversal#how-to-prevent-a-path-traversal-attack)
