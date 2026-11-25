# 19 — AI Agent + Tools (Function Calling) / Agent with tools

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/19-agent-with-tools](../../exercises/19-agent-with-tools/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 170–175 |
| เฉลย | `exercises/19-.../solution/02 - AI Agent with Tools (Function Calling).json` |

LLM เก่งแต่ "พูดอย่างเดียว" — Function Calling ทำให้มัน **ลงมือทำ** โมเดลตัดสินใจเองว่าเมื่อไรต้องใช้เครื่องมือภายนอก (คำนวณ, ค้นข้อมูล real-time) แล้วเรียกเองตามงาน บทนี้สร้าง agent ที่มีมือจริง: ตัวอย่างคอร์สใช้ Calculator (คำนวณแม่น) + Wikipedia (ค้นข้อมูลจริง)

## Function Calling คืออะไร

เราอธิบายให้ LLM รู้ว่า "มี tools อะไรให้ใช้" มันจะวิเคราะห์คำสั่งแล้วส่งคำสั่งรูปแบบ JSON เรียก tool ที่เหมาะสมในเวลาจริง แทนที่จะตอบด้วยการเดา — ผลคือความแม่นยำจริง (เลข ๆ จากเครื่องคิดเลข ไม่ใช่การเดาของโมเดล) และความสามารถที่ขยายได้ (เรียก CRM, Database, Weather API ก็ได้)

## กลไกการทำงาน (ReAct 4 ขั้น)

1. **Input** — ผู้ใช้พิมพ์ผ่าน Chat Trigger
2. **Reasoning** — Agent คิดตาม System Message และรายการ tools
3. **Action (Function Call)** — ส่ง JSON เรียก tool ที่เลือก เช่น Calculator กับนิพจน์ที่ควรคำนวณ
4. **Observation & Response** — รับผลลัพธ์ tool กลับมา รวมเข้า context แล้วเรียบเรียงตอบ

## องค์ประกอบของ AI Agent ใน n8n

- **Brain (The Model)** — เช่น GPT-4o-mini เป็นตัวตัดสินใจหลัก
- **Memory** — Window Buffer Memory จำบทสนทนาล่าสุด 5 รอบ
- **Tools (The Hands)** — เครื่องมือที่ยอมให้เรียก เช่น Calculator, Wikipedia
- **System Prompt** — กติกาการทำงาน เช่น "You are a helpful AI assistant with access to various tools", "You MUST call the appropriate tool first before responding" — ประโยคบังคับชัด ๆ ช่วยลดการตอบเดา

## ข้อดีและธุรกิจ

**Accuracy** (ลด hallucination ด้วย tool อ้างอิงจริง), **Extended capability** (ต่อ CRM/Database/Weather/HTTP ได้ไม่จำกัด), **Automation** (จาก chatbot สู่ "Digital Worker" ที่ทำงานจริงได้)

## Key takeaways

- agent ที่มี tools คือ digital worker ไม่ใช่แค่แชทบอท
- ถ้าไม่ใส่ constraint ใน system prompt agent จะย้อนกลับไปเดาคำตอบเอง

## ลงมือทำ

เปิด [exercises/19-agent-with-tools/LAB.md](../../exercises/19-agent-with-tools/LAB.md) — import `solution/02 - AI Agent with Tools (Function Calling).json` แล้วทดสอบ: ถามโจทย์คำนวณ `(3245 * 12) + 897 = ?` (ต้องเรียก Calculator), ถามข้อมูลนอกความรู้โมเดล `Who founded Apple?` (ต้องเรียก Wikipedia) และดู call log ของ agent

## Check understanding

1. ทำไมเลขคำนวณจาก Calculator น่าเชื่อกว่าคำตอบจากโมเดล
2. System prompt ประโยคไหนห้าม agent ตอบโดยไม่เรียก tool
3. อยากให้ agent อ่านข้อมูลจาก Google Sheets ของบริษัท — เพิ่ม tool แบบไหน
4. ถ้าลืมใส่ constraint ใน system prompt จะเกิดอะไรขึ้น

## Next

→ [exercises/19-agent-with-tools](../../exercises/19-agent-with-tools/README.md) — สร้าง agent ที่มีมือเรียก tool จริง
→ บทถัดไป: [20 — Simple RAG + Memory](../20-simple-rag-memory/README.md)
