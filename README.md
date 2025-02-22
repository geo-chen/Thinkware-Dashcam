# Thinkware Dashcam

**CVE-2024–53614** - hardcoded plaintext decryption key in Thinkware Cloud APK

## Description
A hardcoded decryption key in Thinkware Cloud APK v4.3.46 allows attackers to access sensitive data and execute arbitrary commands with elevated privileges.

## Responsible Disclosure
Thinkware has been notified on 12 Nov 2024, via their PSTI vulnerability disclosure programme, in Thinkware Support #132091. A heads-up, that this report would be shared with MITRE, was also provided to them. The support team acknowledged this on 13 Nov 2024 and confirmed that they have forwarded my report to their mobile app development team for their consideration. A request for disclosure was made on 19 Nov 2024.

## Vulnerability Type
CWE-321: Use of Hard-coded Cryptographic Key

## Affected Component
<REDACTED>

## Affected Product Code Base
Thinkware Cloud APK v4.3.46

## Attack Vector
A MitM network attacker who sniffs the encrypted login data could use this decrypted key to reveal login credentials to Thinkware cloud, which hosts sensitive video and audio footage of dashcams.
