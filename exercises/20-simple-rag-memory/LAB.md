# Exercise 20 — Simple RAG + Memory

## Goal
- chatbot ตอบจากเอกสารนโยบายจริง + จำบทสนทนา

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/03 - Simple RAG with Memory.json
2. Execute ส่วน Load Data จน vector store ถูกเติม
3. เปิด Chat ถาม 5 คำถามตาม LAB: เบี้ยเลี้ยงญี่ปุ่น, วงเงินโรงแรม manager, ขั้นอนุมัติต่างประเทศ, รถส่วนตัวขอนแก่น, บัตรเครดิตบริษัท
4. ถามต่อเนื่อง "แล้วเกาหลีล่ะ?" เพื่อทดสอบ memory + RAG พร้อมกัน

## Check your work
- ตอบได้ครบ 5 คำถามจากเอกสาร และเข้าใจสรรพนามในคำถามต่อเนื่อง

## Stretch (optional)
- ['เพิ่มเอกสารนโยบายของคุณเองจาก other/datasets/ เข้า load flow']
