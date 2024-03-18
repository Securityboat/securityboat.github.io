# GCP API

GCP (Google Cloud Platform) provides a wide range of APIs (Application Programming Interfaces) that developers can use to build applications that interact with various GCP services. These APIs include the Google Cloud Storage API for managing object storage, the Google Cloud Vision API for image recognition and analysis, the Google Cloud Speech-to-Text API for converting audio to text, the Google Cloud Natural Language API for text analysis, and the Google Cloud Translation API for real-time language translation. There are many more APIs available, and developers can access them through REST APIs, client libraries, or the Google Cloud Console.

## 1. Check for API Key API Restrictions

1. Run **projects list** command to list the project

```
gcloud projects list --format="table(projectId)"
```

2. The command output should return the requested GCP project IDs:

```
PROJECT_ID
  cc-project5-112233
  cc-internal-111222
```

3. Run **services api-keys list** commandlists keys of a given project, including keys that were soft-deleted in the past 30 days

```
gcloud alpha services api-keys list  --project=cc-project5-112233  --format="table(uid)"
```

4. The command output should return the IDs of the active API keys:

```
UID:
  abcd1234-abcd-1234-abcd-1234abcd1234
  1234abcd-1234-abcd-1234-abcd1234abcd
```

5. gcloud alpha services api-keys describe - describe an API key's metadata

```
gcloud alpha services api-keys describe abcd1234-abcd-1234-abcd-1234abcd1234 --format="json(restrictions)"
```

6. Based on the **services api-keys describe** command output, you can determine whether or not the use of the selected API key is restricted to specific APIs only:

* If the command output returns **null**, there is no API restriction control enabled, therefore the selected API key can call any supported Google Cloud Platform (GCP) API:

```
null
```

* If the command output returns one or more APIs, check the **"apiTargets"** array for the list of GCP APIs that can use the selected API key. If the **"apiTargets"** array contains **"cloudapis.googleapis.com"**, as shown in the example below, the selected API key can call any GCP API because the **"cloudapis.googleapis.com"** option represents the API collection of all the cloud services/APIs offered by Google Cloud Platform:

```
{
  "restrictions": {
    "apiTargets": [
      {
        "service": "cloudapis.googleapis.com"
      }
    ]
  }
}
```

7. Repeat steps no. 5 and 6 for each API key generated for the selected GCP project.
8. Repeat steps no. 3 – 7 for each project deployed within your Google Cloud account.

## 2. Check for API Key Application Restrictions

1. Run **projects list** command to list the project

```
gcloud projects list --format="table(projectId)"
```

2. The command output should return the requested GCP project IDs:

```
PROJECT_ID
  cc-project5-112233
  cc-internal-111222
```

3. Run **services api-keys list** command  using the ID of the GCP project that you want to examine as the identifier parameter and custom query filters to describe the identifier of each active API key generated for the selected project:

```
gcloud alpha services api-keys list  --project=cc-project5-112233  --format="table(uid)"
```

4. The command output should return the IDs of the active API keys:

```
UID:
  abcd1234-abcd-1234-abcd-1234abcd1234
  1234abcd-1234-abcd-1234-abcd1234abcd
```

5. Run **services api-keys describe** command (Windows/macOS/Linux) using the ID of the API key that you want to examine as the identifier parameter and custom query filters to describe the API key application restrictions configured for the selected key:

```
gcloud alpha services api-keys describe abcd1234-abcd-1234-abcd-1234abcd1234  --format="json(restrictions)"
```

6. Based on the **services api-keys describe** command output, you can determine if the use of the selected API key is unrestricted:

* If the command output returns **null**, there is no restriction control enabled to specify which websites, IP addresses, or mobile applications can use the key, therefore the selected API key usage is unrestricted:

```
null
```

* If the command output returns one or more HTTP referrers for API key application restrictions, as shown in the example above, check the **"allowedReferrers"** array for the list of domains that can use the selected API key. If the referrer is set to a wildcard, i.e. **\*** or **\*.\[TLD]** or **\*.\[TLD]/\***, where \[TLD] represents the top-level domain, there are no well-defined restrictions that specify which trusted websites can use your key, therefore the selected API key usage is unrestricted:

```
{
  "restrictions": {
    "browserKeyRestrictions": {
      "allowedReferrers": [
        "*.example.com"
      ]
    }
  }
}
```

* If the **services api-keys describe** command output returns one or more IPv4/IPv6 addresses for API key application restrictions, as shown in the example above, check the **"allowedIps"** array for the list of hosts that can access the selected API key. If the **"allowedIps"** is set to any host, i.e. **0.0.0.0, 0.0.0.0/0** or **::0**, there is no restriction control implemented to specify which host can use your key, therefore the selected API key usage is unrestricted:

```
{
  "restrictions": {
    "serverKeyRestrictions": {
      "allowedIps": [
        "0.0.0.0/0"
      ]
    }
  }
}
```

7. Repeat steps no. 5 and 6 for each API key generated for the selected GCP project.
8. Repeat steps no. 3 – 7 for each project deployed within your Google Cloud account.

## 3.  Enable Cloud Asset Inventory

1. Run **projects list** command to list the project

```
gcloud projects list  --format="table(projectId)"
```

2. The command output should return the requested GCP project identifiers:

```
PROJECT_ID
cc-web-project-112233
cc-mobile-project-123123
```

3. Run **services list** command which lists API keys

```
gcloud services list  --project cc-web-project-112233  --enabled  --filter=name:cloudasset.googleapis.com
```

4. The command output should return the name and the title of the requested API:

```
Listed 0 items.
```

If the **services list** command output returns **Listed 0 items**, as shown in the output example above, the Cloud Asset API is currently disabled, therefore the Google Cloud Asset Inventory is not enabled for the selected GCP project.

5. Repeat steps no. 3 and 4 for each project created within your Google Cloud account.

## 4.  Rotate Google Cloud API Keys

1. Run **projects list** command (Windows/macOS/Linux) with custom query filters to list the ID of each project available in your Google Cloud account:

```
gcloud projects list --format="table(projectId)"
```

2. The command output should return the requested GCP project IDs:

```
PROJECT_ID
  cc-project5-112233
  cc-internal-123123
  cc-web-prod-111222
```

3. Run **services api-keys list** command  using the ID of the GCP project that you want to examine as the identifier parameter and custom query filters to describe the identifier of each active API key created for the selected project:

```
gcloud alpha services api-keys list  --project=cc-project5-112233   --format="table(uid)"
```

4. The command output should return the IDs of the active API keys:

```
UID:
  abcd1234-abcd-1234-abcd-1234abcd1234
  1234abcd-1234-abcd-1234-abcd1234abcd
```

5. Run **services api-keys describe** command  using the ID of the API key that you want to examine as the identifier parameter and custom query filters to describe the API key application restrictions configured for the selected key:

```
gcloud alpha services api-keys describe abcd1234-abcd-1234-abcd-1234abcd1234  --format="json(createTime)"
```

6. The command output should return the API key creation date/time:

```
CREATE_TIME: 2020-10-25T09:01:20.329336Z
```

Check the timestamp returned by the **services api-keys describe** command output to determine when the selected API key was created. If more than 90 days have passed since the key was created, the selected Google Cloud Platform (GCP) API key is not regenerated (rotated) on a regular basis.

7. Repeat steps no. 5 and 6 for each API key generated for the selected GCP project.
8. Repeat steps no. 3 – 7 for each project deployed within your Google Cloud account.

