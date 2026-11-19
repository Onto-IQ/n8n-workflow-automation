# Exercise 19 — AI Agent + Tools (Function Calling)

## Goal
- agent ที่เลือกใช้ Calculator/Wikipedia ได้ถูกงาน

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/02 - AI Agent with Tools.json
2. อ่าน system message แล้ว Execute ทดสอบสองคำถามมาตรฐาน
3. ถามคำถามกล组件ที่ต้องคำนวณ + ค้นข้อมูลปนกัน แล้วดู execution ว่าเรียก tool ไหนกี่ครั้ง
4. แก้ constraint ใน system message แล้วเทียบพฤติกรรม

## Check your work
- execution log แสดงการเรียก tool ตรงตามคำถาม และคำตอบมีข้อมูลจริง

## Stretch (optional)
- ['เพิ่ม HTTP Request tool ใหม่ (เช่น API อากาศ) ให้ agent']
