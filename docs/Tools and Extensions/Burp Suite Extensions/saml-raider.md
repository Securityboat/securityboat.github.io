# **SAML Raider**

## **Description**

**SAML Raider** is an extension used for testing SAML infrastructures. It offers two core functionalities: Manipulating SAML Messages and managing X.509 certificates.

### Message Editor Features:

- Sign SAML messages & assertions (signature spoofing attack)
- Remove signatures (signature exclusion attack)
- Edit SAML messages (SAMLRequest, SAMLResponse & custom parameter names)
- Perform eight common XSW attacks
- Insert XXE and XSLT attack payloads
- Supported Profiles: SAML Web Browser Single Sign-on Profile, Web Services Security SAML Token Profile
- Supported Bindings: POST Binding, Redirect Binding, SOAP Binding, URI Binding

### Certificate Manager Features:

- Import X.509 certificates (PEM and DER format)
- Import X.509 certificate chains
- Export X.509 certificates (PEM format)
- Delete imported X.509 certificates
- Display information of X.509 certificates
- Import private keys (PKCD#8 in DER format and traditional RSA in PEM Format)
- Export private keys (traditional RSA Key PEM Format)
- Cloning X.509 certificates and certificate chains
- Create new X.509 certificates
- Editing and self-signing existing X.509 certificates

## **Steps to Install**

1. Start Burp Suite.
2. Navigate to the Extender tab.
3. Visit the BApp Store.
4. Search for SAML Raider.
5. Click Install.

## **References**

- [SAML Raider GitHub Repository](https://github.com/PortSwigger/saml-raider)
- [Compass Security Blog Post on SAML Burp Extension](https://blog.compass-security.com/2015/07/saml-burp-extension)
