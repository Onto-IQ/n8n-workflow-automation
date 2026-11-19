# Exercise 22 — Workshop #3: RAG ด้วย Pinecone

## Goal
- ระบบถามตอบคู่มือองค์กรบน Pinecone ที่ข้อมูลไม่หาย

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. สมัคร pinecone.io → สร้าง Project n8n-rag-course → สร้าง Index n8n-demo-index (dim 1536, cosine)
2. สร้าง API key แล้วทำ credential Pinecone ใน n8n
3. Import ไฟล์ solution/04 - RAG with Pinecone (Load + Query).json แล้วแก้ YOUR_DRIVE_FOLDER_ID
4. Execute ส่วน Load → Chat ถาม: นโยบายลา, ขั้นเบิกจ่าย, ติดต่อ IT
5. ตรวจ index stats ใน Pinecone console

## Check your work
- มี vector count ใน index และ chat ตอบจากเอกสารได้ 3 คำถาม

## Stretch (optional)
- ['ทดลอง metadata filtering แยกเอกสารตาม department']
