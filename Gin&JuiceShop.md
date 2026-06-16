``Anonymous
``index page
```
/product
/blog
/subscribe
/login
/cart
/admin (Access Control)
Vuln:
	TLS cert
	Cookie without httpOnlyflag
	External server interaction
	URL override (X-Original-URL, X-Rewrite-URL)
```
``product page
```
search product bar "/catalog"
	Vuln: Strict transport security not enforced
		TLS Cookie without secure flag set "trackingId"
		Base64-encoded data in parameter
check stock
	Vuln: Strict transport security not enforced
		TLS cookie without secure flag
		Cookie without secure flag
		XEE "/catalog/product/stock" (Find)
add cart
	Vuln: Strict transport security not enforced
		TLS Cookie without secure flag
		Cookie without httpOnly flag
		Cacheable HTTPS response
		URL Input return in response(reflected)
		Input returnd in response(reflected) Cookie
		CSS (reflected)
		HTTP response header injection
		Client-side template injection
		SQL injection in TrackingId (Find)
		relected DOM-based
view cart
```
``blog page
```
search blog bar
	Vuln: Base64-encoded data in parameter
		Strict transport security not enforced
		TLS Cookie without secure flag
		Cookie without httpOnly flag
		Cacheable HTTPS response
		Input returnd in response(reflected) Search
		Client-side prototype pollution
		XSS (DOM-based) "can steal cookie"
		Client-side template injection (AngularJS v1.7.7)
blog details
```
``about page
```
nothing
```

``User Account
```
login
my-account
cart
```


