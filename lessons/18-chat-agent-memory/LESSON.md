# Lesson 18 — Chat Agent + Memory

เนื้อหาสอนประกอบ slide (slides 172–176 (หน้าจอ 165–169)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ทดสอบผ่าน Chat มุมซ้ายล่าง (หรือ message ใน AI Agent node): บอกชื่อ → ถามชื่อตัวเอง → agent ต้องจำได้
- ไม่มี memory = โรคปลาทอง (stateless); Session Key แยกความจำรายคน (เช่น user id จาก LINE กันความจำนาย A ปนนาย B)
- Window Buffer เก็บ N ข้อความล่าสุด ประหยัด token; รุ่นสูง: Postgres/Redis Chat Memory (ถาวร, scale ได้), Conversation Summary (สรุปย่อ ลด token ในบทสนทนายาว), external เช่น Zep/Motorhead

## Demo / walkthrough
1. Import จาก solution/ → เปิดหน้าต่าง Chat → เล่นทดสอบ 2 รอบตาม LAB

## Key takeaways
- LLM ต้องเชื่อมใต้ AI Agent node เสมอ; memory เลือกตามความถาวรที่ต้องการ

## Check understanding
- ต่างกันอย่างไร: Window Buffer กับ Conversation Summary
