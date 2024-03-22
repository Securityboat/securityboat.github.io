---
description: >-
  Uploaded files represent a significant risk to applications. The first step in
  many attacks is to get some code to the system to be attacked. Then the attack
  only needs to find a way to get the code e
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

# **Unrestricted File Upload**

### **Vulnerability Name**

Unrestricted File Upload in _\[Module/Functionality]_

### **Vulnerability Description**

File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size. Failing to properly enforce restrictions on these could mean that even a basic image upload function can be used to upload arbitrary and potentially dangerous files instead. This could even include server-side script files that enable remote code execution.

In some cases, the act of uploading the file is in itself enough to cause damage. Other attacks may involve a follow-up HTTP request for the file, typically to trigger its execution by the server.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Log in to the application.
2. Go to _\[Affected URL]_.
3. Upload _\[Unrestricted File]_.
4. Observe as the file is uploaded.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

In the worst case scenario, the file's type isn't validated properly, and the server configuration allows certain types of file (such as `.php` and `.jsp`) to be executed as code. In this case, an attacker could potentially upload a server-side code file that functions as a web shell, effectively granting them full control over the server.

If the filename isn't validated properly, this could allow an attacker to overwrite critical files simply by uploading a file with the same name. If the server is also vulnerable to directory traversal, this could mean attackers are even able to upload files to unanticipated locations.

Failing to make sure that the size of the file falls within expected thresholds could also enable a form of denial-of-service (DoS) attack, whereby the attacker fills the available disk space.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Check the file extension against a whitelist of permitted extensions rather than a blacklist of prohibited ones. It's much easier to guess which extensions you might want to allow than it is to guess which ones an attacker might try to upload.
* Make sure the filename doesn't contain any substrings that may be interpreted as a directory or a traversal sequence (`../`).
* Rename uploaded files to avoid collisions that may cause existing files to be overwritten.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/File\_Upload\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/file-upload#how-to-prevent-file-upload-vulnerabilities](https://portswigger.net/web-security/file-upload#how-to-prevent-file-upload-vulnerabilities)

