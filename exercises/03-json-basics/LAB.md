# Exercise 03 — JSON พื้นฐานสำหรับ n8n

## Goal
- เข้าใจข้อมูลที่ไหลใน n8n ผ่าน workflow สอน JSON

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/01-Learn-JSON-Basics.json
2. Execute workflow แล้วเปิดดู output ของแต่ละ node ทีละตัว
3. ใน node สุดท้าย แก้ expression ให้ดึง field ที่โจทย์กำหนดใน LAB แบบฝึกหัด
4. สร้าง Code node ใหม่คืนค่า object ของตัวเอง: ชื่อ อายุ รายการโปรด (array)

## Check your work
- output ของ Code node แสดง object ตามที่กำหนด และทุก expression ไม่ error

## Stretch (optional)
- ['ใช้ $node["ชื่อ node เก่า"].json... ดึงค่าย้อนกลับ 3 node']
