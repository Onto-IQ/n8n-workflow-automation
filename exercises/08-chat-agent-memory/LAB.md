# Exercise 18 — Chat Agent + Memory

## Goal
- agent ที่จำชื่อและบริบทของคุณได้ตลอดบทสนทนา

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/01 - Basic Chat Agent & Memory.json
2. ตรวจ 3 ส่วน: Chat Trigger → AI Agent (เลือก model + system message) → Window Buffer Memory (context window 5)
3. พิมพ์ "ฉันชื่อ<ชื่อคุณ>" แล้วถามต่อ "ฉันชื่ออะไร?"
4. ปิด memory node แล้วถามซ้ำ — สังเกต agent ลืมทันที แล้วเปิดคืน

## Check your work
- agent ตอบชื่อถูกเมื่อเปิด memory และลืมเมื่อปิด

## Stretch (optional)
- ['เปลี่ยนเป็น Postgres Chat Memory แล้ว restart workflow ทดสอบความถาวร']
