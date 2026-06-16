```
for i in range(150):
    if i % 3:
        print("carlos")
    else:
        print("wiener")
```

```
i = 0
with open("passwords.txt", "r", encoding="utf-8") as f:
    for line in f:
        pwd = line.strip()   # ลบ \n ออก
        if i % 3:
            print(pwd)
        else:
            print("peter")
            print(pwd)
            i += 1
        i += 1
```
