`User Enum Check
	[] Response, Length, Grep Match To prepare, Status Code
	[] Check User Lock > payload (NULL) > Grep Extract >find 
`Simple Bypass 2FA
	[] Intercept modify Location Header , Modify Response
	[] Check Cookie
`Forget Pass
	[] If got temp-forget-password-token check it's can reuse with same token
Rate Limit
	[] X-Forwarded-For
	[] IP Block > Check login time || Logic Flaw
**BruteForce User:Password in base64**
![[Pasted image 20260609152551.png]]
![[Pasted image 20260609152606.png]]