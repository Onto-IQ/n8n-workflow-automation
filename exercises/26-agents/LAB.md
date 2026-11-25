# Exercise 26 — n8n Agents: Agent Builder

## Goal
- สร้างและ publish Agent "ผู้ช่วยออฟฟิศ" ที่ตอบคำถามจาก FAQ ดึงเมลล่าสุดได้ คุยผ่าน Telegram และถูกเรียกจาก workflow ด้วย Message an Agent

## Setup
1. เปิด n8n ยืนยันว่าเวอร์ชัน ≥ 2.32.3 (มุมซ้ายล่าง) และเห็นแท็บ **Agents** ใน project — ถ้าไม่เห็น ให้อัปเกรด stack ตาม `lessons/25-self-hosting` ก่อน (`docker compose pull && docker compose up -d`)
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
3. เปิด `starter/agent-blueprint.md` กรอกแผน agent ของคุณให้ครบก่อนแตะ UI
4. เลือก project → แท็บ **Agents** → **Create Agent** ตั้งชื่อ (เช่น `office-assistant`) + เลือกไอคอน
5. เลือก **Model** จาก credential โมเดลที่มี (ต้องรองรับ tool calling) แล้วเขียน **Instructions** ภาษาไทยจาก blueprint — บทบาท ขอบเขต กฎ "ตอบจาก FAQ tool ก่อนเสมอ"
6. ทดสอบใน **Preview** ด้วยคำถามทดลอง 1 ข้อ ปรับ instructions จนน้ำเสียง/ขอบเขตถูกใจ
7. Import `solution/02 - Agent Tool - Company FAQ.json` → **Publish** workflow นี้ → กลับมาที่ agent เพิ่มเป็น **workflow tool** ตั้งชื่อ tool ให้สื่อความ (เช่น `lookup_company_faq`)
8. เพิ่ม **Gmail tool** (integration สำเร็จรูป — ดึงเมลล่าสุด) แล้วเปิด **require approval** ที่ tool นี้
9. ต่อ **Telegram channel** ด้วย Telegram credential (ต้องมี `WEBHOOK_URL` เป็น https สาธารณะ — หน่วย 25)
10. เพิ่ม **Schedule** digest รายวัน (เวลาที่เลือกได้) แล้วกด **Publish** agent → เปิด publish history ดูเวอร์ชันแรก
11. แก้ instructions เพิ่มอีก 1 ประโยค → **Publish** ซ้ำ → ลองใช้ publish history ย้อนดูความต่างสองเวอร์ชัน
12. Import `solution/01 - Message an Office Assistant.json` เลือก agent ของคุณใน node **Message an Agent** แล้ว Execute — อ่าน `text` กับ `toolCalls` ใน output
13. ทดสอบผ่าน Telegram: ทักบอท ถามคำถาม FAQ และขอ "ดูเมลล่าสุด" — รับช่องอนุมัติ (Approve/Reject) ให้ครบ
14. ปิดท้ายที่แท็บ **Sessions** — ย้อนดูว่า agent เรียก tool อะไร ตอบอะไร

## Check your work
- Publish history มีอย่างน้อย 2 เวอร์ชัน และ agent ยังตอบได้หลังแก้ instructions
- การเรียกจาก workflow ได้ `text` ที่ตอบตาม FAQ และเห็น `toolCalls` ชี้ไปที่ `lookup_company_faq`
- ใน Telegram ขอดูเมลแล้วมีคำขออนุมัติขึ้น และงานทำต่อได้หลังกด Approve
- แท็บ Sessions มีบทสนทนาจากทั้ง Preview, Telegram และ workflow อย่างละอย่างน้อย 1 รายการ

## Stretch (optional)
- สร้าง agent ที่สอง (เช่นผู้เชี่ยวชาญเรื่องการลา/วันหยุด) publish แล้วผูกเป็น **sub-agent** ของ office-assistant พร้อมเขียน "เมื่อไรควรใช้"
- เปิด **structured output** ที่ node Message an Agent ให้ตอบเป็น JSON ตาม schema ที่กำหนด แล้วนำ `structuredOutput` ไปต่อ node ถัดไป
- เพิ่ม **skill** ร่วม (เช่น "มารยาทการตอบแบบองค์กรไทย") แล้วใช้ซ้ำกับ agent ตัวอื่น
