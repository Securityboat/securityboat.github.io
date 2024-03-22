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

# **Clickjacking**

### **Vulnerability Name**

Clickjacking in _\[Module/Functionality]_

### **Vulnerability Description**

Clickjacking is an attack that tricks a user into clicking a webpage element that is invisible or disguised as another element. This can cause users to unwittingly download malware, visit malicious web pages, provide credentials or sensitive information, transfer money, or purchase products online.

The absence of the X-Frame-Options header in a web application's HTTP response can allow clickjacking attacks. This security header is used to instruct the browser on whether or not the web page can be embedded within an iframe on another site. Clickjacking is a client-side security issue that affects a variety of browsers and platforms.

> **Add your specific vulnerability description if required, the one given above is a general description.**

### **Steps to Reproduce**

1. Create a clickjacking POC by copying the code below into a new HTML file.
2. Replace the URL with your target domain and save the file.
3. Open this file in a new incognito tab.
4. Observe that the target application is successfully loaded into the iframe tags, indicating that it is vulnerable to clickjacking attacks.

<pre class="language-html" data-overflow="wrap" data-line-numbers data-full-width="false"><code class="lang-html">&#x3C;!DOCTYPE html>
&#x3C;html>
&#x3C;head>
	&#x3C;title>Clickjack test page&#x3C;/title>
&#x3C;/head>
&#x3C;body>
<strong>	&#x3C;iframe style="height: 500px; width: 500px;" src="http://example.com">&#x3C;/iframe>
</strong>&#x3C;/body>
&#x3C;/html>
</code></pre>

### **POC**

> **Modify the steps to reproduce above if required. Attach snapshots (POC) or a video link here.**

### **Impact**

An attacker could embed your website in an iframe and by tricking the UI, the user himself could unintentionally perform dangerous actions. You may think that kind of attack is not so dangerous but combined with other vulnerabilities, it could be deadly.

> **Add your specific impact if required, the one given above is a general impact.**

### **Remediation**

Server-side protection against clickjacking is provided by defining and communicating constraints over the use of components such as iframes.

* Preventing the browser from loading the page in frame using the X-Frame-Options or Content Security Policy (frame-ancestors) HTTP headers.
* Preventing session cookies from being included when the page is loaded in a frame using the SameSite cookie attribute.
* Implementing JavaScript code in the page to attempt to prevent it being loaded in a frame (known as a "frame-buster").

> **Add your specific remediation if required, the above is a general remediation.**

### **Reference**

* [https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking\_Defense\_Cheat\_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking\_Defense\_Cheat\_Sheet.html)
* [https://portswigger.net/web-security/clickjacking#how-to-prevent-clickjacking-attacks](https://portswigger.net/web-security/clickjacking#how-to-prevent-clickjacking-attacks)
