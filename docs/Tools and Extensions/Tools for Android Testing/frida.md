# **Frida**



Frida is a free and open-source dynamic code instrumentation toolkit, used for intercepting IPC(Interprocess Communication) requests and modifying it to make a function perform the desired operation, this concept is called Hooking. Dynamic instrumentation is the process of modifying the instructions of a binary program while it executes.

Some use cases of Frida

* Spy on Crypto APIs
* Modify function’s output
* Bypass AES encryption
* Bypass SSLPinning and Root detection
* Trace private application code
* Bypass various software sided locks (like app lock)

### **Setting Up Frida For Testing**

We need to install the Frida tool on a laptop/PC and Frida Server on a mobile device.&#x20;

#### **Steps to Frida tool install on Laptop/PC**

1. Install Python 3 and the latest pip.
2. Open the terminal or command prompt and run the following command.              `pip install frida-tools`
3. Verify Frida is installed properly.                                                                         `frida --version`
4. If the version is displayed then Frida is properly installed.

#### **Steps to install on Android device&#x20;**

1. Execute the following command to get to know about the process type on the device( Emulator/Physical device ).                                                                                      `adb shell                                                                    getprop | grep abi`                                                       &#x20;
2. Download the supported Frida server from  [https://github.com/frida/frida/releases](https://github.com/frida/frida/releases)
3. Unzip the downloaded folder and CD into the directory.
4.  Push Frida Server into the device.&#x20;

    `ADB push Frida server /data/local/tmp`
5. Do ADB shell and CD into _/data/local/tmp._                                                              `adb shell                                                     su                                                             cd data/local/tmp`
6. Give Executable permission to Frida Server.                                                     `chmod 777 frida-server`
7. Run Frida Server.                                                                                              `./frida-server`

### **How To use**

