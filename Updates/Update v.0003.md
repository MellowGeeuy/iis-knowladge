# Update v.0003 — สารบัญเลื่อนเปิดปิดแบบ smooth

**วันที่:** 2026-09-15 · **ไฟล์ที่แก้:** `index.html`

## สิ่งที่ต้องได้
กดหุบ/เปิดสารบัญแล้วต้องเลื่อนลื่น ไม่ใช่หายวับ

## ปัญหาของวิธีเดิม
เดิมหุบด้วย `display: none` ซึ่ง animate ไม่ได้เลย

## ทางที่ลองแล้วไม่ผ่าน

| วิธี | ผลที่เจอ |
|---|---|
| `transition: grid-template-columns` ตรง ๆ | renderer ค้างจน CDP timeout 45 วินาที และแท็บ crash หนึ่งครั้ง |
| `grid-template-columns: auto` + `transition: width` ที่ตัวแถบ | track แบบ `auto` วัดตาม max-content ของ item จึงไม่ยอมหด แม้สั่ง `width: 0` แบบ inline ก็ยังได้ 264px |

## วิธีที่ใช้จริง
ลงทะเบียน custom property เป็น `<length>` แล้ว animate ตัวมัน ส่วน grid track อ่านค่าจากมันอีกที
การ interpolate จึงเกิดกับ length ตัวเดียว ไม่ใช่ทั้ง track list

```css
@property --nav-w { syntax: "<length>"; inherits: false; initial-value: 264px; }
.shell {
  --nav-w: var(--side);
  grid-template-columns: var(--nav-w) minmax(0, 1fr);
  transition: --nav-w .3s ease;
}
.shell.nav-off { --nav-w: 0px; --wide: var(--wide-open); }
```

อื่น ๆ ที่ตามมา
- หุ้มเนื้อหาในแถบด้วย `.side-in` ที่กว้างคงที่ `var(--side)` และย้าย `overflow-y: auto` มาไว้ชั้นนี้
  ตัวแถบเป็น `overflow: hidden` ตัวหนังสือจึงไม่บีบตามระหว่างเลื่อน แค่ถูกเฉือนออกไป
- เส้นขอบขวาของแถบจาง ๆ ไปพร้อมกัน (`transition: border-color .3s`) ไม่งั้นเหลือเส้น 1px ค้าง
- แถบบนเปลี่ยนจาก `display: none/block` เป็น `max-height: 0 → 60px` จะได้คลี่ลงมาพร้อมกัน
  ไม่ใช่โผล่พรึบแล้วดันเนื้อหาลง
- ปุ่มสารบัญแบบขีดสามขีดเป็นของจอแคบอย่างเดียว ย้าย `display: none` ไปไว้ที่ `.menu-btn` ชั้นฐาน
  แล้วให้ media query เปิดคืน ลดกฎซ้อนจากเดิมสองบรรทัด
- `@media (prefers-reduced-motion: reduce)` ที่มีอยู่แล้วครอบ transition ชุดนี้ด้วย

## ตรวจแล้ว
- เก็บค่า `--nav-w` ระหว่างเลื่อน (ตอนแท็บ visible) ได้ `264 → 234 → 172 → 88 → 52 → 20 → 13 → 1.9 → 0`
  ใช้เวลา ~320ms โค้งตาม ease ตามที่ตั้งไว้
- สถานะปลายทาง: `grid-template-columns` = `0px 1405.19px` · แถบซ้ายเหลือ 1px (เส้นขอบ)
  · แถบบนสูง 54px · `.page` 1000 → 1264px
- จอ 400px (ทดสอบผ่าน iframe): แถบเป็น `fixed` 272px อยู่นอกจอที่ x = -272
  · `.side-in` กว้าง 100% ไม่บีบ · แถบบนสูง 54px `max-height: none`
  · ปุ่มขีดสามขีดแสดง ปุ่มหุบกับปุ่มเปิดถูกซ่อน · grid เหลือคอลัมน์เดียว
  · บังคับใส่คลาส `nav-off` แล้วแถบยังกว้าง 272px ปุ่มขีดสามขีดยังอยู่ ไม่กระทบ drawer
- ไม่มี JS error

## หมายเหตุ
วัด transition ในแท็บที่ Chrome ถือว่า `hidden` ไม่ได้ เพราะเบราว์เซอร์ไม่เดินเฟรมให้
ค่าที่อ่านได้จะค้างที่ค่าเริ่มต้นหรือกระโดดไปค่าปลายทางเลย ตัวเลขชุดข้างบนเก็บตอนแท็บ visible
