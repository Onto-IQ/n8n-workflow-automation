# Exercise 13 — Workshop #2: คัดกรองใบสมัครจาก Gmail

## Goal
- รันระบบคัดกรองจนได้ผลคะแนนจริงใน Sheets

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/03 - Candidate Screening from Gmail.json
2. ตั้ง Gmail Trigger ให้ตรง mailbox HR ของคุณ + แก้ YOUR_JOB_DESC_FILE_ID และ YOUR_SHEET_ID
3. เตรียม Sheets header: Received At, Email, Firstname, Lastname, Gender, Age, Education, Matching Score, Hire, Recommendation, Subject
4. ส่งอีเมลแนบ resume (ไฟล์ตัวอย่างใน other/datasets/JD and Resume/) เข้า mailbox
5. ตรวจผลคะแนนใน Sheets และอีเมลตอบกลับ

## Check your work
- แถวใหม่ใน Sheets มีคะแนน + คำแนะนำจาก AI และผู้สมัครได้รับอีเมลยืนยัน

## Stretch (optional)
- ['เพิ่มเงื่อนไข score < 60 ส่งแจ้งทีมผ่าน LINE']
