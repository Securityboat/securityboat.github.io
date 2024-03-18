# SAML Raider

### Description

This extension is used for testing SAML infrastructures. It contains two core functionalities: Manipulating SAML Messages and manage X.509 certificates.

The message editor provides the following capabilities:

* Sign SAML messages & assertions (signature spoofing attack)
* Remove signatures (signature exclusion attack)
* Edit SAML messages (SAMLRequest, SAMLResponse & custom parameter names)
* Perform eight common XSW attacks
* Insert XXE and XSLT attack payloads
* Supported Profiles: SAML Webbrowser Single Sign-on Profile, Web Services Security SAML Token Profile
* Supported Bindings: POST Binding, Redirect Binding, SOAP Binding, URI Binding

The certificate manager provides the following capabilities:

* Import X.509 certificates (PEM and DER format)
* Import X.509 certificate chains
* Export X.509 certificates (PEM format)
* Delete imported X.509 certificates
* Display information of X.509 certificates
* Import private keys (PKCD#8 in DER format and traditional RSA in PEM Format)
* Export private keys (traditional RSA Key PEM Format)
* Cloning X.509 certificates
* Cloning X.509 certificate chains
* Create new X.509 certificates
* Editing and self-sign existing X.509 certificates

### Steps to install

1. Start Burp Suite.
2. Move to the Extender tab.
3. Go to BApp Store.
4. Search SAML raider.
5. Hit Install.

### References

{% embed url="https://github.com/PortSwigger/saml-raider" %}

{% embed url="https://blog.compass-security.com/2015/07/saml-burp-extension" %}
