# **Bug Bounty Checklist For Android**

## **Table of Contents**

- [ ] Important Tools
- [ ] Improper Platform Usage
- [ ] Insecure Data Storage
- [ ] Insecure Communication
- [ ] Insecure Authentication
- [ ] Insufficient Cryptography
- [ ] Insecure Authorization
- [ ] Client Code Quality
- [ ] Code Tampering
- [ ] Reverse Engineering
- [ ] Extraneous Functionality

## **Important Tools**

- [ ] MobSF
- [ ] Frida
- [ ] Yazzhini
- [ ] Objection
- [ ] Run time Security Framework (RMS)
- [ ] House
- [ ] APK Toolkit
- [ ] JADX
- [ ] Drozer
- [ ] Fridump
- [ ] APKLeaks

## **Improper Platform Usage**

- [ ] Test for app permissions.
- [ ] Test for minimum security requirements.
- [ ] Test for OS versions that are allowed to install ( Insecure version ).
- [ ] Check ports open at the Firewall.
- [ ] Test default credentials on the application server.
- [ ] Check password policy implementation.
- [ ] Test for security misconfiguration on server API.
- [ ] Test input validation on API.
- [ ] Test for information exposure through API response message.

## **Insecure Data Storage**

- [ ] Testing local storage for sensitive data
- [ ] Testing Logs for sensitive data.
- [ ] Determine whether sensitive data is sent to third parties.
- [ ] Determine whether the keyboard cache is disabled for text input fields.
- [ ] Determine whether sensitive data exposed via IPC Mechanisms
- [ ] Check for sensitive data exposure through User Interface.
- [ ] Testing Backups for sensitive data.
- [ ] Finding sensitive information for Auto-Generated screenshots.
- [ ] Check memory for sensitive data.
- [ ] Testing the Device-Access-Security Policy

## **Insecure Communication**

- [ ] Check for insecure transport layer protocols.
- [ ] Test for insecure algorithms.
- [ ] Test for SSL pinning implementation.
- [ ] Test for End-to-End encryption.
- [ ] Check use of disabling certificate validation.

## **Insufficient Cryptography**

- [ ] Testing for key management.
- [ ] Test for use of custom encryption protocols.
- [ ] Test for token/session creation and handling.

**Insecure Authorization**

- [ ] Test for client-side authorization breaches.
- [ ] Test for Insecure Direct Object Reference.
- [ ] Test for function level access controls.
- [ ] Test for bypassing business logic flaws.

## **Client Code Quality**

- [ ] Test for SQL injection and local file inclusion.
- [ ] Test Service components.
- [ ] Test insufficient webview hardening.
- [ ] Test XML injection.
- [ ] Test for Local file inclusion through NSFileManager or webviews.
- [ ] Test for sensitive information masking.

## **Code Tampering**

- [ ] Test for unauthorize code modification.
- [ ] Test for runtime manipulation.
- [ ] Check for rooted device.

## **Reverse Engineering**

- [ ] Test for code Obfuscating.
- [ ] Test for information leakage/ HArdcoded credentials in the binaries.

## **Extraneous Functionality**

- [ ] Test for password string disclosure.
- [ ] Test for hidden and unscrutinised functionality

