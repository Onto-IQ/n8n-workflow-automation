# Lesson 19 — AI Agent + Tools (Function Calling)

เนื้อหาสอนประกอบ slide (slides 177–182 (หน้าจอ 170–175)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Function calling = LLM ตัดสินใจว่าเมื่อไรต้องใช้เครื่องมือภายนอก (คำนวณ, ค้นข้อมูล real-time)
- ReAct 4 จังหวะ: Input → Reasoning (ดู system message เลือก tool) → Action (ส่ง JSON ให้ tool) → Observation & Response (รวมกับ memory แล้วตอบ)
- System prompt คือหัวใจ: ระบุ role + รายการ tool ชัด ๆ + constraint เช่น "You MUST call the appropriate tool first before responding" เพื่อบังคับใช้ tool แทนการเดา (ลด hallucination)
- ทดสอบ: "(3245 * 12) + 897 = ?" → Calculator; "Who founded Apple?" → Wikipedia

## Demo / walkthrough
1. Import จาก solution/ แล้วยิงคำถามทั้งสองแบบ

## Key takeaways
- agent ที่มี tools = digital worker ไม่ใช่แค่แชทบอท

## Check understanding
- ถ้าไม่ใส่ constraint ใน system prompt agent อาจทำอะไร
