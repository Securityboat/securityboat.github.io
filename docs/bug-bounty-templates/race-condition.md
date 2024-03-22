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

# **Race condition**

### **Vulnerability Name**

Race condition at _\[Parameter]_ in _\[Module/Functionality]_

### **Vulnerability Description**

Race conditions are a common type of vulnerability closely related to business logic flaws. They occur when websites process requests concurrently without adequate safeguards. This can lead to multiple distinct threads interacting with the same data at the same time, resulting in a "collision" that causes unintended behavior in the application.&#x20;

A race condition attack uses carefully timed requests to cause intentional collisions and exploit this unintended behavior for malicious purposes. Like other logic flaws, the impact of a race condition is heavily dependent on the application and the specific functionality in which it occurs.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Log in the application.
2. Intercept the request in burp suite and send it to repeater.
3. Alter the value of _\[Vulnerable Parameter]_ and send the request.
4. Observe the response.

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

This vulnerability can grant attackers access to secured areas of an application. Once the attacker replaces the database update with their own set of data, they will be able to log in as an administrator. Other possibilities include manipulating API calls, tricking a central server into executing the same action multiple times despite it not being valid after the first time.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

* Avoid mixing data from different storage places.
* Ensure sensitive endpoints make state changes atomic by using the datastore's concurrency features.
* As a defense-in-depth measure, take advantage of datastore integrity and consistency features like column uniqueness constraints.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://portswigger.net/web-security/race-conditions#how-to-prevent-race-condition-vulnerabilities](https://portswigger.net/web-security/race-conditions#how-to-prevent-race-condition-vulnerabilities)
* [https://cwe.mitre.org/data/definitions/362.html](https://cwe.mitre.org/data/definitions/362.html)
