# **Searching for Code in Classic ASP**

**General Strings**

Input APIs in ASP are commonly used to retrieve the input from the request, therefore code review should ensure these requests (and dependent logic) cannot be manipulated by an attacker. Output APIs are used by ASP to write the response body that will be sent to the end user, hence code review should check these requests are used in a proper manner and no sensitive information can be returned. Cookies can also be a source of information leakage.

| **STRING TO SEARCH** |                      |              |                         |
| -------------------- | -------------------- | ------------ | ----------------------- |
| Request              | Request.QueryString  | Request.Form | Request.ServerVariables |
| Query\_String        | hidden               | include      | .inc                    |
| Response.Write       | Response.BinaryWrite | <%=          | .cookies                |

**Error Handling**

Ensure errors in an application are handled properly, otherwise an attacker could use error conditions to manipulate the application.

| **STRING TO SEARCH** |                     |                      |                 |
| -------------------- | ------------------- | -------------------- | --------------- |
| err.                 | Server.GetLastError | On Error Resume Next | On Error GoTo 0 |

**Information in URL**

These APIs are used to extract information from the URL object in the request. Code review should check that the information extracted from the URL is sanitized.

| **STRING TO SEARCH** |                  |              |                 |
| -------------------- | ---------------- | ------------ | --------------- |
| location.href        | location.replace | method=”GET” | On Error GoTo 0 |

**Database**

These APIs can be used to interact with a database, which can lead to SQL attacks. Code review can check these API calls use sanitized input.

| **STRING TO SEARCH** |             |             |             |
| -------------------- | ----------- | ----------- | ----------- |
| commandText          | select from | update      | insert into |
| delete from where    | IRowSet     | execute     | .execute    |
| .open                | ADODB.      | Commandtype | ICommand    |

**Session**

These API calls can control session within ASP applications.

| **STRING TO SEARCH** |                 |                   |   |
| -------------------- | --------------- | ----------------- | - |
| session.timeout      | session.abandon | session.removeall |   |

**DOS Prevention & Logging**

The following ASP APIs can help prevent DOS attacks against the application. Leaking information to a log can be of use to an attacker, hence the following API call can be checked in code review to ensure no sensitive information is being written to logs.

| **STRING TO SEARCH** |                   |            |   |
| -------------------- | ----------------- | ---------- | - |
| server.ScriptTimeout | IsClientConnected | WriteEntry |   |

**Redirection**

Do not allow attacker input to control when and where rejection occurs.

| **STRING TO SEARCH** |                       |                   |                 |
| -------------------- | --------------------- | ----------------- | --------------- |
| Response.AddHeader   | Response.AppendHeader | Response.Redirect | Response.Status |
| Response.StatusCode  | Server.Transfer       | Server.Execute    |                 |
