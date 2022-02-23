---
description: Active Directory
cover: >-
  https://images.unsplash.com/photo-1541728472741-03e45a58cf88?crop=entropy&cs=srgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw5fHxoYWNrZXJ8ZW58MHx8fHwxNjQ0OTUxOTI2&ixlib=rb-1.2.1&q=85
coverY: 421.77650429799417
---

# 🔰 Search - 10.10.11.129 | WIN

![](<../.gitbook/assets/image (24).png>)

## <mark style="color:purple;background-color:green;">\_\_Enumeration\_\_</mark>

<details>

<summary><mark style="color:purple;">NMAP</mark></summary>

```
Nmap scan report for 10.10.11.129
Host is up (0.32s latency).                                                                                                                      
                                                                                                                                                 
PORT      STATE SERVICE       VERSION
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: Search &mdash; Just Testing IIS
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2022-02-23 13:16:38Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-02-23T13:18:10+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Not valid before: 2020-08-11T08:13:35
|_Not valid after:  2030-08-09T08:13:35
443/tcp   open  ssl/http      Microsoft IIS httpd 10.0
| ssl-cert: Subject: commonName=research
| Not valid before: 2020-08-11T08:13:35
|_Not valid after:  2030-08-09T08:13:35
|_http-title: Search &mdash; Just Testing IIS
|_ssl-date: 2022-02-23T13:18:10+00:00; 0s from scanner time.
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
| tls-alpn: 
|_  http/1.1
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-02-23T13:18:10+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Not valid before: 2020-08-11T08:13:35
|_Not valid after:  2030-08-09T08:13:35
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=research
| Not valid before: 2020-08-11T08:13:35
|_Not valid after:  2030-08-09T08:13:35
|_ssl-date: 2022-02-23T13:18:10+00:00; 0s from scanner time.
3269/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: search.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2022-02-23T13:18:10+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=research
| Not valid before: 2020-08-11T08:13:35
|_Not valid after:  2030-08-09T08:13:35
9389/tcp  open  mc-nmf        .NET Message Framing
49667/tcp open  msrpc         Microsoft Windows RPC
49675/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         Microsoft Windows RPC
49714/tcp open  msrpc         Microsoft Windows RPC
49739/tcp open  msrpc         Microsoft Windows RPC
Service Info: Host: RESEARCH; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2022-02-23T13:17:35
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled and required

```

```
sudo nmap -sC -sV -A -p53,80,139,445,88,135,389,443,464,593,636,3268,3269,9389,49667-49739 search.htb -Pn --script "ldap* and not brute" --script "safe or smb-enum-*"


```

</details>

<details>

<summary><mark style="color:green;">Web Services</mark></summary>

**Technologies**

![](<../.gitbook/assets/image (23).png>)\
![](<../.gitbook/assets/image (25).png>)

**Dirsearch | Gobuster**

```yaml
Target: http://research/ & https://research/      
[08:46:34] 403 -    1KB - /certenroll/                                      
[08:46:34] 401 -    1KB - /certsrv/                                                    
[08:46:49] 403 -    1KB - /images/                                                              
[08:46:52] 403 -    1KB - /js/         
[08:46:52] 200 -   44KB - /index.html                                       
[08:47:13] 403 -    1KB - /staff/                                                      


```

#### Page Screenshots

![](<../.gitbook/assets/image (26).png>)

</details>

<details>

<summary><mark style="color:red;">AD Enumeration</mark></summary>



</details>

#### :notebook\_with\_decorative\_cover: <mark style="color:blue;">**Other**</mark>

Both webpages - at http and https - are same.\
SSL Cert Info --> _`CN=search-RESEARCH-CA,DC=search,DC=htb`_

* Extract information from **DNS** - `dig ANY @10.10.11.129 search.htb`\
  ![](<../.gitbook/assets/image (9).png>)\
  Hosts found --> _research.search.htb.  hostmaster.search.htb._ (Nothing :P)

## <mark style="color:red;background-color:yellow;">\_\_Exploitation\_\_</mark>

## _<mark style="color:orange;">FOOTHOLD</mark>_







### Getting reverse shell



\


### Enumerating the machine for lateral movement

```
-----BEGIN OPENSSH PRIVATE KEY-----
```

## _<mark style="color:red;">PIVOTING</mark>_







## _<mark style="color:red;">PRIVILEGE ESCALATION</mark>_

**For enumeration** - [https://nored0x.github.io/red-teaming/windows-enumeration/](https://nored0x.github.io/red-teaming/windows-enumeration/)\
We could also use WinPEAS.bat or obfuscated WinPEAS.exe to bypass AV and enumerate.



****

### EXPLOITATION

* **VULNERABLE to **_<mark style="color:red;">**UNQUOTED SERVICE PATH**</mark>_**  attack**





* **Making the Exploit POC in C#**

```csharp
```



* **Exploiting the Path Injection and getting `NT AUTHORITY\SYSTEM`**







<mark style="color:purple;">****</mark>\ <mark style="color:purple;">****</mark>\ <mark style="color:purple;">**ROOT ! :)**</mark>

### **GETTING PERSISTENCE ON THE MACHINE**

* **Dumping hashes**



* **Transfer to attacker host**&#x20;



