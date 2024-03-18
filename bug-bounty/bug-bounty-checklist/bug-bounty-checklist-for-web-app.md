# Bug Bounty Checklist for Web App

## Bug Bounty Checklist for Web App

> This checklist may help you to have a good methodology for bug bounty hunting\
> When you have done a action, don't forget to check ;)\
> Happy hunting !

### Table of Contents

* [Recon on wildcard domain](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#%22Recon\_on\_wildcard\_domain%22)
* [Single domain](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Single\_domain)
* [Information Gathering](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Information)
* [Configuration Management](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Configuration)
* [Secure Transmission](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Transmission)
* [Authentication](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Authentication)
* [Session Management](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Session)
* [Authorization](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Authorization)
* [Data Validation](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Validation)
* [Denial of Service](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Denial)
* [Business Logic](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Business)
* [Cryptography](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Cryptography)
* [Risky Functionality - File Uploads](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#File)
* [Risky Functionality - Card Payment](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#Card)
* [HTML 5](https://github.com/sehno/Bug-bounty/blob/master/bugbounty\_checklist.md#HTML)

### Recon on wildcard domain

* &#x20;Run amass
* &#x20;Run subfinder
* &#x20;Run assetfinder
* &#x20;Run dnsgen
* &#x20;Run massdns
* &#x20;Use httprobe
* &#x20;Run aquatone (screenshot for alive host)

### Single Domain

#### Scanning

* &#x20;Nmap scan
* &#x20;Burp crawler
* &#x20;ffuf (directory and file fuzzing)
* &#x20;hakrawler/gau/paramspider
* &#x20;Linkfinder
* &#x20;Url with Android application

#### Manual checking

* &#x20;Shodan
* &#x20;Censys
* &#x20;Google dorks
* &#x20;Pastebin
* &#x20;Github
* &#x20;OSINT

### Information Gathering

* &#x20;Manually explore the site
* &#x20;Spider/crawl for missed or hidden content
* &#x20;Check for files that expose content, such as robots.txt, sitemap.xml, .DS\_Store
* &#x20;Check the caches of major search engines for publicly accessible sites
* &#x20;Check for differences in content based on User Agent (eg, Mobile sites, access as a Search engine Crawler)
* &#x20;Perform Web Application Fingerprinting
* &#x20;Identify technologies used
* &#x20;Identify user roles
* &#x20;Identify application entry points
* &#x20;Identify client-side code
* &#x20;Identify multiple versions/channels (e.g. web, mobile web, mobile app, web services)
* &#x20;Identify co-hosted and related applications
* &#x20;Identify all hostnames and ports
* &#x20;Identify third-party hosted content
* &#x20;Identify Debug parameters

### Configuration Management

* &#x20;Check for commonly used application and administrative URLs
* &#x20;Check for old, backup and unreferenced files
* &#x20;Check HTTP methods supported and Cross Site Tracing (XST)
* &#x20;Test file extensions handling
* &#x20;Test for security HTTP headers (e.g. CSP, X-Frame-Options, HSTS)
* &#x20;Test for policies (e.g. Flash, Silverlight, robots)
* &#x20;Test for non-production data in live environment, and vice-versa
* &#x20;Check for sensitive data in client-side code (e.g. API keys, credentials)

### Secure Transmission

* &#x20;Check SSL Version, Algorithms, Key length
* &#x20;Check for Digital Certificate Validity (Duration, Signature and CN)
* &#x20;Check credentials only delivered over HTTPS
* &#x20;Check that the login form is delivered over HTTPS
* &#x20;Check session tokens only delivered over HTTPS
* &#x20;Check if HTTP Strict Transport Security (HSTS) in use

### Authentication

* &#x20;Test for user enumeration
* &#x20;Test for authentication bypass
* &#x20;Test for bruteforce protection
* &#x20;Test password quality rules
* &#x20;Test remember me functionality
* &#x20;Test for autocomplete on password forms/input
* &#x20;Test password reset and/or recovery
* &#x20;Test password change process
* &#x20;Test CAPTCHA
* &#x20;Test multi factor authentication
* &#x20;Test for logout functionality presence
* &#x20;Test for cache management on HTTP (eg Pragma, Expires, Max-age)
* &#x20;Test for default logins
* &#x20;Test for user-accessible authentication history
* &#x20;Test for out-of channel notification of account lockouts and successful password changes
* &#x20;Test for consistent authentication across applications with shared authentication schema / SSO

### Session Management

* &#x20;Establish how session management is handled in the application (eg, tokens in cookies, token in URL)
* &#x20;Check session tokens for cookie flags (httpOnly and secure)
* &#x20;Check session cookie scope (path and domain)
* &#x20;Check session cookie duration (expires and max-age)
* &#x20;Check session termination after a maximum lifetime
* &#x20;Check session termination after relative timeout
* &#x20;Check session termination after logout
* &#x20;Test to see if users can have multiple simultaneous sessions
* &#x20;Test session cookies for randomness
* &#x20;Confirm that new session tokens are issued on login, role change and logout
* &#x20;Test for consistent session management across applications with shared session management
* &#x20;Test for session puzzling
* &#x20;Test for CSRF and clickjacking

### Authorization

* &#x20;Test for path traversal
* &#x20;Test for bypassing authorization schema
* &#x20;Test for vertical Access control problems (a.k.a. Privilege Escalation)
* &#x20;Test for horizontal Access control problems (between two users at the same privilege level)
* &#x20;Test for missing authorization

### Data Validation

* &#x20;Test for Reflected Cross Site Scripting
* &#x20;Test for Stored Cross Site Scripting
* &#x20;Test for DOM based Cross Site Scripting
* &#x20;Test for Cross Site Flashing
* &#x20;Test for HTML Injection
* &#x20;Test for SQL Injection
* &#x20;Test for LDAP Injection
* &#x20;Test for ORM Injection
* &#x20;Test for XML Injection
* &#x20;Test for XXE Injection
* &#x20;Test for SSI Injection
* &#x20;Test for XPath Injection
* &#x20;Test for XQuery Injection
* &#x20;Test for IMAP/SMTP Injection
* &#x20;Test for Code Injection
* &#x20;Test for Expression Language Injection
* &#x20;Test for Command Injection
* &#x20;Test for Overflow (Stack, Heap and Integer)
* &#x20;Test for Format String
* &#x20;Test for incubated vulnerabilities
* &#x20;Test for HTTP Splitting/Smuggling
* &#x20;Test for HTTP Verb Tampering
* &#x20;Test for Open Redirection
* &#x20;Test for Local File Inclusion
* &#x20;Test for Remote File Inclusion
* &#x20;Compare client-side and server-side validation rules
* &#x20;Test for NoSQL injection
* &#x20;Test for HTTP parameter pollution
* &#x20;Test for auto-binding
* &#x20;Test for Mass Assignment
* &#x20;Test for NULL/Invalid Session Cookie

### Denial of Service

* &#x20;Test for anti-automation
* &#x20;Test for account lockout
* &#x20;Test for HTTP protocol DoS
* &#x20;Test for SQL wildcard DoS

### Business Logic

* &#x20;Test for feature misuse
* &#x20;Test for lack of non-repudiation
* &#x20;Test for trust relationships
* &#x20;Test for integrity of data
* &#x20;Test segregation of duties

### Cryptography

* &#x20;Check if data which should be encrypted is not
* &#x20;Check for wrong algorithms usage depending on context
* &#x20;Check for weak algorithms usage
* &#x20;Check for proper use of salting
* &#x20;Check for randomness functions

### Risky Functionality - File Uploads

* &#x20;Test that acceptable file types are whitelisted
* &#x20;Test that file size limits, upload frequency and total file counts are defined and are enforced
* &#x20;Test that file contents match the defined file type
* &#x20;Test that all file uploads have Anti-Virus scanning in-place.
* &#x20;Test that unsafe filenames are sanitised
* &#x20;Test that uploaded files are not directly accessible within the web root
* &#x20;Test that uploaded files are not served on the same hostname/port
* &#x20;Test that files and other media are integrated with the authentication and authorisation schemas

### Risky Functionality - Card Payment

* &#x20;Test for known vulnerabilities and configuration issues on Web Server and Web Application
* &#x20;Test for default or guessable password
* &#x20;Test for non-production data in live environment, and vice-versa
* &#x20;Test for Injection vulnerabilities
* &#x20;Test for Buffer Overflows
* &#x20;Test for Insecure Cryptographic Storage
* &#x20;Test for Insufficient Transport Layer Protection
* &#x20;Test for Improper Error Handling
* &#x20;Test for all vulnerabilities with a CVSS v2 score > 4.0
* &#x20;Test for Authentication and Authorization issues
* &#x20;Test for CSRF

### HTML 5

* &#x20;Test Web Messaging
* &#x20;Test for Web Storage SQL injection
* &#x20;Check CORS implementation
* &#x20;Check Offline Web Application

### Source: 

{% embed url="https://github.com/sehno/Bug-bounty/blob/master/bugbounty_checklist.md" %}

