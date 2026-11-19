# Lesson 13 — Workshop #2: คัดกรองใบสมัครจาก Gmail

เนื้อหาสอนประกอบ slide (slides 131–141 (หน้าจอ 124–134)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Pipeline: Gmail Trigger (หัวข้อมี สมัครงาน/Resume/CV, มีแนบ) → Code เตรียม candidate object → IF มี resume → Loop ทีละไฟล์ → Switch แยกประเภท (PDF/DOCX/TXT) → Extract From File (binary → text) → โหลด JD จาก Drive → AI Agent + Structured Output Parser (บังคับ JSON: ชื่อ อายุ คะแนน เหตุผล) → Sheets → Gmail ตอบกลับ
- หัวใจคือ prompt บทบาท "HR ผู้เชี่ยวชาญ ตอบเป็น JSON เท่านั้น" + Output Parser เพื่อลงตารางได้ทันที

## Demo / walkthrough
1. Import จาก solution/ แล้วส่งอีเมลสมัครงานทดลองเข้า mailbox ที่ trigger ฟังอยู่

## Key takeaways
- Binary → Text → AI → Structured output คือแพตเทิรับไฟล์ที่ใช้ได้กับทุกงานเอกสาร

## Check understanding
- ถ้าไม่มี Output Parser จะเกิดอะไรขึ้นเวลาลง Sheets
