---
name: kg-circle-nodes-over-boxes
type: decision
agent: friday
date: 2026-09-15
---

## Triple

[[kg-circle-nodes-over-boxes]] --is--> ตัดสินใจวาด node ของ Knowledge Graph เป็นวงกลมขนาดแปรตาม degree แทนกล่องที่กว้างตามชื่อ
[[kg-circle-nodes-over-boxes]] --solves--> จัดผังให้เป็นระเบียบไม่ได้เลย เพราะกล่องกว้างสูงสุด 244px กินพื้นที่กีดขวางจนเส้นตรงเดินไม่ผ่าน
[[kg-circle-nodes-over-boxes]] --caused-by--> เงื่อนไข "ห้ามมีเส้นพาดผ่านกล่อง" บวกกับ node ที่เป็นกล่องข้อความ บังคับให้ผังต้องกระจายแบบ organic เท่านั้น
[[kg-circle-nodes-over-boxes]] --source--> https://obsidian.md/help/plugins/graph ("The more nodes that reference a given node, the bigger it gets" · Text fade threshold · แรงสี่ตัว center/repel/link force กับ link distance)
[[kg-circle-nodes-over-boxes]] --verified-with--> วัดผัง 9 แบบด้วยเกณฑ์เดียวกัน · แบบวงกลมได้เส้นตัดกันเอง 82 คู่ เทียบกับผังกล่องเดิม 81 · ภาพเล็กลงจาก 1414x1333 เหลือ 1275x1059 · เส้นสั้นลงจาก 278px เหลือ 214px
[[kg-circle-nodes-over-boxes]] --verified-with--> หลังขัดผัง เส้นลอดผ่านวง 0 · วงทับกัน 0 · ชื่อ node หาที่ว่างได้ 60 จาก 60
[[kg-circle-nodes-over-boxes]] --avoid--> จัด node เป็นแถวเป็นคอลัมน์แล้วลากเส้นตรง · ลองแล้วได้เส้นพาดผ่านกล่อง 112 เส้น
[[kg-circle-nodes-over-boxes]] --avoid--> relax force layout ใหม่ทั้งกราฟทั้งที่ผังเดิมผ่านเงื่อนไขอยู่แล้ว · ลองแล้วได้ 233 เส้น แย่กว่าเดิมมาก
[[kg-circle-nodes-over-boxes]] --breaks--> viewBox ของ SVG ถ้าใส่กล้องซูมทับ จะถูกย่อสองชั้น ภาพออกมาเล็กผิดปกติ ต้องตัด viewBox ทิ้ง
[[kg-circle-nodes-over-boxes]] --documented-in--> C:\Users\loxbit\Desktop\PARA\Projects\iis-knowladge\Updates\Update v.0007.md
[[kg-circle-nodes-over-boxes]] --produces--> https://claude.ai/artifact/MtQBM7F1ToxaDQEK6YtFjM (หน้าเทียบผัง 9 แบบ วัดด้วยเกณฑ์เดียวกัน)

## Note

**วิธีที่ได้ผลเวลาต้องแก้ผังที่ผ่านเงื่อนไขอยู่แล้ว** — อย่ารันใหม่ทั้งกราฟ ให้ตรึงของเดิมไว้แล้วแก้เฉพาะจุด
ตอนเพิ่ม node 6 ตัวใช้วิธีขยายพิกัดออก 1.36 เท่าแล้วค้นที่วางทีละตัวบน grid ได้ผลครบทุกตัว

**การผลักแบบ reactive ไม่ลู่เข้า** — ดันกล่องพ้นเส้นหนึ่งแล้วไปขวางอีกเส้น ลองสามรอบก็ยังวน
ที่ได้ผลคือค้นตำแหน่งเป็นวงรอบตัวเอง แล้วรับเฉพาะตำแหน่งที่จำนวนเส้นมีปัญหาลดลงจริง

**ข้อสังเกต (ยังไม่ได้ทดสอบกับผู้อ่านจริง):** การที่ชื่อ node จางหายตอนซูมออกอาจทำให้ภาพนิ่ง ๆ
ในเอกสารดูว่างเปล่า จึงกันไว้ว่า node ที่ถูกชี้กับเพื่อนบ้านต้องอ่านชื่อได้เสมอ แต่ยังไม่รู้ว่าพอไหม
