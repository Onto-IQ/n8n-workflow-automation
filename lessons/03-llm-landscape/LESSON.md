# Lesson 12 — สถานการณ์ LLM ปี 2026

เนื้อหาสอนประกอบ slide (slides 120–129 (หน้าจอ 113–122)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Context is the new gold: window 1M–2M tokens (จนถึง infinite context) — Context Engineering สำคัญกว่าการ retrain
- Context Caching (Gemini/DeepSeek): จำข้อมูลมหาศาลไว้ฝั่ง provider ลด cost+latency มากเมื่อข้อมูลนิ่ง
- Dynamic Memory & Compaction: สรุปย่อบริบทเก่าเป็น long-term memory อัตโนมัติ
- LLM API ยัง stateless — agent บน n8n ที่จำผู้ใช้ข้ามวันต้องมี Memory ของตัวเอง หรือใช้ Stateful API (เช่น Assistants/Thread) ซึ่งแลกด้วย vendor lock-in + คุม cost ยาก
- AI+Automation = Orchestrator: Trigger → Process → AI Node → Action; ตัวอย่างธุรกิจ: support, สรุปเอกสาร, content, รายงานรายวัน, email classification, e-commerce personalization

## Demo / walkthrough
1. จากหน้าจอ 121–123 สรุปด้วยกราดฟึก 3 คำถามใน LAB

## Key takeaways
- n8n ได้ประโยชน์จาก cache ของ provider เต็ม ๆ แต่ memory ข้าม session ยังต้องจัดการเอง

## Check understanding
- เมื่อไรควรใช้ Stateful API แม้จะ lock-in
