# 12 — สถานการณ์ LLM ปี 2026 / The LLM landscape in 2026

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/12-llm-landscape](../../exercises/12-llm-landscape/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 113–122 |

ก่อนต่อ AI เข้ากับ n8n (หน่วย 13–23) ต้องเห็นสนามจริงก่อน: โมเดลเปลี่ยนเร็ว ราคาต่างกันมาก และมีเทคนิคที่เปลี่ยนเกมอยู่ 3 เรื่อง บทนี้ไม่ต้องเขียนอะไร — แต่การเลือกผิดตรงนี้ทำให้งานจริงช้าและแพงโดยไม่จำเป็น

## Technical landscape ที่เปลี่ยนไป

1. **Context is the New Gold** — context window ขยายจาก 4K/8K เป็นระดับ 1M–2M tokens และมี "Infinite Context" ผ่าน Retrieval/Context Engineering — แต่ context ยักษ์ไม่ฟรี: latency กับค่าใช้จ่ายสูงตาม จึงต้องใช้ร่วมกับ caching
2. **Memory Architecture & Caching** — Gemini กับ DeepSeek นำ Context Caching มาให้: cache system prompts หรือข้อมูลงานซ้ำ ๆ ลด latency/ต้นทุนชัดเจน (ยิ่งข้อมูลนิ่ง ยิ่งคุ้ม)
3. **Dynamic Memory & Compaction** — Memory node ของ AI agent มี auto-compaction สรุปงานเก่าเป็น long-term memory ให้ scope การจำกว้างขึ้นโดยไม่พาตัวหนัก

## ทำไม n8n ได้ประโยชน์ทันที

- **เปลี่ยน model ได้ในคลิก** — Gemini, Anthropic, DeepSeek, ผู้ให้บริการในประเทศ สลับได้โดยไม่แตะ logic
- **ระวังเรื่อง 3 ตัวนี้**: **Cost** (โมเดลวัสดุถูกวันนี้อาจแพงพรุ่งนี้), **Latency** (โมเดลใหญ่ช้าเป็นวินาที), **Stateful API** (โมเดล Chat ยุคใหม่เก็บ memory ฝั่ง provider เอง เช่น Assistants/Thread — ถ้าเก็บ Thread_ID ใน n8n ให้วางแผนเรื่อง memory ให้ชัด) จำไว้ว่า LLM API พื้นฐานยัง **stateless** — agent ที่ต้องจำผู้ใช้ข้ามวันต้องมี Memory ของตัวเองบน n8n หรือยอมใช้ Stateful API ซึ่งแลกด้วย vendor lock-in และคุม cost ยาก
- หน้าที่ n8n คือ **orchestrator**: เลือกใช้ model ให้เหมาะกับงาน ต่อข้อมูลองค์กรเข้ากับ AI และคุมต้นทุน — สูตรทั่วไป: Trigger → Process → AI Node → Action ใช้ได้ทั้งงาน support, สรุปเอกสาร, สร้าง content, รายงานรายวัน, จัดหมวดอีเมล และ personalization ฝั่ง e-commerce

## นัยต่อการเรียนส่วนที่เหลือ

หน่วย 13 ใช้ AI อ่านเรซูเม่, หน่วย 17–20 สร้าง agent พร้อม memory/RAG, หน่วย 21–23 ต่อ MCP และ multi-agent — ทั้งหมดยึดหลักเดียวกัน: **โมเดลคือชิ้นส่วนที่สลับได้ สถาปัตยกรรมบน n8n คือของคุณ**

## Key takeaways

- n8n ได้ประโยชน์จาก context cache ของ provider เต็ม ๆ — แต่ memory ข้าม session ยังต้องจัดการเองบน n8n

## ลงมือทำ

เปิด [exercises/12-llm-landscape/LAB.md](../../exercises/12-llm-landscape/LAB.md) — เติม decision matrix เลือกโมเดลให้สามสถานการณ์งานจริง (คุ้มค่า / เร็ว / ละเอียดสุด) พร้อมเหตุผล

## Check understanding

1. Context caching ช่วยอะไร และงานลักษณะไหนเห็นผลชัด
2. "Stateful API" ของ Chat Model ยุคใหม่ทำให้การออกแบบ memory ใน n8n ต้องคิดต่างอย่างไร
3. งานคัดกรองเอกสารจำนวนมาก ควรเลือกโมเดลแบบไหนเป็นกำลังหลัก เพราะอะไร
4. เมื่อไรควรยอมใช้ Stateful API แม้รู้ว่าจะเจอ vendor lock-in

## Next

→ [exercises/12-llm-landscape](../../exercises/12-llm-landscape/README.md) — ฝึกตัดสินใจเลือกโมเดลก่อนลงมือ
→ บทถัดไป: [13 — Workshop #2: คัดกรองใบสมัครจาก Gmail](../13-workshop-candidate-screening/README.md)
