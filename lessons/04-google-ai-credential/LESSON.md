# Lesson 14 — Credential Google AI Studio (Gemini)

เนื้อหาสอนประกอบ slide (slides 143–149 (หน้าจอ 136–142)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Google AI Studio → API keys → Create API key (สร้าง/เลือก project, ตั้งชื่อ, copy key)
- นำ key ไปสร้าง credential Google Gemini ใน n8n
- รีวิว workflow LINE Chat Gemini: ข้อความ LINE → AI Agent "จอย" (Gemini 2.5 Flash, ตอบสั้น มี emoji) → Window Buffer Memory 20 ข้อความ แยกตาม user id → ตอบกลับ LINE

## Demo / walkthrough
1. Import workflow จาก solution/ แล้วทัก LINE หาบอท

## Key takeaways
- Gemini key ออกฟรีใน AI Studio — เหมาะเป็นโมเดลแรกของ class

## Check understanding
- Memory แยกตาม user id ทำไมจึงสำคัญ
