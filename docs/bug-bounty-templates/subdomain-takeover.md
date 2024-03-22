---
description: >-
  Subdomain takeover is a process of registering a non-existing domain name to
  gain control over another domain.
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

# **Subdomain Takeover**

### **Vulnerability Name**

Subdomain Takeover of _\[Subdomain URL]_

### **Vulnerability Description**

A subdomain takeover occurs when an attacker gains control over a subdomain of a target domain. Typically, this happens when the subdomain has a canonical name (CNAME) in the Domain Name System (DNS), but no host is providing content for it.&#x20;

This can happen because either a virtual host hasn't been published yet or a virtual host has been removed. An attacker can take over that subdomain by providing their own virtual host and then hosting their own content for it.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Go to _\[Subdomain URL]_.
2. Observe as this URL shows _\[Specific Error]_.
3. The provider/engine for our target application is _\[Provider Name]_.
4. Since _\[Provider Name]_ does not perform any automated fingerprint check, we can try to register for this subdomain.&#x20;
5. Observe we are able to takeover _\[Subdomain URL]_ by registering it without any authentication.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

Attacker can potentially read cookies set from the main domain, perform cross-site scripting, or circumvent content security policies, thereby enabling them to capture protected information (including logins) or send malicious content to unsuspecting users.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Define standard processes for provisioning and deprovisioning hosts. Do all steps as closely together as possible.
* Put pressure on hosting vendors to close gaps; ask how they verify that someone claiming a virtual host actually has a legitimate claim to the domain name. Work within your organization to make this part of the vendor qualification process.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://developer.mozilla.org/en-US/docs/Web/Security/Subdomain\_takeovers](https://developer.mozilla.org/en-US/docs/Web/Security/Subdomain\_takeovers)
* [https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/02-Configuration\_and\_Deployment\_Management\_Testing/10-Test\_for\_Subdomain\_Takeover](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web\_Application\_Security\_Testing/02-Configuration\_and\_Deployment\_Management\_Testing/10-Test\_for\_Subdomain\_Takeover)

