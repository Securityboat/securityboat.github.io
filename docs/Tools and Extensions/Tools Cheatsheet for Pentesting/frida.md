# **Frida**

1\. **Understanding the Target**: Before using Frida, you need to understand the target application or process you want to instrument. Identify the functions, APIs, or behaviors you want to intercept or modify.

2\. **Installation**

- Install Frida tools on your development machine (laptop/PC) using pip:
    ```
    pip install frida-tools
    ```
- Install Frida server on the target device (Android in this case):
    - Determine the device architecture (arm/arm64/x86/x86_64) using:
    ```
    adb shell getprop | grep abi
    ```
    - Download the compatible Frida server from the official repository: [Frida Releases](https://github.com/frida/frida/releases)
    - Extract the downloaded archive and navigate to the directory.
    - Push Frida server to the device:
    ```
    adb push frida-server /data/local/tmp
    ```
    - Enter ADB shell and navigate to the directory:
    ```
    adb shell
    cd /data/local/tmp
    ```
    - Provide executable permissions to Frida server:
    ```
    chmod 777 frida-server
    ```
    - Start Frida server:
    ```
    ./frida-server
       ```

3\. **Instrumentation**

- Launch the target application on the device.

- Write Frida scripts (JavaScript) to define hooks or modifications.

- Run the Frida CLI or scripts using Frida tools to inject instrumentation into the target process.

4\. **Example Usage**:

   - Spy on Crypto APIs:
     ```javascript
     Java.perform(function () {
         var Crypto = Java.use('javax.crypto.Cipher');
         Crypto.doFinal.overload('[B').implementation = function (data) {
             console.log("doFinal intercepted with data: " + data);
             return this.doFinal(data);
         };
     });
     ```
   - Bypass SSL Pinning:
     ```javascript
     Java.perform(function () {
         var TrustManagerImpl = Java.use('com.android.org.conscrypt.TrustManagerImpl');
         TrustManagerImpl.verifyChain.implementation = function (untrustedChain, trustAnchorChain, host, clientAuth, ocspData, tlsSctData) {
             // bypassing SSL pinning
             return;
         };
     });
     ```

5\. **Execution**:

   - Run Frida scripts against the target application:
     ```
     frida -U -f <package_name> -l <script.js> --no-pause
     ```
     Replace `<package_name>` with the target application's package name and `<script.js>` with the path to your Frida script.

6\. **Verification**: Monitor the output of Frida scripts to verify that hooks are functioning as expected. You can observe logs or interactions as defined in your Frida scripts.

7\. **Cleanup**: After testing, make sure to stop Frida server on the device and remove the injected instrumentation from the target process.
