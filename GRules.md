# GRules — กฎการทำงานของโปรเจกต์ [Project Name]

> อ้างอิง: MDN Web Docs · Google JS Style Guide · BEM · SMACSS

---

## กฎทั่วไป (General Rules)

- ชื่อไฟล์: `kebab-case` lowercase เสมอ
- ห้าม hardcode API keys, tokens, passwords ในโค้ด
- Update log: สร้าง `Updates/Update v.xxxx.md` ทุก session ที่มีการแก้ไขโค้ด

---

## กฎการ Coding

### HTML
- ใช้ semantic HTML5 elements
- `id`: `kebab-case` unique ต่อหน้า
- `class`: BEM pattern → `block__element--modifier`

### CSS
- Token ครั้งเดียว — นิยาม `:root { --var }` ในไฟล์เดียว ห้าม copy inline
- Naming: `.component__element--modifier` | `.u-utility` | `.is-state`
- ห้าม hardcode สีหรือ spacing — ใช้ CSS Custom Properties เสมอ

### JavaScript
- ตัวแปร / function: `camelCase`
- Class: `PascalCase`
- Constant: `UPPER_SNAKE_CASE`
- ไฟล์: `kebab-case`
- ห้ามเขียน business logic inline ใน HTML — แยกเป็นไฟล์ `.js`
- Module layers: `utils/ → modules/ → pages/`

---

## กฎโครงสร้างไฟล์

```
project/
├── assets/
│   ├── css/          ← CSS ของเรา
│   ├── js/
│   │   ├── utils/    ← Pure functions
│   │   ├── modules/  ← Feature modules
│   │   └── pages/    ← Page init scripts
│   ├── libs/         ← Vendor only
│   └── images/
└── docs/
```

---

## กฎ UI/UX

- ใช้ Design Tokens จาก CSS Custom Properties เสมอ
- ห้าม hardcode สีโดยตรง
- Animation duration < 300ms

---

## กฎ Security

- ห้าม hardcode credentials ในโค้ด
- ตรวจสอบ Auth ทุกครั้งที่เพิ่ม endpoint ใหม่

---

## กฎที่ห้ามทำ (Do NOT)

- ❌ ห้าม hardcode API keys, tokens, passwords
- ❌ ห้ามนิยาม CSS token ซ้ำในหลายไฟล์
- ❌ ห้ามเขียน JS logic inline ใน HTML
- ❌ ห้ามเก็บ vendor libs ปะปนกับ code ของเรา
- ❌ ห้ามใช้ `!important` ใน CSS
- ❌ ห้ามลบไฟล์โดยไม่ backup หรือ confirm กับ G ก่อน

---

_อัปเดตล่าสุด: 2026-09-15_

