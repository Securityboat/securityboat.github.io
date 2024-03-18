# JSON Web Tokens (JWT4B)

### Description

JSON Web Tokens (JWT4B) is used to decode and manipulate JSON web tokens on the fly, and it checks for their validity and automates common attacks.

Features of JWT4B

* Automatic recognition
* JWT Editor
* Resigning of JWTs
* Signature checks
* Automated attacks available such as "Alg None" & "CVE-2018-0114"
* Validity checks and support for 'expires', 'not before', 'issued at' fields in the payload
* Automatic tests for security flags in cookie transmitted JWTs

### Steps to install

1. Start Burp Suite.
2. Move to the Extender tab.
3. Go to BApp Store.
4. Search JSON web tokens.
5. Hit Install.

### Build Your Own Version with Eclipse

1. Clone this repository [https://github.com/PortSwigger/json-web-tokens](https://github.com/PortSwigger/json-web-tokens) create a new Eclipse Java project.
2. Right-click go to configure and click on "Convert to Maven Project".
3. Open Burp Suite go to Extender.
4. Go to APIs and click on "Save files interface" Copy all files to JWT4B\src\burp
5. Export runnable fat JAR including libraries.
6. Load the JAR in Burp through the Extender Tab -> Extensions -> Click Add

### Reference

{% embed url="https://github.com/PortSwigger/json-web-tokens" %}
