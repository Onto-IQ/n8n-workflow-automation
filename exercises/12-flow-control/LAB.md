# Exercise 04 — Flow Control: IF, Switch, Merge

## Goal
- สร้างระบบจัดเกรดนักเรียน: ข้อมูลจำลอง → IF (VIP?) → Switch (score) → Merge

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/02-Flow-Control-Demo.json
2. ไล่ดูทีละ node: Code สร้างข้อมูล → IF → Switch → Merge (mode Append)
3. Execute workflow แล้วสังเกต item วิ่งทางไหนบ้างและเพราะอะไร
4. แก้ค่า score ใน Code node เป็น 90/60/30 แล้วรันซ้ำ สังเกตเส้นทางเปลี่ยน

## Check your work
- ทุกค่า score เดินทางถูกสาย และ Merge รวมผลครบทุกกรณี

## Stretch (optional)
- ['เพิ่มเกรด C (50–69) โดยแก้ expression ของ Switch']
