# Exercise 25 — Self-Hosting n8n

## Goal
- n8n ของคุณรันบนเครื่องคุณ เข้าได้ผ่านโดเมน HTTPS ของตัวเอง

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. จดโดเมน + เชื่อม Cloudflare + เปลี่ยน nameserver
2. สร้าง Tunnel และเก็บ token
3. ติดตั้ง Docker Desktop → clone repo → cp .env.example .env → กรอกค่าครบ 5 ค่า
4. docker compose up -d → เข้า http://localhost:5678 ตั้ง Owner account
5. ทดสอบ webhook unit 08 ผ่าน Production URL (https://)

## Check your work
- Webhook ทดสอบจากอินเทอร์เน็ตเข้าถึง workflow ผ่านโดเมน HTTPS ของคุณ

## Stretch (optional)
- ['ตั้ง docker compose pull ตามด้วย up -d เพื่ออัปเดต n8n 2.x']
