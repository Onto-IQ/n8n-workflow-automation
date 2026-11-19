# Lesson 17 — AI Agent คืออะไร

เนื้อหาสอนประกอบ slide (slides 165–171 (หน้าจอ 158–164)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Agent = รับคำสั่ง → วางแผน → ตัดสินใจ → ลงมือทำ เรียก Tools/APIs ได้ มี Memory; chatbot ทั่วไปแค่ถาม-ตอบ
- องค์ประกอบใน n8n: LLM (Brain, ต่อใต้ AI Agent node เสมอ) + Memory + Tools + n8n Orchestrator
- ReAct loop: Think → Act → Observe → Repeat/Done
- ขั้นสร้างใน n8n: AI Agent node → เลือก model → ใส่ Tools → ใส่ Memory → เชื่อม trigger → ทดสอบแล้ว Activate (เริ่มจาก template แล้วปรับ)

## Demo / walkthrough
1. วาดผัง agent บนกระดาษ/whiteboard ตาม slide 167 แล้วเทียบกับ node ใน n8n

## Key takeaways
- n8n คือ Orchestrator ที่ประกอบ LLM+Memory+Tools เป็น Agent สำเร็จรูป

## Check understanding
- ส่วนไหนขาด agent จะ "โกง" คำตอบแทนการหาข้อมูลจริง (hallucination)
