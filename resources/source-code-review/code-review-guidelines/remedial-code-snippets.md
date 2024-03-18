---
description: Sample remedial code snippet examples
---

# Remedial Code Snippets

### **Always Use Security Manager**

The security manager is a class that allows applications to implement a security policy. It allows an application to determine, before performing a possibly unsafe or sensitive operation, what the operation is and whether it is being attempted in a security context that allows the operation to be performed. The application can allow or disallow the operation.

**Non-Complaint Code:**

```
try {
 System.setSecurityManager(null);
} catch (SecurityException se) { System.out.println("SecurityManager is already set!"); }
```

**Running environment:**

_`Java <application name>`_

**Compliant Code:**

```
try {
 System.setSecurityManager(new CustomSecurityManager("password here"));
 SecurityManager sm = System.getSecurityManager();
 if(sm != null) { //check if file can be read
 FilePermission perm = new FilePermission("/temp/tempFile", "read");
 sm.checkPermission(perm);
 }
} catch (SecurityException se) { System.out.println("Not allowed"); }
```

**Running environment:**

```
Java -Djava.security.manager -Djava.security.policy = policyURL <application name>
```

**Risk Assessment**

Running Java code without a Security Manager being set means that there is no security at all.

| **Risk Level:** | High |
| --------------- | ---- |

### **Do not Bypass Security Manager Checks**

&#x20;Security manager checks may be allowed to get bypassed depending on the immediate caller's class loader. When an API (see table below) is invoked on a class object, a comparison is run between the immediate caller's class loader and that of the class object. The class object is the object on which an API is invoked. For instance, in the presence of a security manager, the **getSystemClassLoader** and **getParent** methods succeed only if the caller's class loader is the delegation ancestor of the current class loader or if the caller's class loader is the same as the current one or if the code in the current execution context has the Run Time Permission, namely "getClassLoader".

| **APIs capable of bypassing the Security Manager’s checks** |
| ----------------------------------------------------------- |
| `java.lang.Class.newInstance`                               |
| `java.lang.Class.getClassLoader`                            |
| `java.lang.Class.getClasses`                                |
| `java.lang.Class.getField(s)`                               |
| `java.lang.Class.getMethod(s)`                              |
| `java.lang.Class.getConstructor(s)`                         |
| `java.lang.Class.getDeclaredClasses`                        |
| `java.lang.Class.getDeclaredField(s)`                       |
| `java.lang.Class.getDeclaredMethod(s)`                      |
| `java.lang.Class.getDeclaredConstructor(s)`                 |
| `java.lang.ClassLoader.getParent`                           |
| `java.lang.ClassLoader.getSystemClassLoader`                |
| `java.lang.Thread.getContextClassLoader`                    |

**Non-Complaint Code:**

```
public class UntrustedClass
{ 
  public static void untrustedCode() {
     Date now = new Date();
     Class<?> dateClass = now.getClass();
     ExceptionExample.createInstance(dateClass);
    }
 }
public class ExceptionExample
{
    public static void createInstance(Class<?> dateClass)
    {
      try { // Create another Date object using the Date Class
            Object o = dateClass.newInstance();
            if (o instanceof Date) {
              Date d = (Date)o;
              System.out.println("The time is: " + d.toString());
             }
       }
       catch (InstantiationException ie) { System.out.println(ie.toString()); }
       catch (IllegalAccessException iae) { System.out.println(iae.toString()); }    	
    }
}

```

Do not accept Class, ClassLoader, or Thread instances from untrusted code or outside of your package. If inevitable, safely acquire these instances by ensuring they come from trusted sources. Additionally, make sure to discard tainted inputs from untrusted code. Likewise, objects returned by the affected methods should not be propagated back to the untrusted code.

**Compliant Code:**

```
public class UntrustedClass
{
 public static void untrustedCode() {
 Date now = new Date();
 ExceptionExample.createInstance(now);
 }
 }
public class ExceptionExample
{
 public static void createInstance(Date dateObject)
 {
 try {
 Date d = dateObject; // Create another Date object
 System.out.println("The time is: " + d.toString());
 }
 catch (IllegalAccessException iae) { System.out.println(iae.toString()); }
 }
}
```

**Risk Assessment**

Bypassing Security manager checks will seriously compromise the security of a Java application.

| **Risk Level:** | Medium |
| --------------- | ------ |

### **Denial of Service**

Input into a system should be checked so that it will not cause excessive resource consumption disproportionate to that used to request the service. Commonly affected resources are CPU cycles, memory, disk space, and file descriptors.

In rare cases, it may not be practical to ensure that the input is reasonable. It may be necessary to carefully combine resource checking with the logic of processing the data. In addition to attacks that cause excessive resource consumption, attacks that result in persistent DoS, such as wasting significant disk space, need to be defended against. Server systems should be especially robust against external attacks.

#### Beware of activities that may use disproportionate resources

Examples of attacks include:

* Requesting a large image size for vector graphics. For instance, SVG and font files.
* Integer overflow errors can cause sanity checking of sizes to fail.
* An object graph constructed by parsing a text or binary stream may have memory requirements many times that of the original data.
* "Zip bombs" whereby a short file is very highly compressed. For instance, ZIPs, GIFs and gzip encoded HTTP contents. When decompressing files, it is better to set limits on the decompressed data size rather than relying upon compressed size or meta-data.
* "Billion laughs attack" whereby XML entity expansion causes an XML document to grow dramatically during parsing. Set the XMLConstants.FEATURE\_SECURE\_PROCESSING feature to enforce reasonable limits.
* Causing many keys to be inserted into a hash table with the same hash code, turning an algorithm of around O(n) into O(n2).
* Regular expressions may exhibit catastrophic backtracking.
* XPath expressions may consume arbitrary amounts of processor time.
* Java deserialization and Java Beans XML deserialization of malicious data may result in unbounded memory or CPU usage.
* Detailed logging of unusual behavior may result in excessive output to log files.
* Infinite loops can be caused by parsing some corner case data. Ensure that each iteration of a loop makes some progress.

#### Release resources in all cases

Some objects, such as open files, locks, and manually allocated memory, behave as resources that require every acquire operation to be paired with a definite release. It is easy to overlook the vast possibilities for execution paths when exceptions are thrown. Resources should always be released promptly no matter what.

Even experienced programmers often handle resources incorrectly. In order to reduce errors, duplication should be minimized, and resource handling concerns should be separated. The Execute Around Method pattern provides an excellent way of extracting the paired acquire and release operations. The pattern can be used concisely using the Java SE 8 lambda feature.

**Non-Complaint Code:**

```
 long sum = readFileBuffered(InputStream in -> {
 long current = 0;
 for (;;) {
 int b = in.read();
 if (b == -1) {
 return current;
 }
 current += b;
 }
 });
```

**Complaint Code:**

```
public  R readFileBuffered(
    InputStreamHandler handler
        ) throws IOException {
            try (final InputStream in = Files.newInputStream(path)) {
                handler.handle(new BufferedInputStream(in));
            }
}
```

For resources without support for the enhanced feature, use the standard resource acquisition and release.

**Complaint Code:**

```
public  R locked(Action action) {
    lock.lock();
        try {
            return action.run();
        } finally {
            lock.unlock();
}

```

Ensure that any output buffers are flushed in the case that output was otherwise successful. If the flush fails, the code should exit via an exception.

**Complaint Code:**

```
public void writeFile(
		OutputStreamHandler handler
        ) throws IOException {
            try (final OutputStream rawOut = Files.newOutputStream(path)) {
                final BufferedOutputStream out =
                    new BufferedOutputStream(rawOut);
                handler.handle(out);
                out.flush();
            }
        }
    }
```

Some decorators of resources may themselves be resources that require correct release. For instance, in the current Oracle JDK implementation compression-related streams are natively implemented using the C heap for buffer storage. Care must be taken that both resources are released in all circumstances.

**Complaint Code:**

```
public void bufferedWriteGzipFile(
 OutputStreamHandler handler
 ) throws IOException {
  try (
   final OutputStream rawOut = Files.newOutputStream(path);
   final OutputStream compressedOut =
    new GzipOutputStream(rawOut);
   ) {
  final BufferedOutputStream out =
    new BufferedOutputStream(compressedOut);
  handler.handle(out);
  out.flush();
 }
 }
```

&#x20;Note, however, that in certain situations a try statement may never complete running (either normally or abruptly). For example, code inside of the try statement could indefinitely block while attempting to access a resource. If the try statement calls into untrusted code, that code could also intentionally sleep or block in order to prevent the clean-up code from being reached. As a result, resources used in a try-with-resources statement may not be closed, or code in a finally block may never be executed in these situations.

#### Resource limit checks should not suffer from integer overflow

The Java language provides bounds checking on arrays which mitigates the vast majority of integer overflow attacks. However, some operations on primitive integral types silently overflow. Therefore, take care when checking resource limits. This is particularly important on persistent resources, such as disk space, where a reboot may not clear the problem.

Some checking can be rearranged so as to avoid overflow. With large values, current + max could overflow to a negative value, which would always be less than max.

**Non-Complaint Code:**

```
private void checkGrowBy(long extra) {
  if (extra < 0 || current > max - extra) {
  throw new IllegalArgumentException();
   }
  }
 }
```

If performance is not a particular issue, a verbose approach is to use arbitrary-sized integers.

**Complaint Code:**

```
private void checkGrowBy(long extra) {
    BigInteger currentBig = BigInteger.valueOf(current);
    BigInteger maxBig = BigInteger.valueOf(max );
    BigInteger extraBig = BigInteger.valueOf(extra );
    if (extra < 0 ||
    currentBig.add(extraBig).compareTo(maxBig) > 0) {
    throw new IllegalArgumentException();
  }
 }
```

A peculiarity of two's complement integer arithmetic is that the minimum negative value does not have a matching positive value of the same magnitude. So, `Integer.MIN_VALUE == -Integer.MIN_VALUE, Integer.MIN_VALUE == Math.abs(Integer.MIN_VALUE)`and, for integer `a, a < 0` does not imply `-a > 0`. The same edge case occurs for `Long.MIN_VALUE`.

As of Java SE 8, the `java.lang.Math` class also contains methods for various operations (`addExact, multiplyExact, decrementExact`, etc.) that throw an _ArithmeticException_ if the result overflows the given type.

**Risk Assessment**.

| **Risk Level:** | High |
| --------------- | ---- |

### **Session Management/URL Authorization**

&#x20;Proper authentication and session management is critical to web application security. Flaws in this area most frequently involve the failure to protect credentials and session tokens through their lifecycle. These flaws can lead to the hijacking of user or administrative accounts, undermine authorization and accountability controls, and cause privacy violations

**Non-Complaint Code:**

```
public void login(string username, string password)
{
	HttpSession session = request.getSession (true);
//validate the username and password
  //redirect to login page upon unsuccessful validation
 //upon successful validation
Customer customerBean = (Customer)
session.setAttribute("CustomerBean", Customer);
}

```

Other JSP and controller servlets

```
public Bool isLoged(string username, string password)
{
 HttpSession session = request.getSession (true);
 Customer customerBean = (Customer)
 session.getAttribute('CustomerBean');
 if (customerBean == null) 
 {
  respoSpire.sendRedirect
  ("https://www.Spire.com/login.htm");
  return false;
 }
return true;
}
```

**Compliant Code:**

Every time a user logs in to the application for the first, create a new session Id for the user and invalidate any existing session IDs.

```
public void login(string username, string password)
{
 HttpSession session = request.getSession (true);
//validate the username and password
//redirect to login page upon unsuccessful validation
//upon successful validation
 if (session.isNew() == false) {
session.invalidate();
session = request.getSession(true);
}
 Customer customerBean = (Customer)
 session.setAttribute("CustomerBean", Customer);
}
```

```
public Bool isLoged(string username, string password)
{
 HttpSession session = request.getSession (true);
 Customer customerBean = (Customer)
 session.getAttribute('CustomerBean');
 if (customerBean == null)
 {
 respoSpire.sendRedirect
 ("https://www.Spire.com/login.htm");
 return false;
 }
return true;
}
```

Authorize the user before displaying any information to him. This can be accomplished by looking into the session for the object binded by the application to the user’s session.

If the cookie object is being set with various attributes apart from the session ID check the cookie is set only to transmit over HTTPS/SSL. In java, this is performed by the method

`cookie.setSecure()`

HTTPOnly cookie is meant to provide protection against XSS by not letting client-side script access the cookie. The HttpOnly property can be set on the JSESSIONID cookie as follows.

```
// Check if this is where the JSESSIONID is being set (assuming that JSESSIONID is the only cookie used)
if (respoSpire.containsHeader("SET-COOKIE"))
{
 String sessionid = request.getSession().getId();
 respoSpire.setHeader("SET-COOKIE", "JSESSIONID=" + sessionid + "; Path=/…..; HttpOnly");
}
// Continue down the Filter Chain
chain.doFilter(request, respoSpire);
```

In the scenario where custom cookies are being used, it can be set to HttpOnly, as follows:

```
respoSpire.setHeader("Set-Cookie", "originalcookiename=originalvalue; HTTPOnly");
```

Invalidate the session at the time of logout.

```
session.invalidate();
session = request.getSession(true);
session.setAttribute("userid",userid);
respoSpire.sendRedirect("login.jsp");
```

**Risk Assessment**

Session IDs help in identifying the user and maintaining his session. Hence it is important to have robust session management in place.

| **Risk Level:** | High |
| --------------- | ---- |

### **URL Redirects and Forwards**

Web applications frequently redirect and forward users to other pages and websites and use untrusted data to determine the destination pages. Without proper validation, attackers can redirect victims to phishing or malware sites, or use forwards to access unauthorized pages.

Un-validated redirects and forwards are possible when a web application accepts untrusted input that could cause the web application to redirect the request to a URL contained within untrusted input. By modifying untrusted URL input to a site, an attacker may successfully launch a phishing scam and steal user credentials.

As the server name in the modified link is identical to the original site, phishing attempts may have a more trustworthy appearance. Invalidated redirect and forward attacks can also be used to maliciously craft a URL that would pass the application’s access control check and then forward the attacker to privileged functions that they would normally not be able to access.

**Redirects**

Redirect functionality on a website allows a user’s browser to be told to go to a different page on the site. This can be done to improve the user interface or track how users are navigating the site.

To provide the redirect functionality a site may have a specific URL to perform the redirect:

**`http:// www.example.com/utility/redirect.cgi`**

This page will take a parameter (from URL or POST body) of ‘URL’ and will send back a message to the user’s browser to go to that page, for example:

**`http://www.example.com/utility/redirect.cgi?URL=http://www.example.com/viewtxn.html`**

However, this can be abused as an attacker can attempt to make a valid user click on a link that appears to be for www.example.com but which will invoke the redirect functionality on example.com to cause the users browser to go to a malicious site (one that could look like example.com and trick the user into entering sensitive or authentication information:

**`http://www.example.com/utiltiy/redirect cgi?URL=http://attacker.com/fakelogin.html`**

**Forwards**

Forwards are similar to redirects however the new page is not retrieved by the user’s browser (as occurred with the redirect) but instead the server framework will obtain the forwarded page and return it to the user’s browser. This is achieved by ‘forward’ commands within Java frameworks (e.g. Struts) or ‘Server.Transfer’ in .Net.

As the forward is performed by the server framework itself, it limits the range of URLs the attacker can exploit to the current website (i.e. attacker cannot ‘forward’ to attacker.com), however, this attack can be used to bypass access controls. For example, where a site sends the forwarded page in the response:

* If purchasing, forward to ‘purchase.do’
* If cancelling, forward to ‘cancelled.do’

This will then be passed as a parameter to the website:

**`http://www.example.com/txn/acceptpayment.html?FWD=purchase`**

If instead, an attacker used the forward to attempt to access a different page within the website, e.g. as the admin do, then they may access pages that they are not authorized to view, because authorization is being applied on the ‘acceptpayment’ page, instead of the forwarded page.

If any part of the URL being forwarded, or redirected, to is based on user input, then the site could be at risk.

**Redirects**

The following examples demonstrate unsafe redirect and forward code. The following Java code receives the URL from the ‘URL’ parameter and redirects to that URL.

**`response.sendRedirect(request.getParameter(“url”));`**

The above code is vulnerable to an attack if no validation or extra method controls are applied to verify the certainty of the URL. This vulnerability could be used as part of a phishing scam by redirecting users to a malicious site. If user input has to be used as part of the URL to be used, then apply strict validation to the input, ensuring it cannot be used for purposes other than intended.

_Note that vulnerable code does not need to explicitly call a ‘redirect’ function, but instead could directly modify the response to cause the client browser to go to the redirected page._

Where an attacker has posted a redirecting URL on a forum or sends in an e-mail, the website can check the referrer header to ensure the user is coming from a page within the site, although this countermeasure will not apply if the malicious URL is contained within the site itself.

Consider creating a whitelist of URLs or options that a redirect is allowed to go to or deny the ability for the user input to determine the scheme or hostname of the redirect. A site could also encode (or encrypt) the URL value to be redirected to such that an attacker cannot easily create a malicious URL parameter that, when unencoded (or unencrypted), will be considered valid.

**Forwards**

The countermeasure for forwards is to either whitelist the range of pages that can be forwarded to (similar to redirects) and to enforce authentication on the forwarded page as well as the forwarding page. This means that even if an attacker manages to force a forward to a page, they should not have access to, the authentication check on the forwarded page will deny them access.

**Note on J2EE**

There is a noted flaw related to the “sendRedirect” method in J2EE applications. For example:

**`response.sendRedirect(“home.html”);`**

This method is used to send a redirection response to the user who then gets redirected to the desired web component whose URL is passed an argument to the method. One such misconception is that execution flow in the Servlet/JSP page that is redirecting the user stops after a call to this method. Note that if there is code present after the ‘If’ condition it will be executed.

The fact that execution of a servlet or JSP continues even after sendRedirect() method, also applies to Forward method of the RequestDispatcher Class. However, \<jsp:forward> tag is an exception, it is observed that the execution flow stops after the use of \<jsp:forward> tag.

After issue, a redirect or forward, terminate code flow using a “return” statement.

**Risk Assessment**

| **Risk Level:** | High |
| --------------- | ---- |

### **Grant Only the Required Permission**

&#x20;The **java.security.AllPermission** class grants all possible permissions to the caller. This facility was included for routine testing purposes to make it less cumbersome to deal with a multitude of permissions or for use when the code is completely trusted. It should never be applied in the production environment unless it’s a trusted environment.

**Non-Complaint Code:**

```
/* grant the thirdpartylib library AllPermission */
grant codebase "file: ${ thirdpartylib.home}/j2ee/home/ thirdpartylib.jar" {
 permission java.security.AllPermission;
};
```

**Compliant Code:**

```
grant codeBase "file:${ thirdpartylib.home}/j2ee/home/ thirdpartylib.jar", signedBy "AppropriateUser" {
 permission java.io.FilePermission "/tmp/*", "read";
 permission java.io.SocketPermission "*", "connect";
};
} catch (SecurityException se) { System.out.println("Not allowed"); }
```

In the case of a trusted third-party/in-house developed library where they need the permission as similar to the application, provide the permission same as the user who runs the application. Do not provide more than what is required.

**Risk Assessment**

Granting **AllPermission** to **untrusted** production code means that there is no security at all.

| **Risk Level:** | High |
| --------------- | ---- |

### **Reflect Permission**

The suppressAccessChecks permission granted in the context of java.lang.reflect.ReflectPermission suppresses all standard Java language access checks when the permitted class tries to operate on public, default, protected or private members of another class. This implies that the permitted class can obtain permission to examine any field or invoke any method belonging to an arbitrary class.

**Non-Complaint Code:**

```
/* grant the thirdpartylib library AllPermission */
grant codebase "file:${ thirdpartylib.home}/j2ee/home/ thirdpartylib.jar" {
 permission java.lang.reflect.ReflectPermission "suppressAccessChecks";
};
```

**Compliant Code:**

```
grant codeBase "file:${ thirdpartylib.home}/j2ee/home/ thirdpartylib.jar", signedBy "AppropriateUser" {
 permission java.io.FilePermission "/tmp/*", "read";
 permission java.io.SocketPermission "*", "connect";
};
} catch (SecurityException se) { System.out.println("Not allowed"); }
```

**Risk Assessment**

Granting ReflectPermission with action suppressAccessChecks is dangerous because it allows normally inaccessible fields and methods to become available by using reflection.

| **Risk Level:** | High |
| --------------- | ---- |

### **Input Data Validation**

&#x20;Use a standard input validation mechanism to validate all input data for length, type, syntax, and business rules before accepting the data to be displayed or stored. Preferably use an "accept known good" validation strategy. Reject invalid input rather than attempting to sanitize potentially hostile data. Do not forget that error messages might also include invalid data.

Client-side input validation is easy to bypass. Client-side validation can be implemented to improve performance, should not be trusted. Hence all the input validation should happen at the server-side.

Following is the data validation strategy which needs to be followed.

* **Known Good** (Accept)

In accept the known-good approach, you only allow the characters that are required by the application to carry out its task. For e.g. Username field requires only alphanumeric characters and can have a length restriction of 15 chars.

**Non-Complaint Code :**

```
out.println(request.getParameter(“username”));
```

**Compliant Code :**

```
public class ValidatingHttpRequest {
 public ValidatingHttpRequest(HttpServletRequest request) {
 super(request);
 }
 public String getParameter(String name) {
 HttpServletRequest req = (HttpServletRequest) super.getRequest();
 return validate( name, req.getParameter( name ) );
 }
// This is a VERY restrictive pattern alphanumeric < 20 chars
 private Pattern pattern = Pattern.compile("^[a-zA-Z0-9]{0,20}$");
 private String validate( String name, String input ) throws ValidationException {
// important - always canonicalize before validating
 String canonical = canonicalize( input );
// check to see if input matches whitelist character set
 if ( !pattern.matcher( canonical ).matches() ) {
 throw new ValidationException( "Improper format in " + name + " field";
 }
 return sb.toString();
 }
}
```

* **Known Bad** (Reject)

If the business requirement is to allow the use of special characters in the application, then in this scenario the characters which can cause harm to your application should be mandatorily rejected.

The characters who are not supposed to pass through the application are:

`“`**`<`**`”, “`**`>`**`”, “`**`%`**`”, “`**`&`**`”, “`**`;`**`”, “`**`/`**`”, “`**`’`**`”, “`**`+`**`”, “`**`--`**`“, “`**`xp_`**`”`

**Risk Assessment**

Most of the scripting and injection attacks happen due to improper/no validation of the user-supplied input. Hence it is critical that all the user-supplied input or input that can be tampered with by the user (cookies, hidden fields, headers etc.) and is used by the application are subjected to strict data validation.

| **Risk Level:** | High |
| --------------- | ---- |

### **Injection and Inclusion**

A very common form of attack involves causing a particular program to interpret data crafted in such a way as to cause an unanticipated change of control. Typically, but not always, this involves text formats.

#### Generate valid formatting

Attacks using maliciously crafted inputs to cause incorrect formatting of outputs are well-documented [\[7\]](https://www.oracle.com/technetwork/java/seccodeguide-139067.html#ref-7). Such attacks generally involve exploiting special characters in an input string, incorrect escaping, or partial removal of special characters.

If the input string has a particular format, combining correction and validation is highly error-prone. Parsing and canonicalization should be done before validation. If possible, reject invalid data and any subsequent data, without attempting correction. For instance, many network protocols are vulnerable to cross-site POST attacks, by interpreting the HTTP body even though the HTTP header causes errors.

Use well-tested libraries instead of ad hoc code. There are many libraries for creating XML. Creating XML documents using raw text is error-prone. For unusual formats where appropriate libraries do not exist, such as configuration files, create classes that cleanly handle all formatting and only formatting code.

#### Avoid dynamic SQL

It is well known that dynamically created SQL statements including untrusted input are subject to command injection. This often takes the form of supplying an input containing a quote character (') followed by SQL. Avoid dynamic SQL.

For parameterized SQL statements using Java Database Connectivity (JDBC), use `java.sql.PreparedStatement` or `java.sql.CallableStatement` instead of `java.sql.Statement`. In general, it is better to use a well-written, higher-level library to insulate application code from SQL. When using such a library, it is not necessary to limit characters such as quote ('). If text destined for XML/HTML is handled correctly during output ([3.2.8.3](https://www.oracle.com/technetwork/java/seccodeguide-139067.html#3-3)), then it is unnecessary to disallow characters such as less than (<) in inputs to SQL.

**Non Complaint Solution:**

```
String sql = "Select * from Customer where CustomerID =’” +request.getParameter(“customerID”) +"’”;
String sql = request.getParameter("customerID");
PreparedStatement prepStmt = con.prepareStatement("SELECT * FROM Customer WHERE CustomerId = '+sql+'");
```

**Compliant Code:**

```
final String sql = "Select * from Customer where CustomerID =?";
final PreparedStatement ps = con.prepareStatement(sql);
ps.setString(1,customerID)
ResultSet rs = ps.executeQuery();
```

#### XML and HTML generation requires care

Untrusted data should be properly sanitized before being included in HTML or XML output. Failure to properly sanitize the data can lead to many different security problems, such as Cross-Site Scripting (XSS) and XML Injection vulnerabilities. It is important to be particularly careful when using Java Server Pages (JSP).

There are many different ways to sanitize data before including it in output. Characters that are problematic for the specific type of output can be filtered, escaped, or encoded. Alternatively, characters that are known to be safe can be allowed, and everything else can be filtered, escaped, or encoded. This latter approach is preferable, as it does not require identifying and enumerating all characters that could potentially cause problems.

Implementing correct data sanitization and encoding can be tricky and error-prone. Therefore, it is better to use a library to perform these tasks during HTML or XML construction.

#### Avoid any untrusted data on the command line

When creating new processes, do not place any untrusted data on the command line. Behavior is platform-specific, poorly documented, and frequently surprising.

External programs can be invoked from Java code using the exec() method of `java.lang.Runtime` class. As a result, a reference to the Process class is returned to the JVM. The exitValue() method can be used to observe the return value of the process.

Malicious data may, for instance, cause a single argument to be interpreted as an option (typically a leading - on Unix or / on Windows) or as two separate arguments. Any data that needs to be passed to the new process should be passed either as encoded arguments (e.g., Base64), in a temporary file, or through an inherited channel.

**Non Complaint Solution:**

```
// security manager check
String programName = System.getProperty("program.name");
if (programName != null){
 // runs user controlled program
 Runtime runtime = Runtime.getRuntime();
 Process proc = runtime.exec("/bin/sh " + programName);
}
```

**Compliant Code:**

```
process proc;
int filename = Integer.parseInt(System.getproperty("program.name")); // only allow integer choices
Runtime = Runtime.getRuntime();
switch(filename) {
 case 1: proc = runtime.exec("hardcoded\program1"); break; // option 1
 case 2: proc = runtime.exec("hardcoded\program2"); break; // option 2
 default: System.out.println("Invalid option!"); break;
}
```

#### Restrict XML inclusion

XML Document Type Definitions (DTDs) allow URLs to be defined as system entities, such as local files and HTTP URLs within the local intranet or localhost. XML External Entity (XXE) attacks insert local files into XML data which may then be accessible to the client. Similar attacks may be made using XInclude, the XSLT document function, and the XSLT import and include elements. The safest way to avoid these problems while maintaining the power of XML is to reduce privileges and to use the most restrictive configuration possible for the XML parser. Reducing privileges still allows you to grant some access, such as inclusion to pages from the same-origin website if necessary. XML parsers can also be configured to limit functionality based on what is required, such as disallowing external entities or disabling DTDs altogether.

Note that this issue generally applies to the use of APIs that use XML but are not specifically XML APIs.

**Non-Complaint Code:**

```
private void receiveXMLStream(InputStream is, DefaultHandler defHandler) {
  SAXParserFactory factory = SAXParserFactory.newInstance();
  try {
    SAXParser saxParser = factory.newSAXParser();
    saxParser.parse(is, defHandler);
  } catch (Throwable t) { /* Call custom exception handler */ }
}
// Default handler
class ErrorHandler extends DefaultHandler {
   private void report(SAXParseException s) {
      System.out.println(s.getLineNumber()+ ": " + s.getMessage()); // handle as required
   }
   public void warning(SAXParseException s) {
      report(s);
   }
   public void error(SAXParseException s) {
      report(s);
   }
   public void fatalError(SAXParseException s) throws SAXParseException {
      report(s);
      throw s;
   }
  /* May also contain usual parsing code (event handling) */
}

```

A valid XML statement will pass thru this server-level validation. Also, when there are two tags with the same tag name the SAX parser will override the old tag data with the latest. Even if this is not possible, the user can enter comments to bypass certain values and lot of other valid XML-based attacks can be performed.

**Compliant Code:**

```
private static void receiveXMLStream(InputStream inStream, DefaultHandler defHandler)
 throws ParserConfigurationException, SAXException, IOException {
 SchemaFactory sf = SchemaFactory.newInstance(XMLConstants.W3C_XML_SCHEMA_NS_URI);
 sf.setErrorHandler(new ErrorHandler());
 StreamSource ss = new StreamSource(new File("defaultschema.xsd"));
 Schema schema = sf.newSchema(ss);
 SAXParserFactory spf = SAXParserFactory.newInstance();
 spf.setSchema(schema);
 SAXParser saxParser = spf.newSAXParser();
 saxParser.parse(inStream, defHandler);
}
```

Likewise, when the Document Object Model (DOM) approach is used to parse XML structures, the DOM validation features of JAXP should be used.

#### Care with BMP files

BMP image files may contain references to local ICC (International Color Consortium) files. Whilst the contents of ICC files are unlikely to be interesting, the act of attempting to read files may be an issue. Either avoid BMP files or reduce privileges.

#### Disable HTML display in Swing components

Many Swing pluggable look-and-feel interpret the text in certain components starting with \<html> as HTML. If the text is from an untrusted source, an adversary may craft the HTML such that other components appear to be present or perform inclusion attacks.

To disable the HTML render feature, set the "`html.disable`" client property of each component to `Boolean.TRUE` (no other Boolean true instance will do).

`label.putClientProperty("html.disable", true);`

#### Take care interpreting untrusted code

Code can be hidden in a number of places. If the source is not trusted to supply code, then a secure sandbox must be constructed to run it in. Some examples of components or APIs that can potentially execute untrusted code include:

* Scripts run through the `javax.script` scripting API or similar.
* LiveConnect interfaces with JavaScript running in the browser. The JavaScript running on a web page will not usually have been verified with an object code signing certificate.
* By default, the Oracle implementation of the XSLT interpreter enables extensions to call Java code. Set the `javax.xml.XMLConstants.FEATURE_SECURE_PROCESSING` feature to disable it.
* Long Term Persistence of JavaBeans Components supports execution of Java statements.
* Java Sound will load code through the `javax.sound.midi.MidiSystem.getSoundbank` methods.
* RMI may allow the loading of remote code specified by remote connection. On the Oracle JDK, this is disabled by default but may be enabled or disabled through the  `java.rmi.server.useCodebaseOnly`  system property.
* LDAP (RFC 2713) allows the loading of remote code in a server response. On the Oracle JDK, this is disabled by default but may be enabled or disabled through the `com.sun.jndi.ldap.object.trustURLCodebase` system property.
* Many SQL implementations allow the execution of code with effects outside of the database itself.

#### Prevent injection of exceptional floating-point values

Working with floating-point numbers requires care when importing those from outside of a trust boundary, as the NaN (not a number) or infinite values can be injected into applications via untrusted input data, for example by conversion of (untrusted) Strings converted by the Double.valueOf method. Unfortunately, the processing of exceptional values is typically not immediately noticed without introducing sanitization code. Moreover, passing an exceptional value to an operation propagates the exceptional numeric state to the operation result.

Both positive and negative infinity values are possible outcomes of a floating-point operation when results become too high or too low to be representable by the memory area that backs a primitive floating-point value. Also, the exceptional value NaN can result from dividing 0.0 by 0.0 or subtracting infinity from infinity.

The results of casting propagated exceptional floating-point numbers to short, integer, and long primitive values that need special care, too. This is because an integer conversion of a NaN value will result in a 0, and a positive infinite value is transformed to `Integer.MAX_VALUE`(or `Integer.MIN_VALUE` for negative infinity), which may not be correct in certain use cases.

There are distinct application scenarios where these exceptional values are expected, such as scientific data analysis which relies on numeric processing. However, it is advised that the result values be contained for that purpose in the local component. This can be achieved by sanitizing any floating-point results before passing them back to the generic parts of an application.

As mentioned before, the programmer may wish to include sanitization code for these exceptional values when working with floating-point numbers, especially if related to authorization or authentication decisions or forwarding floating-point values to JNI. The `Double` and `Float` classes help with sanitization by providing the `isNan` and `isInfinite` methods. Also, keep in mind that comparing instances of `Double`. `NaN` via the equality operator always results to be false, which may cause lookup problems in maps or collections when using the equality operator on a wrapped double field within the equals method in a class definition.

A typical code pattern that can block further processing of unexpected floating-point numbers is shown in the following example snippet.

```
if (Double.isNaN(untrusted_double_value)) {
 // specific action for non-number case
 }
 if (Double.isInfinite(untrusted_double_value)){
 // specific action for infinite case
 }
 // normal processing starts here
```

**Risk Assessment**

Injection flaws occur when user-supplied data is sent to an interpreter as part of a command or a particular query. Attackers trick the interpreter into executing unintended commands via supplying specially crafted data. Injection flaws allow attackers to create, read, update, or delete any arbitrary data available to the application. In the worst-case scenario, these flaws allow an attacker to completely compromise the application and the underlying systems, even bypassing deeply nested firewalled environments.

The purpose of the command injection attack is to inject and execute commands specified by the attacker in the vulnerable application. In a situation like this, the application, which executes unwanted system commands, is like a pseudo system shell, and the attacker may use it as any authorized system user.

Failing to validate XML user input may result in information disclosure and in certain cases, provides the ability to falsify the business logic.

| **Risk Level:** | High |
| --------------- | ---- |

### **Cross-Site Request Forgery**

A CSRF attack forces a logged-on victim’s browser to send a request to a vulnerable web application, which then performs the chosen action on behalf of the victim. Any application that accepts HTTP requests from an authenticated user without having some control to verify that the HTTP request is unique to the user’s session. Nearly all web applications!! is vulnerable to CSRF attacks. A session ID is not in scope here as the rogue HTTP request shall also contain a valid session ID as the user is authenticated already.

* A unique id is generated upon a login. The unique Id could be derived from a secure random generator such as Secure Random for J2EE. The unique id is stored in a unique random named attribute, which is also generated at runtime. This key-value pair will be stored in the user’s session.
* The attribute name of this unique id is stored in an attribute called SessionState. The SessionState attribute will be stored in the user’s session.
* A unique Id is appended to each link/form on the requested page prior to being displayed to the user. Usually, it will be stored as one of the hidden parameters.
* Upon every request the application checks if the unique Id passed with the HTTP request is valid for a given request by validating against the user’s session.
* If the unique ID is not present terminate the user session, display an error to the user.

**Risk Assessment**

CSRF vulnerability is very widespread across web applications. For critical applications or transactions, this flaw should be taken care of by providing an extra level of confirmation or password.

| **Risk Level:** | Medium |
| --------------- | ------ |

### **Do-not Use URL Class**

The concept of virtual hosting allows a web server to host multiple websites on the same computer, sometimes sharing the same IP address. Unfortunately, when the URL class was designed, this technique was unperceived. As a result, two completely different URLs that resolve to the same IP address always compare equally. Also, the URI class also performs normalization of the URL which would eliminate any directory attacks.

**Non Complaint Solution:**

```
import java.net.*;
public class Filter {
 public static void canIAllow(String website) throws MalformedURLException {
 final URL allowed = new URL("http://Spire.com");
 if(allowed.equals(new URL(website))) {
 System.out.println("URL OK, proceed!");
 }else {
 System.out.println("URL blocked");
 }
 }
}
```

**Compliant Code:**

```
import java.net.*;
public class Filter {
 public static void canIAllow(String website) throws MalformedURLException {
 final URI allowed = new URI("http://Spire.com");
 if(allowed.equals(new URL(website))) {
 System.out.println("URL OK, proceed!");
 }else {
 System.out.println("URL blocked");
 }
 }
}
```

**Risk Assessment**

Allowing a URL without checking the validity and access will allow an attacker to exploit it.

| **Risk Level:** | Medium |
| --------------- | ------ |

### **Conflict in Atomicity**

Do not escalate a privilege and perform an action without knowing the caller’s permissions.

The static method doPrivileged() is used to affirm that the invoking method is taking responsibility for exercising its own permissions and that the access permissions of its callers should be ignored. For example, an application may have permissions to operate on a sensitive file; however, a caller of this application may be allowed to operate with only basic user permissions. Invoking doPrivileged() in the context of this method allows it to exercise its own (possibly elevated) permissions under such circumstances.

**Non-Complaint Code:**

```
public static FileInputStream openPasswordFile(String password_file) throws FileNotFoundException {
 //Declare as final and assign before the body of the anonymous inner class
 //Array f[] is used to maintain language semantics while using final
 final FileInputStream f[]={null};
 final String file = password_file;
 //Use own privilege to open the sensitive password file
 AccessController.doPrivileged(new PrivilegedAction() {
 public Object run() {
 try {
 f[0] = new FileInputStream("c:\\" + file); //Perform privileged action
 }catch(FileNotFoundException cnf) { System.err.println(cnf.getMessage()); }
 return null; //Still mandatory to return from run()
 }
 }
 return f[0]; //Returns a reference to privileged objects (inappropriate)
 }
```

The file is opened in a special privileged mode and the file pointer is returned. This is dangerous and the person who gets this reference can accomplish any privileged task.

**Compliant Code:**

Now the new code is changed to perform an action rather than returning a reference of the file. Now the privileged action takes place inside the function call and the lifetime of any critical resource used is encapsulated inside the class. Now nobody could call openpasswordfile() rather they will call the changePassword(). This will make sure, the untrusted applications cannot call

```
public static void changePassword() {
 //Use own privilege to open the sensitive password file
 final String password_file = "password";
 final FileInputStream f[] = {null};
 AccessController.doPrivileged(new PrivilegedAction() {
 public Object run() {
 try {
 f[0] = openPasswordFile(password_file); //call the privileged method here
 }catch(FileNotFoundException cnf) { System.err.println("Error: Operation could not be performed"); }
 return null;
 }
 });
 //Perform other operations such as password verification
 }
 private static FileInputStream openPasswordFile(String password_file) throws FileNotFoundException {
 FileInputStream f = new FileInputStream("c:\\" + password_file);
 //Perform read/write operations on password file
 return f;
 }
```

**Risk Assessment**

Elevating a privilege or returning a reference should be controlled within the scope of the object or package. If left uncontrolled, they can potentially endanger the system and provide a valid platform for the attackers to exploit the machine.

| **Risk Level:** | High |
| --------------- | ---- |

**Restrict Accessibility**

Classes and class members (classes, interfaces, fields, and methods) are subject to access control. The access is indicated by an access modifier: public, protected, private, or the absence of an access modifier (the default access). A simplified view of the access control rules is summarized in the following table. An 'x' conveys that the particular access is permitted from within that domain.

| Access Specifier | Class | Package | Sub-Class | World |
| ---------------- | ----- | ------- | --------- | ----- |
| Private          | x     |         |           |       |
| None             | x     | X       |           |       |
| Protected        | x     | X       | x         |       |
| Public           | x     | X       | x         | x     |

**Non-Complaint Code:**

```
public class PublicClass {
 public int x;
 public int y;
 public void getPoint() {
 System.out.println("(" + x + "," + y + ")");
 }
}
```

**Compliant Code:**

```
final class PrivateClass {
 private int x;
 private int y;
 private void getPoint() { //private constructor
 System.out.println("(" + x + "," + y + ")");
 }
}
```

| **APIs that should be used with care/to be avoided**                 |
| -------------------------------------------------------------------- |
| `java.lang.Class.newInstance`                                        |
| `java.lang.reflect.Constructor.newInstance`                          |
| `java.lang.reflect.Field.get*`                                       |
| `java.lang.reflect.Field.set*`                                       |
| `java.lang.reflect.Method.invoke`                                    |
| `java.util.concurrent.atomic.AtomicIntegerFieldUpdater.newUpdater`   |
| `java.util.concurrent.atomic.AtomicLongFieldUpdater.newUpdater`      |
| `java.util.concurrent.atomic.AtomicReferenceFieldUpdater.newUpdater` |

**Risk Assessment**

Performing access checks against the immediate caller, instead of against each caller in the execution sequence, may seriously compromise the security of a java application.

| **Risk Level:** | Medium |
| --------------- | ------ |

### **Limit the extensibility of the classes and methods**

A nonfinal class or method that is not meant to be inherited can be overridden by an attacker if it is not declared as final. If inheritance is to be limited to trusted implementations for a public, nonfinal class, then the class type should be confirmed before creating the instance at each place where an instance of the nonfinal class can be created. A Security Manager check should be enforced on detecting a subclass.

A nonfinal class can be subverted simply by declaring a malicious class that inherits from the nonfinal class, which implies that there is no need for reflection. However, reflection is necessary if the nonfinal class is private or otherwise inaccessible to the attacker.

**Non-Complaint Code:**

```
class BankOperation
{
// bank details
}
//This class has been written by the attacker
public class SubClass extends BankOperation
{
 public void getBalance() {
 //get the balance and transfer money to attackers account
 }
}
```

**Compliant Code:**

```
final class BankOperation
{
// bank details
}
```

**Risk Assessment**

Allowing a nonfinal class or method to be inherited without checking the class instances allows an attacker to exploit it.

| **Risk Level:** | High |
| --------------- | ---- |

### **Error Handling**

Applications frequently generate error messages and display them to users. Many times, these error messages are quite useful to attackers, as they reveal implementation details or information that is useful in exploiting a vulnerability. There are several common examples of this:

Detailed error handling, where inducing an error displays too much information, such as stack traces, failed SQL statements, or other debugging information

It must be ensured that the end-users receive a generic error message.

For e.g. (“**Error occurred, try again**”).

**Non-Complaint Code:**

```
try
{
 ------------------
}
catch(Exception e)
{
e.printStackTrace();
}
```

**Compliant Code:**

```
try
{
 ------------------
}
catch(Exception e)
{
Console.WriteLine("An error occurred”);
logerror(“Error: “, e);
}
finally
{
 if (object ! = null)
 object.close(); //release the resources
}
```

**Risk Assessment**

Detailed error messages help in gathering more information related to the underlying resources used by the application.

| **Risk Level:** | High |
| --------------- | ---- |

### **Audit Log**

Applications should always maintain audit logs. These logs have valuable information such as the users, their actions, and workflow. This log can later be used for various purposes like determining the cause of a particular problem, performing an audit, identifying potential fraud or anomalies, and performing forensic analysis.

Activities that should be logged in the audit logs.

* Login Success or failure with the username
* Profile changes and what content was changed
* All transactions with transaction number (critical transactions)
* Password resets
* Change of address
* Changes to the sensitive data.
* Admin user’s activities must be logged
* Server-side validation failures
* All privileged actions

Use the following format for the audit log.

`TIMESTAMP IPADDRESS HOSTNAME APP-NAME MODULENAME PRIORITY SYSTEM-USER APPLICATION-USER MSGID [SD-ID]s MSG`

**Risk Assessment**

Maintaining audit logs helps in tracing back details of a transaction or event at a later point in time.

| **Risk Level:** | High |
| --------------- | ---- |

### **Native Codes**

Native methods are defined in Java and written in traditional languages such as C/C++ (see \[[JNI 06](https://www.securecoding.cert.org/confluence/display/java/AA.+Java+References#AA.JavaReferences-JNI06)]). The added extensibility comes at the cost of flexibility and portability as the code no longer conforms to the policies enforced by Java.

**Compliant Code:**

It is recommended not to use native methods.

**Risk Assessment**

Allowing native methods to be called directly by trusted/untrusted code may seriously compromise the security of a Java application.

| **Risk Level:** | High |
| --------------- | ---- |

### **ByteCode Verifier**

The bytecode verifier is an internal component of the JVM and is responsible for detecting non-confirming Java code. It performs tasks such as ensuring that the class file is in the proper format, illegal type casts are not performed and preventing operand stack overflows or underflows.

**Non-Complaint Code:**

```
package creditvault.values;
public class CreditCard {
 private String creditcard = "1234 1201 1234 0001";
 public getCreditCard()
 {
 Return creditcard
 }
}
package creditvault.values;
public class CreditVerify {
 public static void main(String[] args) {
 CreditCard number = new CreditCard ();
 System.out.println("Please enter your creditcard no:");
 //perform verification
 }
}
```

**Compliant Code:**

```
Java -verify <applilcation> or use -Xverify:all flag
```

_This is not required on Java 2.0 and above as the bytecode is verified by default._

**Risk Assessment**

If the bytecode verifier is not applied to all code, then code could be loaded into a java system that does not conform to the Java Language Specification. This code could bypass checks that are normally expected to be performed by Java code, thereby compromising security.

| **Risk Level:** | Medium |
| --------------- | ------ |
