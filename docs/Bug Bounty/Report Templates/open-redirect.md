---
description: URL redirection or open redirect.
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

# **Open Redirect**

### **Vulnerability Name**

Open Redirect at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Open redirection vulnerabilities arise when an application incorporates user-controllable data into the target of a redirection in an unsafe way. An attacker can construct a URL within the application that causes a redirection to an arbitrary external domain. This behavior can be leveraged to facilitate phishing attacks against users of the application.&#x20;

The ability to use an authentic application URL, targeting the correct domain and with a valid SSL certificate (if SSL is used), lends credibility to the phishing attack because many users, even if they verify these features, will not notice the subsequent redirection to a different domain.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Go to _\[Affected URL]_.
2. Change the value of _\[Vulnerable Parameter]_ to _\[example.com]_ and send the request.
3. Observe as the page redirects to given URL above.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

The user may be redirected to an untrusted page that contains malware which may then compromise the user's machine. This will expose the user to extensive risk and the user's interaction with the web server may also be compromised if the malware conducts keylogging or other attacks that steal credentials, personally identifiable information (PII), or other important data.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

If possible, applications should avoid incorporating user-controllable data into redirection targets. In many cases, this behavior can be avoided in two ways:

* Remove the redirection function from the application, and replace links to it with direct links to the relevant target URLs.
* Maintain a server-side list of all URLs that are permitted for redirection. Instead of passing the target URL as a parameter to the redirector, pass an index into this list.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/kb/issues/00500100\_open-redirection-reflected](https://portswigger.net/kb/issues/00500100\_open-redirection-reflected)
* [https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated\_Redirects\_and\_Forwards\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated\_Redirects\_and\_Forwards\_Cheat\_Sheet.html)

