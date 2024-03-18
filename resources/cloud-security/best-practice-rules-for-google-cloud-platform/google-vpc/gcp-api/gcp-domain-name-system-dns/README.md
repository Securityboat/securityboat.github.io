# GCP Domain Name System (DNS)

### What is DNS ?

DNS refers to the Domain Name System (DNS) service. DNS is a crucial component of the internet that translates human-readable domain names (like google.com) into the numerical IP addresses that computers use to identify each other and communicate.

### What is DNSSEC?

* DNSSEC (Domain Name System Security Extensions) is a security protocol that adds a layer of authentication and integrity to the Domain Name System (DNS).
* DNSSEC helps to prevent DNS spoofing and other attacks that rely on modifying or faking DNS data, thereby increasing the security and reliability of the internet. However, not all domains have implemented DNSSEC, and it requires support from both the domain owner and the DNS resolver used by the client.

Now let's see some misconfigurations in GCP DNS.

### 1 ) Check for DNSSEC Key-Signing Algorithm in Use

To follow security best practices, do not use the RSASHA1 signature algorithm for DNSSEC signing unless it is required for compatibility reasons, as SHA1 is considered weak and vulnerable to collision attacks.

To determine the type of DNSSEC Key-Signing Key algorithm configured for your Domain Name System (DNS) managed zones, perform the following operations:

1. Run _**projects list**_ command  with custom query filters to list the ID of each project available in your Google Cloud account:

```
gcloud projects list  --format="table(projectId)"
```

2. The command output should return the requested GCP project identifiers (IDs):

```
PROJECT_ID
cc-web-project-123456
cc-backend-app-112233
```

3. Run **dns managed-zones list** command  using the ID of the GCP project that you want to examine as identifier parameter and custom filtering to describe the name and the visibility of each DNS managed zone created for the selected project:

```
gcloud dns managed-zones list  --project cc-web-project-123456  --format="table(name,visibility)"
```

4. The command output should return the requested Google Cloud DNS zone metadata:

```
NAME                        VISIBILITY
cloudconformity-dns-zone    public
cloudrealisation-dns-zone   public
```

5. Run **dns managed-zones describe** command  using the name of the public DNS managed zone that you want to examine as identifier parameter and custom query filters to describe the DNSSEC feature configuration available for the selected DNS zone:

```
gcloud dns managed-zones describe cloudconformity-dns-zone --format="json(dnssecConfig)"
```

6. The command output should return the requested configuration information in JSON format:

```
{
  "dnssecConfig": {
    "defaultKeySpecs": [
      {
        "algorithm": "rsasha1",
        "keyLength": 1024,
        "keyType": "keySigning",
        "kind": "dns#dnsKeySpec"
      },
      {
        "algorithm": "rsasha256",
        "keyLength": 1024,
        "keyType": "zoneSigning",
        "kind": "dns#dnsKeySpec"
      }
    ],
    "kind": "dns#managedZoneDnsSecConfig",
    "nonExistence": "nsec3",
    "state": "on"
  }
}
```

Check the DNSSEC configuration object with the "**keyType**" property value set to "**keySigning**". If the **dns managed-zones describe** command output returns "**rsasha1**" as the value of the **dnssecConfig.defaultKeySpecs.algorithm** attribute, as shown in the example above, the DNSSEC Key-Signing Key (KSK) algorithm configured for the selected DNS managed zone is not secure and should not be used unless you need it for compatibility reasons.

### 2 )  Enable DNSSEC for Google Cloud DNS Zones

Having a trustworthy Domain Name System (DNS) that translates a domain name into its associated IP address is extremely important for web security nowadays. Attackers can hijack the process of domain/IP lookup and redirect users to malicious web content through DNS hijacking and Man-In-The-Middle (MITM) attacks.

To determine if DNSSEC is enabled for all your Domain Name System (DNS) managed zones, perform the following actions:

1. Run _**projects list**_ command  using custom query filters to list the IDs of all the projects available in your Google Cloud account:

```
gcloud projects list --format="table(projectId)"
```

2. The command output should return the requested GCP project identifiers (IDs):

```
PROJECT_ID
cc-web-project-123123
cc-backend-app-112233
```

3. Run **dns managed-zones list** command  which command displays the list of your managed-zones.

```
gcloud dns managed-zones list  --project cc-web-project-123123  --format="table(name,visibility)"
```

4. The command output should return the requested Google Cloud DNS zone metadata:

```
NAME                        VISIBILITY
cloudconformity-dns-zone    public
cloudrealisation-dns-zone   public
```

5. Run **dns managed-zones describe** command displays the details of the specified managed-zone.

```
gcloud dns managed-zones describe cloudconformity-dns-zone --format="json(dnssecConfig.state)"
```

6. The command output should return the requested configuration status:

```
STATE
off
```

If the **dns managed-zones describe** command output returns **off** as the value of the **STATE** attribute, as shown in the example above, or the **STATE** configuration attribute does not have any value configured, the Domain Name System Security Extensions (DNSSEC) feature is not enabled for the selected DNS managed zone.

### 3 ) Check for DNSSEC Zone-Signing Algorithm in Use

To follow security best practices, avoid using the RSASHA1 signature algorithm for DNSSEC signing unless it is required for compatibility reasons, because SHA1 is considered weak and vulnerable to collision attacks.

To determine the type of DNSSEC Zone-Signing Key algorithm configured for your public DNS managed zones, perform the following actions:

1. Run **projects list** command (Windows/macOS/Linux) using custom query filters to list the IDs of all the projects available in your Google Cloud account:

```
gcloud projects list  --format="table(projectId)"
```

2. The command output should return the requested GCP project identifiers (IDs):

```
PROJECT_ID
cc-frontend-app-123123
cc-backend-app-112233
```

3. Run **dns managed-zones list** command  which command displays the list of your managed-zones.

```
gcloud dns managed-zones list  --project cc-frontend-app-123123 --format="table(name,visibility)"
```

4. The command output should return the requested Google Cloud DNS zone metadata:

```
NAME VISIBILITY
cloudrealisation-dns-zone public
cloudconformity-dns-zone public
```

5. Run **dns managed-zones describe** command displays the details of the specified managed-zone.

```
gcloud dns managed-zones describe cloudrealisation-dns-zone  --format="json(dnssecConfig)"
```

6. The command output should return the requested configuration information in JSON format:

```
{
  "dnssecConfig": {
    "defaultKeySpecs": [
      {
        "algorithm": "rsasha1",
        "keyLength": 1024,
        "keyType": "keySigning",
        "kind": "dns#dnsKeySpec"
      },
      {
        "algorithm": "rsasha1",
        "keyLength": 1024,
        "keyType": "zoneSigning",
        "kind": "dns#dnsKeySpec"
      }
    ],
    "kind": "dns#managedZoneDnsSecConfig",
    "nonExistence": "nsec3",
    "state": "on"
  }
}
```

Check the DNSSEC configuration object with the "**keyType**" property value set to "**zoneSigning**". If the **dns managed-zones describe** command output returns "**rsasha1**" as the value of the **dnssecConfig.defaultKeySpecs.algorithm** attribute, as shown in the example above, the DNSSEC Zone-Signing Key (ZSK) algorithm configured for the selected DNS managed zone is considered deprecated and insecure, and should not be used unless it is required for compatibility reasons.
