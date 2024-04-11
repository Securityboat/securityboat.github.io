# **Dorking** 

## **Common**
- `inurl /bug bounty` 
- `inurl : / security` 
- `inurl:security.txt` 
- `inurl:security "reward"` 
- `inurl : /responsible disclosure` 
- `inurl : /responsible-disclosure/ reward` 
- `inurl : / responsible-disclosure/ swag` 
- `inurl : / responsible-disclosure/ bounty` 
- `inurl:'/responsible disclosure' hoodie` 
- `responsible disclosure swag r=h:com` 
- `responsible disclosure hall of fame` 
- `responsible disclosure europe` 
- `responsible disclosure white hat` 
- `white hat program` 
- `insite:"responsible disclosure" -inurl:nl` 
- `intext responsible disclosure` 
- `site eu responsible disclosure` 
- `site .nl responsible disclosure` 
- `site responsible disclosure` 
- `responsible disclosure:sites` 
- `responsible disclosure r=h:nl` 
- `responsible disclosure r=h:uk` 
- `responsible disclosure r=h:eu` 
- `responsible disclosure bounty r=h:nl` 
- `responsible disclosure bounty r=h:uk` 
- `responsible disclosure bounty r=h:eu` 
- `responsible disclosure swag r=h:nl` 
- `responsible disclosure swag r=h:uk` 
- `responsible disclosure swag r=h:eu` 
- `responsible disclosure reward r=h:nl` 
- `responsible disclosure reward r=h:uk` 
- `responsible disclosure reward r=h:eu` 
- `"powered by bugcrowd" -site:bugcrowd.com` 
- `"powered by hackerone" "submit vulnerability report"` 
- `"submit vulnerability report"` 
- `site:responsibledisclosure.com` 
- `inurl:'vulnerability-disclosure-policy' reward` 
- `intext:Vulnerability Disclosure site:nl` 
- `intext:Vulnerability Disclosure site:eu` 
- `site:*.*.nl intext:security report reward` 
- `site:*.*.nl intext:responsible disclosure reward` 
- `"security vulnerability" "report"` 
- `inurl"security report"` 
- `"responsible disclosure" university` 
- `inurl:/responsible-disclosure/ university` 
- `buy bitcoins "bug bounty"` 
- `inurl:/security ext:txt "contact"` 
- `"powered by synack"` 
- `intext:responsible disclosure bounty` 
- `inurl: private bugbountyprogram` 
- `inurl:/.well-known/security ext:txt` 
- `inurl:/.well-known/security ext:txt intext:hackerone` 
- `inurl:/.well-known/security ext:txt -hackerone -bugcrowd -synack -openbugbounty` 
- `inurl:reporting-security-issues` 
- `inurl:security-policy.txt ext:txt` 
- `site:*.*.* inurl:bug inurl:bounty` 
- `site:help.*.* inurl:bounty` 
- `site:support.*.* intext:security report reward` 
- `intext:security report monetary inurl:security ` 
- `intext:security report reward inurl:report` 
- `site:security.*.* inurl: bounty` 
- `site:*.*.de inurl:bug inurl:bounty` 
- `site:*.*.uk intext:security report reward` 
- `site:*.*.cn intext:security report reward` 
- `"vulnerability reporting policy"` 
- `"van de melding met een minimum van een" -site:responsibledisclosure.nl` 
- `inurl:/security ext:txt "contact"` 
- `inurl:responsible-disclosure-policy` 
- `"Submission Form powered by Bugcrowd" -bugcrowd.com` 
- `"If you believe you've found a security vulnerability"` 
- `intext:"BugBounty" and intext:"BTC" and intext:"reward"` 
- `intext:bounty inurl:/security` 
- `inurl:"bug bounty" and intext:"€" and inurl:/security` 
- `inurl:"bug bounty" and intext:"$" and inurl:/security` 
- `inurl:"bug bounty" and intext:"INR" and inurl:/security` 
- `inurl:/security.txt "mailto*" -github.com  -wikipedia.org -portswigger.net -magento` 
- `site:http://codepad.co "company"` 
- `site:http://scribd.com "company"` 
- `site:http://npmjs.com "company"` 
- `site:http://npm.runkit.com "company"` 
- `site:http://libraries.io "company"` 
- `site:http://ycombinator.com "company"` 
- `site:http://coggle.it "company"` 
- `site:http://papaly.com "company"` 
- `site:http://google.com "company"` 
- `site:http://trello.com "company"` 
- `site:http://prezi.com "company"` 
- `site:http://jsdelivr.net "company"` 
- `site:http://codepen.io "company"` 
- `site:http://codeshare.io "company"` 
- `site:http://sharecode.io "company"` 
- `site:http://pastebin.com "company"` 
- `site:http://repl.it "company"` 
- `site:https://lnkd.in/dMqN_2B "company"` 
- `site:http://gitter.im "company"` 
- `site:http://bitbucket.org "company"` 
- `site:*.atlassian.net "company"` 
- `site:atlassian.net "company"` 
- `inurl:gitlab "company"` 

# **Github Dorks and Recon** #

| Dork                                            | Description                                                                                 |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------- |
| root\_password                                  | root\_password                                                                              |
| redis\_password                                 | redis\_password                                                                             |
| bucket\_password                                | bucket\_password                                                                            |
| secret\_access\_key                             | secret\_access\_key                                                                         |
| access\_key                                     | access\_key                                                                                 |
| dbuser                                          | db user                                                                                     |
| dbpassword                                      | db password                                                                                 |
| “Company” config                                | “Company” pwd                                                                               |
| “Company” token                                 | “Company” ftp                                                                               |
| “Company” credentials                           | “Company” login                                                                             |
| “Company” secret                                | “Company” pass                                                                              |
| “Company” password                              | “Company” key                                                                               |
| “Company” send\_keys or send,keys               | If other keywords related to passwords failed                                               |
| “Company” ssh2\_auth\_password                  | Unauthorized Access to Servers                                                              |
| “Company” JDBC                                  | Database Credentials                                                                        |
| “Company” connectionstring                      | Database Credentials                                                                        |
| “Company” security\_credentials                 | LDAP ( active directory)                                                                    |
| filename:.npmrc \_auth                          | npm registry authentication data                                                            |
| filename:.dockercfg auth                        | docker registry authentication data                                                         |
| extension:pem private                           | private keys                                                                                |
| extension:ppk private                           | puttygen private keys                                                                       |
| filename:id\_rsa or filename:id\_dsa            | private ssh keys                                                                            |
| extension:sql mysql dump                        | mysql dump                                                                                  |
| extension:sql mysql dump password               | mysql dump look for password; you can try varieties                                         |
| filename:credentials aws\_access\_key\_id       | might return false negatives with dummy values                                              |
| filename:.s3cfg                                 | might return false negatives with dummy values                                              |
| filename:wp-config.php                          | wordpress config files                                                                      |
| filename:.htpasswd                              | htpasswd files                                                                              |
| filename:.env DB\_USERNAME NOT homestead        | laravel .env (CI, various ruby based frameworks too)                                        |
| filename:.env MAIL\_HOST=smtp.gmail.com         | gmail smtp configuration (try different smtp services too)                                  |
| filename:.git-credentials                       | git credentials store, add NOT username for more valid results                              |
| PT\_TOKEN language:bash                         | pivotaltracker tokens                                                                       |
| filename:.bashrc password                       | search for passwords, etc. in .bashrc (try with .bash\_profile too)                         |
| filename:.bashrc mailchimp                      | variation of above (try more variations)                                                    |
| filename:.bash\_profile aws                     | aws access and secret keys                                                                  |
| rds.amazonaws.com password                      | Amazon RDS possible credentials                                                             |
| extension:json api.forecast.io                  | try variations, find api keys/secrets                                                       |
| extension:json mongolab.com                     | mongolab credentials in json configs                                                        |
| extension:yaml mongolab.com                     | mongolab credentials in yaml configs (try with yml)                                         |
| jsforce extension:js conn.login                 | possible salesforce credentials in nodejs projects                                          |
| SF\_USERNAME salesforce                         | possible salesforce credentials                                                             |
| filename:.tugboat NOT \_tugboat                 | Digital Ocean tugboat config                                                                |
| HEROKU\_API\_KEY language:shell                 | Heroku api keys                                                                             |
| HEROKU\_API\_KEY language:json                  | Heroku api keys in json files                                                               |
| filename:.netrc password                        | netrc that possibly holds sensitive credentials                                             |
| filename:\_netrc password                       | netrc that possibly holds sensitive credentials                                             |
| filename:hub oauth\_token                       | hub config that stores github tokens                                                        |
| filename:robomongo.json                         | mongodb credentials file used by robomongo                                                  |
| filename:filezilla.xml Pass                     | filezilla config file with possible user/pass to ftp                                        |
| filename:recentservers.xml Pass                 | filezilla config file with possible user/pass to ftp                                        |
| filename:config.json auths                      | docker registry authentication data                                                         |
| filename:idea14.key                             | IntelliJ Idea 14 key, try variations for other versions                                     |
| filename:config irc\_pass                       | possible IRC config                                                                         |
| filename:connections.xml                        | possible db connections configuration, try variations to be specific                        |
| filename:express.conf path:.openshift           | openshift config, only email and server thou                                                |
| filename:.pgpass                                | PostgreSQL file which can contain passwords                                                 |
| filename:proftpdpasswd                          | Usernames and passwords of proftpd created by cpanel                                        |
| filename:ventrilo\_srv.ini                      | Ventrilo configuration                                                                      |
| \[WFClient] Password= extension:ica             | WinFrame-Client infos needed by users to connect toCitrix Application Servers               |
| filename:server.cfg rcon password               | Counter Strike RCON Passwords                                                               |
| JEKYLL\_GITHUB\_TOKEN                           | Github tokens used for jekyll                                                               |
| filename:.bash\_history                         | Bash history file                                                                           |
| filename:.cshrc                                 | RC file for csh shell                                                                       |
| filename:.history                               | history file (often used by many tools)                                                     |
| filename:.sh\_history                           | korn shell history                                                                          |
| filename:sshd\_config                           | OpenSSH server config                                                                       |
| filename:dhcpd.conf                             | DHCP service config                                                                         |
| filename:prod.exs NOT prod.secret.exs           | Phoenix prod configuration file                                                             |
| filename:prod.secret.exs                        | Phoenix prod secret                                                                         |
| filename:configuration.php JConfig password     | Joomla configuration file                                                                   |
| filename:config.php dbpasswd                    | PHP application database password (e.g., phpBB forum software)                              |
| path:sites databases password                   | Drupal website database credentials                                                         |
| shodan\_api\_key language:python                | Shodan API keys (try other languages too)                                                   |
| filename:shadow path:etc                        | Contains encrypted passwords and account information of new unix systems                    |
| filename:passwd path:etc                        | Contains user account information including encrypted passwords of traditional unix systems |
| extension:avastlic                              | Contains license keys for Avast! Antivirus                                                  |
| extension:dbeaver-data-sources.xml              | DBeaver config containing MySQL Credentials                                                 |
| filename:.esmtprc password                      | esmtp configuration                                                                         |
| extension:json googleusercontent client\_secret | OAuth credentials for accessing Google APIs                                                 |
| HOMEBREW\_GITHUB\_API\_TOKEN language:shell     | Github token usually set by homebrew users                                                  |
| xoxp OR xoxb                                    | Slack bot and private tokens                                                                |
| .mlab.com password                              | MLAB Hosted MongoDB Credentials                                                             |
| filename:logins.json                            | Firefox saved password collection (key3.db usually in same repo)                            |
| filename:CCCam.cfg                              | CCCam Server config file                                                                    |
| msg nickserv identify filename:config           | Possible IRC login passwords                                                                |
| filename:settings.py SECRET\_KEY                | Django secret keys (usually allows for session hijacking, RCE, etc)                         |

## **Google Dorking**

* **site:** This operator restricts results to pages within a specified website or domain. For example, "site:wikipedia.org" will only return results from Wikipedia.

* **intitle:** This operator searches for pages that have a specific word or phrase in the title For example, "intitle:Google Dorking" will return pages with "Google Dorking" in the title.

* **filetype:** This operator limits results to specific file types. For example "filetype:pdf" will only return PDF files.

* **inurl:** This operator searches for a specific word or phrase within the URL. For example, "inurl:login" will return pages with "login" in the URL.

* **related:** This operator finds sites related to a specified URL. For example, "related:example.com" will return websites similar to example.com.

* **cache:** This operator displays the Google cached version of a webpage. For example, "cache:example.com" will show Google's cached version of example.com.

## **Shodan**
* **port:** Identifies devices based on specific open ports.
* **hostname:** Filters devices based on their hostname.
* **country:** Narrows down results by specifying a country.
* **product:** Searches for devices based on the product or software running on them.
* **os:** Identifies devices based on their operating system.
* **city:** Filters results by specifying a city.
* **after:** Finds devices that were indexed after a specific date.
* **before:** Finds devices that were indexed before a specific date.
* **ssl:** Identifies devices with SSL certificates.
* **http.component:** Searches for devices based on specific HTTP components.
* **org:** Filters results to devices associated with a specific organization.
* **has_screenshot:** Identifies devices with available screenshots.
* **net:** Searches within a specific IP range.
* **isp:** Filters devices belonging to a specific Internet Service Provider.
* **title:** Searches for devices with specific content in the HTML title tag.

## **References**

- [Bugcrowd University - GitHub Recon and Sensitive Data Exposure](../attachments/Bugcrowd_University-GitHub_Recon_and_Sensitive_Data_Exposure.pdf)

- [http://10degres.net/github-tools-collection/](http://10degres.net/github-tools-collection/)

- [https://github.com/gwen001/github-search](https://github.com/gwen001/github-search)

- [https://dorks.faisalahmed.me/#](https://dorks.faisalahmed.me/#)

- [https://medium.com/bugbountywriteup/using-shodan-better-way-b40f330e45f6](https://medium.com/bugbountywriteup/using-shodan-better-way-b40f330e45f6)