# Exercise 08 — Webhooks & Triggers

## Goal
- รับ POST เข้า n8n แล้วตอบกลับแบบไดนามิก

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สร้าง Webhook node (method POST, response = Respond to Webhook Node)
2. ต่อด้วย Set node สร้างข้อความตอบกลับจาก $json.body.name
3. ปิดท้ายด้วย Respond to Webhook
4. กด Listen for Test Event แล้วยิง curl -X POST พร้อม JSON {"name":"<ชื่อคุณ>"}

## Check your work
- ผู้เรียกได้รับข้อความตอบกลับที่แทนชื่อของคุณถูกต้อง

## Stretch (optional)
- ['Activate workflow แล้วยิงเข้า Production URL']
