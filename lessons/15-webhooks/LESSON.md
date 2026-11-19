# Lesson 08 — Webhooks & Triggers

เนื้อหาสอนประกอบ slide (slides 69 (หน้าจอ 62)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Webhook = เปิดประตูรับข้อมูล (ข้อความ LINE, form, ระบบอื่น) — จุดเริ่มสำคัญของ AI Agent ที่โต้ตอบกับผู้ใช้
- Test URL ใช้กับ Listen for Test Event; Production URL ใช้เมื่อ workflow Active
- Response Mode = Using Respond to Webhook Node แล้วส่งกลับด้วย node นี้ (ดึง $json.body.name มาประกอบข้อความ)
- HTTPS จำเป็นสำหรับ production webhook — บริการภายนอกยอมเฉพาะ https:// (ดู SETUP.md)

## Demo / walkthrough
1. สร้าง Webhook → กด Listen for Test Event → ยิง POST {"name":"Student"} จาก Postman/curl

## Key takeaways
- Test URL กับ Production URL คนละตัว อย่าสับสนตอน deploy

## Check understanding
- ทำไม LINE ไม่ยอมยิง webhook เข้า http://
