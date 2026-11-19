# Exercise 10 — Workshop #1: ฟอร์ม → Google Workspace + LINE

## Goal
- ติดตั้งและรันระบบรับเรื่องครบวงจรให้ได้จริง

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/02 - Form to Google Workspace & LINE.json
2. เตรียม Google Sheet (คอลัมน์ Timestamp, Name, Email, Phone, Topic, Urgency, Priority, Appointment, Details, Status) และแชร์ให้ n8n
3. ใส่ Folder ID ใน Google Drive node และเลือก credential ทุก node
4. Execute workflow → เปิดฟอร์มทดลองกรอก 2 เคส: ปกติ และ เร่งด่วน
5. ตรวจผลใน Sheets, Calendar, Docs, Drive และข้อความ LINE

## Check your work
- เคสเร่งด่วนเข้า Sheets + นัดใน Calendar + แจ้ง LINE; เคสปกติไม่ยิง LINE

## Stretch (optional)
- ['แต่งหน้า Thank you ของฟอร์ม (Respond node)']
