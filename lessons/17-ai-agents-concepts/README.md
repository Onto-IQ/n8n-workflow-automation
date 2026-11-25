# 17 — AI Agent คืออะไร / What is an AI agent

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/17-ai-agents-concepts](../../exercises/17-ai-agents-concepts/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 158–164 |

สองสัปดาห์แรกเราสร้าง "workflow" — เส้นทางตายตัวที่เราออกแบบทุกก้าว บทนี้เปลี่ยนมุม: **AI Agent** คือ AI ที่รับเป้าหมายแล้ว "ตัดสินใจเอง" ว่าจะใช้เครื่องมือไหน ทำขั้นไหน จนถึงเป้าหมาย นี่คือหัวใจของยุค "Agent-first, Workflow second"

## Agent กับ Chatbot ต่างกัน

- **Chatbot** — ถาม ตอบ จบ ไม่จำ ไม่ทำอะไรนอกบทสนทนา
- **AI Agent** — ครบ 4 อย่าง: **สั่งได้** (รับเป้าหมาย), **สื่อสารได้** (เข้าใจบริบทรอบตัว), **ทำงานได้** (เรียก tools จริง), **จำได้** (memory) และมี **Orchestration** คอยประสาน — กล่าวคือ Agent = LLM + Memory + Tools + ผู้คุมจังหวะ

## หลักการทำงาน: ReAct Loop

Agent ทำงานวนซ้ำ 5 ขั้น: รับ **User Input** → Agent **Reasons** (คิดแผนตาม system message และ tools ที่มี) → **Act** (เรียก tool เช่น Calculator หรือ Wikipedia ด้วยรูปแบบ JSON) → **Observation & Response** (รับผลลัพธ์ รวมเข้า context แล้วตอบ) — วนซ้ำ (Repeat) จนคิดว่าตอบได้ครบ (Done) เข้าใจ loop นี้ = debug agent ได้: อ่านว่ามันคิดอะไร เรียก tool อะไร ได้ผลอะไรกลับมา

## ประโยชน์ + ข้อจำกัด

- ช่วย: งานที่เส้นทางไม่ตายตัว (ตอบคำถามลูกค้าที่หลากหลาย, วิเคราะห์ข้อมูลที่รูปแบบไม่แน่นอน), รัน 24/7, ยกระดับ workflow เดิมให้ฉลาดขึ้น
- จำกัด: **Accuracy** — อาจ hallucinate ถ้าไม่มี tool ค้นข้อมูลจริงช่วย; เส้นทางสั้นและตายตัว → workflow ธรรมดาเร็วกว่าและถูกกว่า

## เริ่มต้นสร้าง Agent ใน n8n (6 ขั้น)

1. กดปุ่ม Add (canvas) → เลือก **AI Agent** node
2. ต่อ **AI Model** (OpenAI/Gemini/OpenRouter) — สมอง (เชื่อมใต้ AI Agent node เสมอ)
3. ต่อ **Tools** — มือ (Calculator, Wikipedia, HTTP, workflow อื่น)
4. ต่อ **Memory** — ความจำ (หน่วย 18)
5. ต่อ **Chat Trigger** — ปากกับหู
6. รัน **Test & Deploy** — ทดสอบใน chat แล้ว publish

Tip: ลองจาก template ก่อน แล้วค่อยดัดแปลง — เร็วกว่าเริ่มจาก canvas เปล่า

## Demo / walkthrough

วาดผัง agent บนกระดาษ/whiteboard: กล่อง LLM ตรงกลาง ล้อมด้วย Memory, Tools และ Trigger แล้วเทียบว่าแต่ละกล่องคือ node ตัวไหนบน canvas ของ n8n

## Key takeaways

- n8n คือ Orchestrator ที่ประกอบ LLM + Memory + Tools เป็น Agent สำเร็จรูปให้แล้ว

## ลงมือทำ

เปิด [exercises/17-ai-agents-concepts/LAB.md](../../exercises/17-ai-agents-concepts/LAB.md) — ออกแบบ agent บนกระดาษ (starter/agent-design.md) ก่อนลงมือจริงในหน่วย 18

## Check understanding

1. Agent กับ workflow ตายตัว ใช้คนละเมื่อไหร่
2. ReAct loop มีขั้นไหนบ้าง และมันช่วย debug อย่างไร
3. Agent ที่ "ไม่มี memory ไม่มี tools" ยังเรียกว่า agent ได้ไหม เพราะอะไร
4. ขาดส่วนไหนแล้ว agent จะ "โกง" เดาคำตอบแทนการหาข้อมูลจริง (hallucination)

## Next

→ [exercises/17-ai-agents-concepts](../../exercises/17-ai-agents-concepts/README.md) — ออกแบบ agent แรกบนกระดาษ
→ บทถัดไป: [18 — Chat Agent + Memory](../18-chat-agent-memory/README.md)
