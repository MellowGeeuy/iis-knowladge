---
name: iis-log-layers-and-substatus
type: research
agent: friday
date: 2026-09-15
---

## Triple

[[iis-log-layers-and-substatus]] --is--> request ที่ตายคนละชั้นของ IIS ถูกบันทึกคนละไฟล์ และรหัส substatus คือตัวที่บอกสาเหตุจริง ไม่ใช่ status code
[[iis-log-layers-and-substatus]] --source--> https://learn.microsoft.com/en-us/windows/win32/http/configuring-http-server-api-error-logging (ตาราง registry value · ErrorLoggingDir)
[[iis-log-layers-and-substatus]] --source--> https://learn.microsoft.com/en-us/iis/manage/provisioning-and-managing-iis/configure-logging-in-iis (หัวข้อ Select W3C Fields to Log)
[[iis-log-layers-and-substatus]] --source--> https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/health-diagnostic-performance/http-status-code (ตาราง substatus 401/403/404/500/502/503)
[[iis-log-layers-and-substatus]] --source--> https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/site-behavior-performance/troubleshoot-http-error-code (หัวข้อ Identify 4xx errors)
[[iis-log-layers-and-substatus]] --solves--> เปิด log ผิดไฟล์แล้วสรุปว่า "ระบบไม่ได้บันทึกอะไรไว้"
[[iis-log-layers-and-substatus]] --avoid--> สรุปสาเหตุจาก status code อย่างเดียวโดยไม่ดู sc-substatus
[[iis-log-layers-and-substatus]] --documented-in--> C:\Users\loxbit\Desktop\PARA\Projects\iis-knowladge\iis-knowladge.md (ส่วนที่ 09 · หัวข้อ "log แต่ละชั้นอยู่ที่ไหน")
[[iis-log-layers-and-substatus]] --verified-with--> WebFetch เอกสาร Microsoft 5 หน้า อ่านเนื้อหาเต็มทุกหน้า · ได้ตำแหน่งไฟล์ log 3 ชั้น + นิยาม W3C field 5 ตัว + รหัส substatus 10 ตัว

## Note

**ข้อเท็จจริงที่ต้องจำ**

- `httperr` ค่าเริ่มต้นอยู่ที่ `%SystemRoot%\System32\LogFiles` แล้ว HTTP Server API สร้างโฟลเดอร์ย่อย `HTTPERR` ให้เอง
  เปลี่ยนที่ registry `ErrorLoggingDir` แล้วต้อง `net stop http` / `net start http` จึงมีผล
- IIS log อยู่ที่ `%SystemDrive%\inetpub\logs\LogFiles` แยกโฟลเดอร์ `W3SVC<site id>` ไฟล์ชื่อ `exYYMMDD.log`
- request ที่ HTTP.sys ปฏิเสธจะ **ไม่มีทาง** ปรากฏใน IIS log เพราะยังไม่ถึง `w3wp.exe`
- วิธีแยกว่า response มาจากชั้นไหน ดู header `Server` — `Microsoft-HttpApi/2.0` คือ HTTP.sys ส่วน `Microsoft-IIS/*` คือ w3wp
- รหัสย่อยของ `401` เอกสารระบุว่าแสดงในเบราว์เซอร์แต่ไม่ถูกเขียนลง IIS log ต้องใช้ Failed Request Tracing แทน

**ข้อสังเกต (ยังไม่ได้ทดสอบบนเครื่องจริง):** ตัวอย่างคำสั่ง PowerShell ที่เขียนไว้ในเอกสารส่วนที่ 09
ยังไม่ได้รันบนเซิร์ฟเวอร์ IIS จริง ตรวจได้แค่ว่าชื่อคำสั่งกับ path ตรงกับที่เอกสาร Microsoft ระบุ
