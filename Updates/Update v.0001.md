# Update v.0001 — หน้า Knowledge Graph เหลือกราฟกับข้อมูล node

**วันที่:** 2026-09-15 · **ไฟล์ที่แก้:** `index.html`

## สิ่งที่ต้องได้
เข้าหน้า KG แล้วเห็นกราฟความสัมพันธ์ทันที คลิก node แล้วข้อมูลของ node นั้นขึ้นที่ด้านล่าง
พร้อมบอกว่าแต่ละความสัมพันธ์คืออะไร · ส่วนอื่นตัดออกทั้งหมด

## สิ่งที่แก้

### ตัดเนื้อหาส่วนอื่นในหน้า KG ออก
เหลือหัวข้อหน้าหนึ่งบรรทัด → กราฟ → panel ข้อมูล node · สิ่งที่เอาออก
- ย่อหน้านำเรื่อง ตารางหลักการ Linked Data 5 ข้อ callout ตัวอย่าง triple ตารางนิยาม node/relationship
- แถบปุ่มกรองหมวด (`.kg-ctl`) และ figcaption ใต้รูป
- ตาราง triple ทั้ง 65 แถว ตารางผลตรวจสอบกราฟ และ callout ท้ายหน้า

### panel ข้อมูล node
- `.kg-panel` → `position: sticky; bottom: 0` เกาะขอบล่างจอ คลิก node แล้วเห็นผลทันทีโดยไม่ต้องเลื่อนพ้นกราฟสูง 895px
- เพิ่ม `.kg-props` แถว property ของ node → `id` · `label` (หมวด) · `ส่วนที่` · `degree`
- แต่ละ relationship แสดงเป็น triple เต็ม `subject predicate object` พร้อมคำอ่านภาษาไทยใต้บรรทัด
  เช่น `Tomcat 11 SCANS webapps` → “สแกนหา application ใน”
- เพิ่มตาราง `MEANS` ใน JS แปล predicate ทั้ง 55 ตัวเป็นคำอ่านไทย อ่านจากฝั่ง subject ไปหาฝั่ง object
- `.kg-p-body` → `max-height: 42vh; overflow-y: auto` และ `:empty { display: none }` ยังไม่เลือก node ก็ยุบเหลือแถบหัว

### ลบของที่ไม่มีที่ใช้แล้ว
CSS `.kg-ctl` `.kg-chip` `.kg-c-*` `.kg-hint` `.kg-sub` `.kg-other` · JS ตัวแปร `filter` กับ `HINT` และ logic กรองหมวด

## ตรวจแล้ว
- ไม่มี JS error · section ในเอกสารยังครบ 16 · node 54 · relationship 65 เท่าเดิม
- คลิกครบทั้ง 54 node ไม่มี relationship ใดที่ยังแสดงเป็นชื่อ predicate ดิบ แปลว่า `MEANS` ครบทุกตัว
- node ที่มี relationship มากสุด (`w3wp.exe` · `Tomcat 11` · 7 เส้น) → panel สูง 280px ขอบล่างชนขอบจอพอดี
- สถานะยังไม่เลือก node → panel สูง 49px body สูง 0
- เลื่อนถึงท้ายหน้า panel กลับเข้า flow ปกติ ไม่ค้างทับอะไร
- diff แตะเฉพาะบล็อก CSS ของ KG · section `#kg` · และ IIFE ของ KG ไม่กระทบส่วนอื่นของเอกสาร
