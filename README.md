# Thinkware Dashcam

## Finding 1 - CVE-2025-2119: Bypass of device pairing
Product: Thinkware Dashcam - https://www.thinkware.com/Products/Dashcam/F800Pro

Model: F800 Pro

Affected components: Authentication mechanism, device registration/pairing 

Attack vector: An attacker who connects using default credentials can bypass the 2nd-factor device registration/pairing/binding


Description: 

While the official documentation states that we need to pair the dashcam to the phone while using the Thinkware Cloud app, that 2nd factor device registration could be bypassed if the services are accessed directly without going through the app:

![image](https://github.com/user-attachments/assets/a8a9beaa-fc70-4b8f-84a0-f7b5d3e90901)

Using default credentials 123456789, I could connect to a thinkware dashcam's wifi. Once I connected to the dashcam, I was able to access the rtsp (port 554) feed and also download all sensitive video recordings using telnet (port 23) without needing to press the wifi button:

![image](https://github.com/user-attachments/assets/e8258cc7-9ed8-4ede-826d-5b56b754c150)
![image](https://github.com/user-attachments/assets/64f80097-7378-4bd3-aa9d-80421c70b3c1)

While performing these actions and downloading the video recordings, there were no sounds activated on the dashcam as well so the victim would not know.


## Finding 2 - CVE-2025-2122: DoS 
The dashcam only supports 1 device at a time. What this means is that an attacker who's connected to the dashcam first would create a denial of service (DoS) for the rightful owner. This might be a side effect of a single-session restriction.

## Finding 3 - CVE-2025-2120: User credentials saved in plain-text
Product: Thinkware Dashcam

Model: F800 Pro

Affected components: Credentials of dashcam 

Attack vector: An attacker who has momentary access to the dashcam can extract the credentials in plain-text.

Description: 

The credentials of the dashcam owner is stored in plain-text in the /tmp/hostapd.conf configuration file:

![image](https://github.com/user-attachments/assets/e4355b45-d11a-4399-b3d6-34c6b2ae458a)


## Finding 4 - CVE-2025-2121: Write-access unprotected
Product: Thinkware Dashcam

Model: F800 Pro

Affected components: File storage

Description:

An attacker connected to the network can write arbitrary files or malware into the dashcam:

![image](https://github.com/user-attachments/assets/b18ccb18-6f50-47e9-b017-6ad043498efe)


## Finding 5 - CVE-2024–53614: Hardcoded plaintext decryption key in Thinkware Cloud APK

### Description
A hardcoded decryption key in Thinkware Cloud APK v4.3.46 allows attackers to access sensitive data and execute arbitrary commands with elevated privileges.

### Responsible Disclosure
Thinkware has been notified on 12 Nov 2024, via their PSTI vulnerability disclosure programme, in Thinkware Support #132091. A heads-up, that this report would be shared with MITRE, was also provided to them. The support team acknowledged this on 13 Nov 2024 and confirmed that they have forwarded my report to their mobile app development team for their consideration. A request for disclosure was made on 19 Nov 2024.

### Vulnerability Type
CWE-321: Use of Hard-coded Cryptographic Key

### Affected Component
<REDACTED>

### Affected Product Code Base
Thinkware Cloud APK v4.3.46

### Attack Vector
A MitM network attacker who sniffs the encrypted login data could use this decrypted key to reveal login credentials to Thinkware cloud, which hosts sensitive video and audio footage of dashcams.
