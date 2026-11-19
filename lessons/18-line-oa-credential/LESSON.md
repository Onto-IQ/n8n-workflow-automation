# Lesson 11 — Credential LINE OA

เนื้อหาสอนประกอบ slide (slides 101–119 (หน้าจอ 94–112)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ขั้นทาง LINE Developers Console: สร้าง Provider → สร้าง Messaging API channel → เปิด Messaging API จาก LINE OA Manager
- ติดตั้ง Community Node "LINE Messaging" (Settings → Community nodes) ก่อนใช้ node
- Credential ต้องมี 2 ค่า: Channel Secret + Channel Access Token (กด Issue ได้ใน console) และเอา Webhook URL จาก n8n ไปวางใน Messaging API ของ LINE

## Demo / walkthrough
1. เดิน console ทีละหน้าตาม LAB แล้วกลับมาตรวจ Settings ใน n8n

## Key takeaways
- Webhook URL ต้องอยู่ฝั่ง LINE ด้วย — สองฝั่งต้องพร้อมจึงคุยกันได้

## Check understanding
- Channel Secret กับ Channel Access Token ใช้ทำอะไรต่างกัน
