# Exercise 26 — n8n Agents: Agent Builder

คู่กับ [lessons/26-agents](../../lessons/26-agents/) — ชื่อโฟลเดอร์ `NN-slug` ตรงกันเสมอ

| | |
|--|--|
| Hands-on | [LAB.md](LAB.md) |
| Starter | [starter/](starter/) |
| Solution | [solution/](solution/) |

ไฟล์ workflow สำเร็จรูป:
- `solution/01 - Message an Office Assistant.json`
- `solution/02 - Agent Tool - Company FAQ.json`

หมายเหตุ: ตัว Agent เองสร้างและ config บน UI (Agent Builder) — ไม่มีไฟล์ JSON ให้ import; ไฟล์สำเร็จรูปทั้งสองคือ workflow ที่รองรับ agent (FAQ tool กับตัวเรียก Message an Agent)

## Goal / เป้าหมาย
- สร้าง Agent "ผู้ช่วยออฟฟิศ" ด้วย Agent Builder ครบวงจร: โมเดล + instructions, workflow tool + Gmail tool (require approval), Telegram channel, schedule, publish แล้วเรียกจาก workflow ด้วย Message an Agent

## Before you start
- เรียน lesson คู่กันจบก่อน (หรืออ่าน [README.md](../../lessons/26-agents/README.md))
- อย่าเปิด `solution/` จนกว่าจะลองเองก่อน
- instance ต้องเป็น n8n ≥ 2.32.3 (สแตกของ repo คือ 2.48.5) และมี credential: โมเดลที่รองรับ tool calling, Gmail, Telegram
