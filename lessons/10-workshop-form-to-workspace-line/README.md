# 10 — Workshop #1: ฟอร์ม → Google Workspace + LINE / Workshop #1: Form → Google Workspace + LINE

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/10-workshop-form-to-workspace-line](../../exercises/10-workshop-form-to-workspace-line/README.md) |
| เวลาโดยประมาณ | ~90 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 85–92 |
| เฉลย | `exercises/10-.../solution/02 - Form to Google Workspace & LINE.json` |

Workshop แรกคือการประกอบทุกอย่างที่เรียนมาเป็น **ระบบรับเรื่องจริง**: ลูกค้ากรอกฟอร์ม → ระบบบันทึกลง Sheets, สร้างนัดใน Calendar, เขียนรายงานเป็น Docs, สำรองไฟล์ลง Drive และถ้าเรื่องด่วน — แจ้งทีมทาง **LINE** ทันที นี่คือ workflow ขนาดจริงที่องค์กรใช้ได้ทันที

## สถาปัตยกรรม (4 ขั้น)

1. **Collect — n8n Form Trigger** สร้างฟอร์มรับข้อมูล (ชื่อ อีเมล เบอร์โทร หัวข้อ รายละเอียด ความเร่งด่วน) ใช้ dropdown กำหนดค่าความเร่งด่วนเพื่อ validation; ตั้ง Respond Mode เป็น "Response Node" เพื่อโชว์หน้าขอบคุณเอง
2. **Process — Code node ("The Brain")** mapping field, จัดรูปวันที่เป็น Timestamp, และคำนวณ priority จากคำสำคัญ (ฉุกเฉิน/ด่วนมาก → HIGH)
3. **Store & Create** — Append ลง **Sheets** (ทุก transaction เข้าฐานข้อมูล), **IF "Has Appointment?"** จริง → สร้าง **Calendar Event** พร้อมเชิญผู้ส่งทางอีเมล, สร้าง **Docs** รายงานสรุป (เขียน Markdown ใน content ได้), สำรองข้อความเป็น .txt ลง **Drive** (เก็บ Folder ID จาก URL ของโฟลเดอร์)
4. **Notify — LINE Push Message** เงื่อนไข "High Priority?" จริง → ส่งแจ้งทีมทันที ผ่าน Push Message; สุดท้าย Respond หน้าขอบคุณ

## คำแนะนำจากท้องสนาม

- ตั้ง credential Google และ LINE ให้พร้อมก่อนเริ่ม (หน่วย 09, 11)
- สร้าง Google Sheet เปล่า + แชร์ให้ n8n เข้าถึง แล้วคัดลอก **Sheet ID** จาก URL ไปใส่ใน node
- กำหนด **Drive Folder ID** ให้ถูกโฟลเดอร์ (ก๊อปจาก URL ตอนเปิดโฟลเดอร์นั้น)
- Conditional logic ควรอยู่บน IF node แยกต่างหาก ไม่ฝังใน Code node ล้วน — อ่าน flow ง่ายกว่า
- ทดสอบฟอร์มด้วยการกด Execute workflow แล้วเปิดฟอร์ม preview

## ลงมือทำ

เปิด [exercises/10-workshop-form-to-workspace-line/LAB.md](../../exercises/10-workshop-form-to-workspace-line/LAB.md) — สร้างเองทีละ node (มีเฉลยใน `solution/` เทียบทีหลัง) แล้วทดสอบส่งฟอร์มจริงทั้งกรณีปกติและ HIGH priority

## Check understanding

1. ข้อมูลไหนควรอยู่ใน Sheets และไหนควรอยู่ใน Docs — เกณฑ์ตัดสิน
2. ถ้าผู้ใช้ไม่ระบุวันนัดหมาย flow จะข้าม node ไหน ด้วยเงื่อนไขอะไร
3. LINE แจ้งเฉพาะเคส HIGH — ถ้าอยากให้แจ้งทุกเคสแต่คนละห้อง แก้ตรงไหน

## Next

→ [exercises/10-workshop-form-to-workspace-line](../../exercises/10-workshop-form-to-workspace-line/README.md) — ประกอบระบบจริงทั้งสาย
