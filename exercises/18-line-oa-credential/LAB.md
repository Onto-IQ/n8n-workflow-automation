# Exercise 11 — Credential LINE OA

## Goal
- LINE credential พร้อมใช้และทดสอบ webhook ติดได้

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สร้าง Provider + Messaging API channel บน developers.line.biz
2. ติดตั้ง community node LINE Messaging ใน n8n (Settings → Community nodes → ตรวจใน Settings หลังติดตั้ง)
3. Issue Channel Secret + Channel Access Token แล้วนำมาสร้าง credential ใน n8n
4. คัดลอก Webhook URL จาก n8n ไปใส่ที่ Messaging API settings ของ LINE แล้วกดบันทึก

## Check your work
- LINE แสดง webhook Verified (หรือส่งข้อความเข้า OA ทดสอบได้)

## Stretch (optional)
- ['เปิดใช้ webhook ของ LINE กับ workflow ทดลอง echo ข้อความ']
