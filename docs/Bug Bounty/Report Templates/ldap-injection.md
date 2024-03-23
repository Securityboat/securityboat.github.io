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

# **LDAP Injection**

### **Vulnerability Name**

LDAP Injection on _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

LDAP injection arises when user-controllable data is copied in an unsafe way into an LDAP query that is performed by the application. If an attacker can inject LDAP metacharacters into the query, then they can interfere with the query's logic.&#x20;

A web application could use LDAP in order to let users authenticate or search other users’ information inside a corporate structure. The goal of LDAP injection attacks is to inject LDAP search filters metacharacters in a query which will be executed by the application.

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

Depending on the function for which the query is used, the attacker may be able to retrieve sensitive data to which they are not authorized, or subvert the application's logic to perform some unauthorized action.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* If possible, applications should avoid copying user-controllable data into LDAP queries. If this is unavoidable, then the data should be strictly validated to prevent LDAP injection attacks.&#x20;
* In most situations, it will be appropriate to allow only short alphanumeric strings to be copied into queries, and any other input should be rejected.&#x20;
* At a minimum, input containing any LDAP metacharacters should be rejected; characters that should be blocked include ( ) ; , \* | & = and whitespace.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Injection\_Prevention\_Cheat\_Sheet.html)
* [https://cwe.mitre.org/data/definitions/90.html](https://cwe.mitre.org/data/definitions/90.html)
