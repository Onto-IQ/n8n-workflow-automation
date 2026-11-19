# Lesson 15 — Credential OpenAI

เนื้อหาสอนประกอบ slide (slides 151–156 (หน้าจอ 144–149)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ระวัง: API ไม่ฟรีเหมือนแชทเว็บ คิดตาม token, ต้องเติมขั้นต่ำ $5, แยกบิลจาก ChatGPT Plus
- Billing: เลือก Individual/Company → ผูกบัตร → ปิด Auto-recharge → ตั้ง Usage limit (เตือน $10 / ตัด $15)
- API keys → Create new secret key (sk-proj-...) — เห็นครั้งเดียว ต้อง copy เก็บทันที
- ใน n8n: เพิ่ม node หมวด Advanced AI (OpenAI Chat Model) → Create New Credential → วาง key → Save

## Demo / walkthrough
1. เดินตาม LAB แล้วทดสอบด้วย node OpenAI Chat Model ง่าย ๆ

## Key takeaways
- ตั้ง Usage limit ก่อนเสมอ — กันบิลพุ่งจาก loop ที่ผิดพลาด

## Check understanding
- Auto-recharge ควรเปิดหรือปิดตอนเรียน เพราะอะไร
