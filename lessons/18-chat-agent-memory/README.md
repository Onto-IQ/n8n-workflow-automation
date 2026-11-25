# 18 — Chat Agent + Memory / Chat agent with memory

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/18-chat-agent-memory](../../exercises/18-chat-agent-memory/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 165–169 |
| เฉลย | `exercises/18-.../solution/01 - Basic Chat Agent & Memory.json` |

ทำไม agent ต้องมี memory? เพราะโมเดล **Stateless** — ลืมทุกอย่างทันทีที่ request จบ คุยคำถามที่ 5 โดยไม่มี memory = agent ไม่รู้ว่าคำถามที่ 1–4 คืออะไร Memory จึงทำให้ agent มี "บริบทต่อเนื่อง" และตอบต่อเนื่องได้เหมือนคุยกับคน บทนี้สร้าง Chat Agent ตัวแรกที่จำบทสนทนาได้จริง

## ปัญหาที่ memory แก้

- **The Goldfish Problem** — agent ลืมบทสนทนา
- **Contextual Awareness** — ต้องรู้ว่า "มัน"/"อันนั้น"/"เมื่อกี้" หมายถึงอะไร
- **User Experience** — จาก single-turn เป็น multi-turn conversation ที่ใช้งานจริงได้

## Memory ใน n8n (Modern AI Nodes)

- **Window Buffer Memory** (ในตัว) — จำบทสนทนาล่าสุดตามจำนวน "โทเคน/รอบ" ที่ตั้ง (ค่าเริ่ม 5 รอบ) ทำงานใน RAM วิ่งเร็ว หายเมื่อ workflow reset/restart — เหมาะกับงานสาธิตและ chat ทั่วไป
- **Session Key** — แยกห้องสนทนาต่อผู้ใช้: กำหนด session_id จาก LINE/Facebook user ให้คนละคนไม่เห็นคุยกัน
- **Database-backed Memory** — Postgres Chat Memory (ถาวรรอด restart), Redis (เร็ว, หมดอายุได้) — เข้าสู่ production
- **Summarization Memory** — agent สรุปงานเก่าเป็นย่อหน้าต่อเนื่อง จำยาวขึ้นโดยไม่พา context บวม

## ลงมือทำ: สร้าง Basic Chat Agent & Memory

1. Chat Trigger → AI Agent → OpenAI Chat Model
2. ต่อ **Window Buffer Memory** (ค่า default 5)
3. ปรับ prompt/system message ให้มีบุคลิก
4. ทดสอบ: ทักไป 4–5 ที อ้างอิงสิ่งที่คุยก่อนหน้า — agent ต้องตอบต่อเนื่องได้
5. เทียบกับถอด memory ออก — เห็นความต่างทันที

## ลงมือทำ

เปิด [exercises/18-chat-agent-memory/LAB.md](../../exercises/18-chat-agent-memory/LAB.md) — import `solution/01 - Basic Chat Agent & Memory.json` คุยจริงหลายรอบ แล้วทดลองปรับค่า window

## Check understanding

1. ทำไม LLM ลืมบทสนทนาเอง และ memory ช่วยอย่างไร
2. Session key มีผลอย่างไรเมื่อมีผู้ใช้หลายคนพร้อมกัน
3. Window buffer กับ Database memory ควรใช้ตัวไหนตอนไหน

## Next

→ [exercises/18-chat-agent-memory](../../exercises/18-chat-agent-memory/README.md) — คุยกับ agent ที่จำได้จริง
