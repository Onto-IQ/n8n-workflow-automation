# Exercise 07 — เรียกใช้ External APIs

## Goal
- ดึงมุกจาก public API แล้วส่งต่อด้วย POST

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สร้าง workflow ใหม่: Manual Trigger → HTTP Request (GET random_joke)
2. Execute แล้วดูโครงสร้าง response
3. ต่อด้วย HTTP Request (POST httpbin.org/post) body = { "setup": ..., "punchline": ... } ใช้ expression ดึงจาก node ก่อนหน้า
4. Execute แล้วดู echo จาก httpbin

## Check your work
- httpbin ตอบกลับ body ที่ส่งไปครบทั้งสอง field

## Stretch (optional)
- ['เปลี่ยนเป็นเรียก API ที่ต้องใช้ Header Auth แล้วดู error 401 เมื่อใส่ key ผิด']
