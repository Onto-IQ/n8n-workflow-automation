# Lesson 09 — Credential Google Workspace (OAuth2)

เนื้อหาสอนประกอบ slide (slides 71–90 (หน้าจอ 64–83)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Credential = ที่เก็บกลางของ secret (API key/OAuth2/DB) — ปลอดภัยกว่า, rotate ง่าย, reuse ข้าม workflow (ประเภทที่เจอบ่อย: API key/token, OAuth2 ซึ่ง n8n refresh token ให้เอง, database)
- ขั้น Google: สร้าง Project → OAuth consent screen (Google Auth Platform: Branding/Audience) → เพิ่ม Test users → Publish App (เลี่ยง token หมดอายุ 7 วัน) → Enable APIs (Gmail, Sheets, Drive, Docs, Calendar) → สร้าง OAuth client ID (Web application) โดยวาง OAuth Redirect URL จากหน้า credential ของ n8n
- Client ID + Client Secret ชุดเดียวใช้ร่วมทุก service ของ Google Workspace ได้

## Demo / walkthrough
1. เดินตาม LAB ทีละขั้นบน console.cloud.google.com พร้อมเปิดหน้า credential ของ n8n ค้างไว้

## Key takeaways
- ขาด Publish App → token หมดอายุทุก 7 วัน; ขาด Redirect URL → connect ไม่ผ่าน

## Check understanding
- Redirect URL เอามาจากไหน
- ทำไมต้อง Enable APIs ทีละตัว
