# **Searching for Code in .NET**

Firstly, one needs to be familiar with the tools one can use in order to perform text searching, following this one needs to know what to look for.

One could scan through the code looking for common patterns or keywords such as “User”, “Password”, “Pswd”, “Key”, “Http”, etc... This can be performed using the “Find in Files” tool in VS or using find string as follows: findstr /s /m /i /d:c:\projects\codebase\sec “http” \*.\*

**HTTP Request Strings**

Requests from external sources are obviously a key area of a security code review. We need to ensure that all HTTP requests received are data validated for composition, max and min length, and if the data falls within the realms of the parameter whitelist. Bottom-line is this is a key area to look at and ensure security is enabled.\


| **STRING TO SEARCH** |                     |                         |                       |
| -------------------- | ------------------- | ----------------------- | --------------------- |
| request.accesstypes  | request.httpmethod  | request.cookies         | request.url           |
| request.browser      | request.querystring | request.certificate     | request.urlreferrer   |
| request.files        | request.item        | request.rawurl          | request.useragent     |
| request.headers      | request.form        | request.servervariables | request.userlanguages |
| request.TotalBytes   | request.BinaryRead  |                         |                       |

**HTML Output**

Here we are looking for responses to the client. Responses which go unvalidated or which echo external input without data validation are key areas to examine. Many client side attacks result from poor response validation.

| **STRING TO SEARCH** |             |            |           |
| -------------------- | ----------- | ---------- | --------- |
| response.write       | HttpUtility | HtmlEncode | UrlEncode |
| innerText            | innerHTML   | <%=        |           |

**SQL & Database**

Locating where a database may be involved in the code is an important aspect of the code review. Looking at the database code will help determine if the application is vulnerable to SQL injection. One aspect of this is to verify that the code uses either SqlParameter, OleDbParameter, or OdbcParameter(System.Data.SqlClient). These are typed and treat parameters as the literal value and not executable code in the database.

| **STRING TO SEARCH** |                 |                     |                     |
| -------------------- | --------------- | ------------------- | ------------------- |
| exec sp\_            | select from     | insert              | update              |
| delete from where    | delete          | execute sp\_        | exec xp\_           |
| exec @               | execute @       | executestatement    | executeSQL          |
| setfilter            | executeQuery    | GetQueryResultInXML | adodb               |
| sqloledb             | sql server      | driver              | Server.CreateObject |
| .Provider            | System.Data.sql | ADODB.recordset     | New OleDbConnection |
| ExecuteReader        | DataSource      | SqlCommand          | Microsoft.Jet       |
| SqlDataReader        | ExecuteReader   | SqlDataAdapter      | StoredProcedure     |

**Cookies**

Cookie manipulation can be key to various application security exploits, such as session hijacking/fixation and parameter manipulation. One should examine any code relating to cookie functionality, as this would have a bearing on session security.

| **STRING TO SEARCH** |          |                 |   |
| -------------------- | -------- | --------------- | - |
| System.Net.Cookie    | HTTPOnly | document.cookie |   |

**machine.config**

It is important that many variables in machine.config can be overridden in the web.config file for a particular application.

| **STRING TO SEARCH** |                 |                    |                 |
| -------------------- | --------------- | ------------------ | --------------- |
| validateRequest      | enableViewState | enableViewStateMac | validateRequest |

**HTML Tags**

Many of the HTML tags below can be used for client side attacks such as cross site scripting. It is important to examine the context in which these tags are used and to examine any relevant data validation associated with the display and use of such tags within a web application.

| **STRING TO SEARCH** |           |                  |                   |
| -------------------- | --------- | ---------------- | ----------------- |
| HtmlEncode           | URLEncode | \<applet>        | \<frameset>       |
| \<embed>             | \<frame>  | \<html>          | \<iframe>         |
| \<img>               | \<style>  | \<layer>         | \<ilayer>         |
| \<meta>              | \<object> | \<frame security | \<iframe security |

**Input Controls**

The input controls below are server classes used to produce and display web application form fields. Looking for such references helps locate entry points into the application.

| **STRING TO SEARCH**         |                         |                       |                          |
| ---------------------------- | ----------------------- | --------------------- | ------------------------ |
| htmlcontrols.htmlinputhidden | webcontrols.hiddenfield | webcontrols.hyperlink | webcontrols.textbox      |
| webcontrols.label            | webcontrols.linkbutton  | webcontrols.listbox   | webcontrols.checkboxlist |
| webcontrols.dropdownlist     |                         |                       |                          |

**Logging**

Logging can be a source of information leakage. It is important to examine all calls to the logging subsystem and to determine if any sensitive information is being logged. Common mistakes are logging userID in conjunction with passwords within the authentication functionality or logging database requests which may contain sensitive data.

| **STRING TO SEARCH** |                   |                          |                          |
| -------------------- | ----------------- | ------------------------ | ------------------------ |
| log4net              | Console.WriteLine | System.Diagnostics.Debug | System.Diagnostics.Trace |

**WEB.config**

The .NET Framework relies on .config files to define configuration settings. The .config files are text-based XML files. Many .config files can, and typically do, exist on a single system. Web applications refer to a web.config file located in the application’s root directory. For ASP.NET applications, web.config contains information about most aspects of the application’s operation.

| **STRING TO SEARCH**     |                        |                       |                          |
| ------------------------ | ---------------------- | --------------------- | ------------------------ |
| requestEncoding          | responseEncoding       | Trace                 | authorization            |
| compilation              | webcontrols.linkbutton | webcontrols.listbox   | webcontrols.checkboxlist |
| webcontrols.dropdownlist | CustomErrors           | httpCookies           | httpHandlers             |
| httpRuntime              | sessionState           | maxRequestLength      | Debug                    |
| forms protection         | appSettings            | ConfigurationSettings | appSettings              |
| connectionStrings        | authentication mode    | Allow                 | Deny                     |
| Credentials              | identity impersonate   | timeout               | remote                   |

**global.asax**

Each application has its own global.asax file if one is required. Global.asax sets the event code and values for an application using scripts. One must ensure that application variables do not contain sensitive information, as they are accessible to the whole application and to all users within it.

| **STRING TO SEARCH**               |                                 |                  |                |
| ---------------------------------- | ------------------------------- | ---------------- | -------------- |
| Application\_OnAuthenticateRequest | Application\_OnAuthorizeRequest | Session\_OnStart | Session\_OnEnd |

**Class Design**

Public and Sealed relate to the design at class level. Classes that are not intended to be derived from should be sealed. Make sure all class fields are Public for a reason. Don’t expose anything that is not necessary

| **STRING TO SEARCH** |        |   |   |
| -------------------- | ------ | - | - |
| Public               | Sealed |   |   |

**Threads and Concurrency**

Locating code that contains multithreaded functions as concurrency issues can result in race conditions, which may result in security vulnerabilities. The Thread keyword is where new threads objects are created. Code that uses static global variables that hold sensitive security information may cause session issues. Code that uses static constructors may also cause issues between threads. Not synchronizing the Dispose method may cause issues if a number of threads call Dispose at the same time, this may cause resource release issues.

| **STRING TO SEARCH** |         |   |   |
| -------------------- | ------- | - | - |
| Thread               | Dispose |   |   |

**Reflection and Serialization**

Code may be generated dynamically at runtime. Code that is generated dynamically as a function of external input may give rise to issues. If code contains sensitive data, does it need to be serialized?

| **STRING TO SEARCH** |                                       |               |                   |
| -------------------- | ------------------------------------- | ------------- | ----------------- |
| Serializable         | AllowPartiallyTrustedCallersAttribute | GetObjectData | System.Reflection |
| StrongNameIdentity   | StrongNameIdentityPermission          |               |                   |

**Storage**

If storing sensitive data in memory, it is recommended to use the following.

| **STRING TO SEARCH** |                 |   |   |
| -------------------- | --------------- | - | - |
| SecureString         | ProtectedMemory |   |   |

**Exceptions & Errors**

Ensure that the catch blocks do not leak information to the user in the case of an exception. Ensure when dealing with resources that the finally block is used. Having trace enabled is not great from an information leakage perspective. Ensure customized errors are properly implemented

| **STRING TO SEARCH** |         |               |                   |
| -------------------- | ------- | ------------- | ----------------- |
| catch                | finally | trace enabled | customErrors mode |

**Cryptography**

If cryptography is used then is a strong enough cipher used, i.e. AES or 3DES? What size key is used? The larger the better. Where is hashing performed? Are passwords that are being persisted hashed? They should be. How are random numbers generated? Is the PRNG “random enough”?

| **STRING TO SEARCH**     |                              |               |        |
| ------------------------ | ---------------------------- | ------------- | ------ |
| RNGCryptoServiceProvider | SHA                          | MD5           | base64 |
| DES                      | RC2                          | System.Random | Random |
| xor                      | System.Security.Cryptography |               |        |

**Authorization, Assert & Revert**

Bypassing the .Net code access security permission? Not a good idea. Below is a list of potentially dangerous permissions such as calling unmanaged code, outside the CLR.

| **STRING TO SEARCH** |                 |                        |                  |
| -------------------- | --------------- | ---------------------- | ---------------- |
| RequestMinimum       | RequestOptional | Assert                 | Debug.Assert     |
| CodeAccessPermission | MemberAccess    | ControlAppDomain       | UnmanagedCode    |
| SkipVerification     | ControlEvidence | SerializationFormatter | ControlPrincipal |
| ControlDomainPolicy  | ControlPolicy   |                        |                  |

**Legacy Methods**

Some standard functions that should be checked in any context include the following

| **STRING TO SEARCH** |        |   |   |
| -------------------- | ------ | - | - |
| printf               | strcpy |   |   |



