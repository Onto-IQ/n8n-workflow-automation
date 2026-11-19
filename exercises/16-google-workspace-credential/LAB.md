# Exercise 09 — Credential Google Workspace (OAuth2)

## Goal
- เชื่อม Google Workspace เข้า n8n สำเร็จ 1 บริการ (Gmail) และพร้อมใช้ที่เหลือ

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สร้าง Project ชื่อ n8n-student-course ใน Google Cloud Console
2. ตั้ง OAuth consent screen: App name + email → User type External → เพิ่มตัวเองเป็น Test user → Publish App (In production)
3. Enable APIs: Gmail, Google Sheets, Google Drive, Google Docs, Google Calendar
4. สร้าง Credentials → OAuth client ID → Web application → วาง OAuth Redirect URL จาก n8n
5. กลับมาที่ n8n: สร้าง credential ประเภท Google OAuth2 → วาง Client ID/Secret → Connect → อนุญาต

## Check your work
- credential แสดงสถานะเชื่อมต่อแล้ว และทดสอบส่งเมลด้วย Gmail node ได้

## Stretch (optional)
- ['สร้าง Google Sheet ทดลองแล้ว Append แถวด้วย Sheets node']
