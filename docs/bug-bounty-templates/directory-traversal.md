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

# **Directory Browsing**

### **Vulnerability Name**

Directory Browsing in _\[Module/Functionality]_

### **Vulnerability Description**

A directory browsing (AKA directory listing) provides an attacker with the complete index of all the resources located inside the directory. The specific risks and consequences vary depending on which files are listed and accessible.

Web servers can be configured to automatically list the contents of directories that do not have an index page. This can aid an attacker by enabling them to quickly identify the resources on a given path and proceed directly to analyzing and attacking those resources.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Navigate to _\[Affected URL]_.
2. Observe that directory browsing is enabled and the resources present in this directory are accessible to an attacker.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

Exposing the contents of a directory can lead to an attacker gaining access to source code or providing useful information for the attacker to devise exploits, such as the creation times of files or any information that may be encoded in file names. The files contained within the directory may reveal sensitive information or provide attackers with information regarding versions, platform information, and source code that may help uncover vulnerabilities in the application or infrastructure.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Configure your web server to prevent directory listings for all paths beneath the web root.
* Ensure sensitive information is removed from application directories and utilize access control lists to prevent access when necessary.
* Place into each directory a default file (such as index.htm) that the web server will display instead of returning a directory listing.

> **Add your specific remediation if required, the above is a general remediation.**

### **References**

* [https://portswigger.net/kb/issues/00600100\_directory-listing](https://portswigger.net/kb/issues/00600100\_directory-listing)
* [https://cwe.mitre.org/data/definitions/548.html](https://cwe.mitre.org/data/definitions/548.html)
