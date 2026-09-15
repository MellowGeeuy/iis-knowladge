# Backup — ผังเดิมของ Knowledge Graph (force layout)

เก็บไว้ก่อนเปลี่ยนไปใช้ผังแบบมีแพตเทิร์น เมื่อ 2026-09-15

## ไฟล์

| ไฟล์ | เนื้อหา |
|---|---|
| `kg-figure-force-layout.svgpart` | tag `<svg>` เปิด พร้อมกลุ่ม `<g id="kgEdges">` และ `<g id="kgNodes">` ของผังเดิมทั้งชุด |
| `.commit` | commit hash ที่ยังมี `index.html` ฉบับเต็มของผังเดิม |

## คุณสมบัติของผังเดิม

- 60 node · 76 relationship · canvas 1414×1333
- ตำแหน่งมาจาก force layout ของเอกสารรุ่นแรก (54 node) แล้วขยายพิกัด 1.36 เท่า
  และวาง node ใหม่ 6 ตัวลงช่องว่างด้วยการค้นบน grid
- ตรวจแล้ว กล่องทับกัน 0 คู่ · เส้นพาดผ่านกล่อง 0 เส้น · ป้ายชื่อหาที่ว่างได้ครบ 76 เส้น

## วิธีกู้คืน

แทนที่สามส่วนใน `index.html` ด้วยเนื้อหาในไฟล์ `.svgpart` คือ tag `<svg ...>` ที่เปิดกลุ่มภาพ
กลุ่ม `<g id="kgEdges">` และกลุ่ม `<g id="kgNodes">` ส่วน `<g id="kgLab">` กับโค้ด JS ไม่ต้องแตะ

หรือกู้ทั้งไฟล์จาก git

```
git show $(cat backup/.commit):index.html > index.html
```
