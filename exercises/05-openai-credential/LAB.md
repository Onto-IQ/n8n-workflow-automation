# Exercise 15 — Credential OpenAI

## Goal
- OpenAI credential ใช้งานได้จริงภายในงบที่ตั้ง

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สมัคร/ล็อกอิน platform.openai.com แล้วตั้ง Billing + limits ตาม slide
2. สร้าง secret key ชื่อ n8n Class Key แล้วเก็บใน password manager
3. สร้าง credential OpenAI ใน n8n ผ่าน node OpenAI Chat Model
4. ทดสอบ: node Chat ถาม "ทดสอบ 1+1" แล้วดูค่า token ที่ใช้ใน execution

## Check your work
- node ตอบกลับสำเร็จโดยไม่ผ่าน limit ที่ตั้ง

## Stretch (optional)
- ['เทียบความเร็ว gpt-4o-mini กับ gpt-4o ด้วย prompt เดียวกัน']
