# Lesson 02 — เริ่มต้น Workflow แรก

เนื้อหาสอนประกอบ slide (slides 37–58 (หน้าจอ 30–51)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- โครงสร้างพื้นฐาน: Trigger → Node → Node เรียงต่อกัน
- Trigger 5 กลุ่ม: Manual (กดปุ่ม ใช้ทดสอบ), Schedule (ตามเวลา เช่น ตี 5), App Event (เหตุการณ์ในแอป เช่น แถวใหม่ใน Google Sheet), Webhook Call (ยิง HTTP มา), On form submission (ฟอร์มใน n8n)
- ทิศทางการทำงาน: Sequential (default ทำทีละ node รอก่อนจบ) กับ Parallel (ทำพร้อมกัน ต้องตั้งค่า)
- หน้าจอ node: กำหนดรายละเอียด → Execute step → ดู Input/Output แยกชัด

## Demo / walkthrough
1. กด + บน canvas → เลือก Trigger manually
2. กด + ถัดไป → เลือก Gmail → Send a message → กรอก To/Subject/Message
3. Execute workflow → ดับเบิลคลิก node เพื่อดู output

## Key takeaways
- ทุก workflow เริ่มที่ trigger เสมอ
- ทดสอบด้วย Manual trigger ก่อนเสมอ แล้วค่อยเปลี่ยนเป็น trigger จริง

## Check understanding
- Workflow เริ่มที่ไหนเสมอ?
- อยากให้รันทุกวันตอนตี 5 ใช้ trigger ตัวไหน
