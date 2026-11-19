# Lesson 16 — Credential OpenRouter

เนื้อหาสอนประกอบ slide (slides 158–164 (หน้าจอ 151–157)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- OpenRouter = ศูนย์รวมโมเดล (Claude, Llama, GPT, Mistral...) สมัครครั้งเดียวใช้ได้ทุกค่าย มีโมเดล :free
- ถ้าใช้เฉพาะ free ข้ามการเติมได้; เติม Credits เริ่ม $5 ถ้าต้องใช้รุ่นเสียง
- Keys → Create Key (sk-or-v1-...) ตั้ง Credit limit ต่อ key ได้ เช่น $1 — กันตัวเอง
- ใน n8n ใช้ผ่าน node OpenRouter (หรือ OpenAI-compatible endpoint)

## Demo / walkthrough
1. สร้าง key → สร้าง credential → เรียกโมเดล free ผ่าน chat node

## Key takeaways
- OpenRouter เหมาะกับการเทียบโมเดลและ fallback ระหว่าง provider

## Check understanding
- Credit limit ต่อ key ช่วยอะไร
