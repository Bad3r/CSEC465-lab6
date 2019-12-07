# Networks:

----------------------------------------------------------------------------------------------------------

# `192.168.0.0` - `192.168.0.99`
----------------------------------------------------------------------------------------------------------

## Discovered Hosts:

```
    192.168.0.1
    192.168.0.33
    192.168.0.33
    192.168.0.1
    192.168.0.1
    192.168.0.33
    192.168.0.33
```

## `192.168.0.1` - PFsense
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
    443/tcp 
    22/tcp 
    80/tcp 
```

- Web ports: `80, 443`

```
80/tcp  open  http
|_http-title: Did not follow redirect to https://192.168.0.1/
443/tcp open  https
|_http-title: Login
| ssl-cert: Subject: commonName=pfSense-5c998c4436ebe/organizationName=pfSense webConfigurator Self-Signed Certificate/stateOrProvinceName=State/countryName=US
| Subject Alternative Name: DNS:pfSense-5c998c4436ebe
```

HTTPS requires a certificate , its expired. HTTP forward to HTTPS
using `X11forward` I was able to bring `PFsense` interface and login with default creds:
```
username: admin
password: pfsense
```


## `192.168.0.3`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

> First 1000 ports are filtered


## `192.168.0.33`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
22/tcp  open  ssh
 80/tcp  open  http
 |_http-title: Apache2 Ubuntu Default Page: It works
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds < SMB
Host script results:
smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: quackenbush
|   NetBIOS computer name: QUACKENBUSH\x00
|   Domain name: \x00
|   FQDN: quackenbush
|_  System time: 2019-12-07T15:53:16-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2019-12-07 15:53:16
|_  start_date: 1600-12-31 19:03:58
```

### smb-protocol

```
Nmap scan report for 192.168.0.33
Host is up (0.0011s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
MAC Address: 00:50:56:01:19:0A (VMware)

Host script results:
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2.02
|     2.10
|     3.00
|     3.02
|_    3.11
```

# `192.168.0.2/24`
----------------------------------------------------------------------------------------------------------

## Discovered Hosts:

- `192.168.2.1` --> PFsense
- `192.168.2.15`
- `192.168.2.25`
- `192.168.2.26`
- `192.168.2.27`

## `192.168.2.1` --> PFsense
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
|_http-title: Did not follow redirect to https://192.168.2.1/
443/tcp open  https
|_http-title: Login
```

## `192.168.2.15`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap
```
PORT    STATE SERVICE
139/tcp open  netbios-ssn
Host script results:
|_nbstat: NetBIOS name: GARAGE3, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:01:17:4d (VMware)
|_smb2-security-mode: SMB: Couldn't find a NetBIOS name that works for the server. Sorry!
|_smb2-time: ERROR: Script execution failed (use -d to debug)
```


## `192.168.2.25`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 15063 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: vega
|   NetBIOS computer name: VEGA\x00
|   Domain name: metrotransit.enterprise
|   Forest name: metrotransit.enterprise
|   FQDN: vega.metrotransit.enterprise
|_  System time: 2019-12-07T12:51:48-08:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
```

### smb-protocol
```
Nmap scan report for 192.168.2.25
Host is up (0.00090s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds
-----------------------------------------------------

Host script results:
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2.02
|     2.10
|     3.00
|     3.02
|_    3.11
```

## `192.168.2.26`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

| smb-os-discovery: 
|   OS: Windows 7 Enterprise 7601 Service Pack 1 (Windows 7 Enterprise 6.1)
|   Computer name: harrison
|   NetBIOS computer name: HARRISON\x00
|   Domain name: metrotransit.enterprise
|   Forest name: metrotransit.enterprise
|   FQDN: harrison.metrotransit.enterprise
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
```


### SMB  enum

```
Nmap scan report for 192.168.2.26
Host is up (0.00094s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-protocols: 
|   dialects: 
|     NT LM 0.12 (SMBv1) [dangerous, but default]
|     2.02
|_    2.10
```


## `192.168.2.27`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Host script results:
|_clock-skew: mean: -30s, deviation: 0s, median: -30s
| smb-os-discovery: 
|   OS: Windows 10 Enterprise 15063 (Windows 10 Enterprise 6.3)
|   OS CPE: cpe:/o:microsoft:windows_10::-
|   Computer name: smith
|   NetBIOS computer name: SMITH\x00
|   Domain name: metrotransit.enterprise
|   Forest name: metrotransit.enterprise
|   FQDN: smith.metrotransit.enterprise
|_  System time: 2019-12-07T12:51:51-08:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
```

### SMB enum

```
Nmap scan report for 192.168.2.27
Host is up (0.0011s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-protocols: 
|   dialects: 
|     NTLM 0.1smb-protocol2 (SMBv1) [dangerous, but default]
|     2.02
|     2.10
|     3.00
|     3.02
|_    3.11
```


# `192.168.0.3/24`
----------------------------------------------------------------------------------------------------------

## Discovered Hosts:

- `192.168.3.1` --> PFsense
- `192.168.3.2`
### smb-  `192.168.3.17`
-  `192.168.3.20`



## `192.168.3.1` --> PFsense
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
22/tcp open  ssh
80/tcp  open  http
443/tcp open  https
```

## `192.168.3.2`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
22/tcp open   ssh
```

## `192.168.3.17`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap

```
22/tcp open   ssh
80/tcp closed http
```


## `192.168.3.20`
----------------------------------------------------------------------------------------------------------

### Enumeration

### nmap
```
22/tcp open  ssh
80/tcp open  http
| http-robots.txt: 1 disallowed entry 
Post-scan script results:
| ssh-hostkey: Possible duplicate hosts
| Key 256 e5:8b:c2:ed:84:39:51:8c:b9:0b:6c:b5:59:78:94:a9 (ECDSA) used by:
|   192.168.3.2
|   192.168.3.20
| Key 2048 2c:72:1e:5b:c4:31:c7:ef:1d:a7:57:a8:63:94:6b:89 (RSA) used by:
|   192.168.3.2
|   192.168.3.20
| Key 256 a2:41:40:72:47:96:1a:6a:79:c8:46:ab:d5:d1:8d:3e (EdDSA) used by:
|   192.168.3.2
|_  192.168.3.20
```










