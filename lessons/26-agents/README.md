# 26 — n8n Agents: Agent Builder / Agents

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/26-agents](../../exercises/26-agents/README.md) |
| เวลาโดยประมาณ | ~75 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 258–263 |
| เฉลย | `exercises/26-.../solution/01 - Message an Office Assistant.json`, `02 - Agent Tool - Company FAQ.json` (ตัว Agent เองสร้างบน UI — ไม่มีไฟล์ JSON) |

จากหน่วย 17–23 เราสร้าง agent ด้วย **AI Agent node** ภายใน workflow — workflow เป็นเจ้าของทุกอย่าง หน่วยนี้พาไปรู้จัก **n8n Agents** ฟีเจอร์ใหม่ยุค 2.x: agent เป็น **resource ลำดับแรก** ใน project (อยู่แท็บ **Agents** ข้าง workflow) มี instructions, โมเดล, tools, memory และ lifecycle ของตัวเอง สร้างครั้งเดียว ใช้ซ้ำได้ทุกที่ — คุยตรงในตัว builder, ต่อเข้าแชท (Telegram/Slack), ตารางเวลา หรือเรียกจาก workflow ด้วย node **Message an Agent**

## Agents คืออะไร — ต่างจาก AI Agent node

- **AI Agent node** (หน่วย 18–23): เป็น node ใน workflow — trigger, กราฟรอบข้าง และ lifecycle ทั้งหมดเป็นของ workflow
- **n8n Agent**: เป็น artifact อิสระใน project — config (โมเดล/instructions/tools/memory) กับ lifecycle (draft/publish/version) เป็นของตัวเอง ทุกบทสนทนาถูกเก็บเป็น **session**
- ปิดฟีเจอร์ Agents ที่ Settings ไม่กระทบ AI Agent node — เป็นสองระบบแยกกัน
- ใช้ Agent เมื่องาน **เปิด (open-ended)** เกิน fixed workflow: agent วิ่ง reasoning loop เลือกเรียก tools, ค้นข้อมูล, ส่งต่อ หรือถามกลับเอง จนได้คำตอบ — ถ้าขั้นตอนตายตัวทำซ้ำได้ ให้ใช้ workflow ตามหลัก **"Agent-first, Workflow second"**

## Agent Builder: Model • Instructions • Tools • Skills

สร้าง: เลือก project → แท็บ **Agents** → **Create Agent** (เปิด Agent Builder ด้วย draft เปล่า) ตั้งชื่อ + ไอคอน หรือให้ **n8n Assistant** ร่าง config จากคำบรรยายก็ได้

- **Model** — เลือก provider/โมเดล ผูก credential (โมเดลที่รองรับ tool calling เช่นจาก OpenAI-compatible endpoint)
- **Instructions** — system prompt: บทบาท น้ำเสียง ข้อจำกัด กฎการเรียก tool; ปรับให้นิ่งก่อนแล้วค่อยเพิ่ม tools
- **Tools** — 4 แหล่ง: ① integration สำเร็จรูป (Gmail, Google Sheets ฯลฯ) ② **workflow ใน project** ที่ขึ้นต้นด้วย trigger **When Executed by Another Workflow** (หน่วย 23) ③ custom tool จาก JSON Schema ④ **MCP server ภายนอก** (ต่อยอดหน่วย 21); tool ที่ไวใช้จัดการข้อมูลตั้ง **ต้องอนุมัติก่อน** (Approve/Reject ในแชท) ได้
- **Skills** — ชุด instruction + ไฟล์อ้างอิง ใช้ซ้ำข้าม agent ได้; agent เลือกใช้จากคำอธิบายของ skill
- **Memory** — session memory เปิดอัตโนมัติ; **Episodic memory** (จำจากบทสนทนาเก่า) ต้องมี OpenAI credential
- **Sub-agents** — ผูก agent ที่ publish แล้วไว้เป็นผู้เชี่ยวชาญเฉพาะทาง พร้อมเขียน "เมื่อไรควรใช้ตัวนี้"

## Channels และ Schedules

- **Channels** — ต่อ agent เข้า **Telegram, Slack, Linear, Microsoft Teams** ได้ (ตั้ง credential ของ channel) — ผู้ใช้คุยกับ agent ผ่านแอปที่คุ้นอยู่แล้ว โดยไม่เขียน webhook เอง (channel บน self-hosted ต้องมี `WEBHOOK_URL` สาธารณะ — Cloudflare Tunnel จากหน่วย 25 คือคำตอบ)
- **Schedules** — ตารางรัน (hourly/daily/weekly/monthly/หรือ cron เอง) เหมือน Schedule Trigger แต่ติดกับตัว agent; schedule รันกับ **เวอร์ชันที่ publish เท่านั้น**

## Draft → Publish → Versions

- ทุก agent มี **draft** (autosave) กับ **published version** — กด **Publish** = ถ่าย snapshot ของ draft
- **Preview** ใน builder ทดสอบ draft ได้ทันที (ถ้า config มี error ปุ่มจะถูกปิดพร้อมบอกรายการที่ต้องแก้)
- **Publish history** เก็บทุกเวอร์ชัน — restore กลับได้เสมอ; **Unpublish** ถอนออกจากใช้งานจริงแต่ draft ยังอยู่
- แท็บ **Sessions** โชว์ทุกบทสนทนา: ข้อความ, tool ที่ถูกเรียก, รายการรออนุมัติ — จุด debug แรกของ agent
- **ต้นทุน**: 1 turn (1 ครั้งที่ agent ตอบ) = 1 execution ใช้โควตาร่วม workflow — การเรียก workflow tool/sub-agent ภายใน turn เดียวไม่นับซ้ำ

## เรียก Agent จาก Workflow: Message an Agent

- node **Message an Agent** ยิงข้อความเข้า agent ที่ publish แล้วจากใน workflow — เลือก agent ที่มีอยู่ (referenced) หรือนิยาม inline; แต่ละข้อความ = 1 execution
- ผลลัพธ์ออกเป็น `text` พร้อม `toolCalls` (tool ที่ถูกเรียก) และ `session`; เปิด **structured output** บังคับตอบตาม JSON Schema ได้ (อ่านต่อที่ `structuredOutput`)
- จุดค้น 2 ทิศ: workflow กลายเป็น **tool** ของ agent ได้ และ agent ถูกเรียกจาก workflow ได้ — ทำ multi-agent ข้ามทั้งสองโลกได้ (มี **Message an Agent Tool** สำหรับต่อจาก AI Agent node โดยตรง)

## เงื่อนไขบน Self-Hosted

- ต้องใช้ **n8n ≥ 2.32.3** (แนะนำ 2.34+; สแตกของ repo pin **2.48.5** แล้ว) — เวอร์ชันเก่าจะไม่เห็นแท็บ Agents
- ต้องรันโหมด **regular** — ฟีเจอร์นี้ยังไม่รองรับ queue mode; เปิด/ปิดได้ที่ **Settings > Agents > Enable Agents**
- สถานะฟีเจอร์คือ **Preview** — UI/พฤติกรรมอาจเปลี่ยนตามรุ่น; Knowledge base บน self-hosted เป็น Preview แยกอีกชั้น
- ทางไกล: agent สร้าง/จัดการจาก **MCP client ภายนอก** ได้ด้วย instance-level MCP — หัวข้อยาก ไว้ต่อยอดนอกคอร์ส

## Demo / walkthrough: สร้าง "ผู้ช่วยออฟฟิศ" บน Agent Builder

1. **Create Agent** ตั้งชื่อ + ไอคอน → เลือกโมเดล (credential OpenAI-compatible) → เขียน instructions ภาษาไทย (บทบาท: ผู้ช่วยตอบคำถามภายในองค์กร อ้าง FAQ ก่อนเสมอ)
2. ทดสอบใน **Preview** — ถามคำถามทดลอง 1 ข้อ ดูว่าน้ำเสียง/ขอบเขตถูกใจหรือยัง
3. เพิ่ม **workflow tool** (FAQ lookup จากไฟล์ `solution/02`) และ **Gmail tool** (ดึงเมลล่าสุด) โดยเปิด require approval ที่ Gmail tool
4. ต่อ **Telegram channel** + ตั้ง **schedule** digest รายวัน → **Publish** → ดู publish history
5. สร้าง workflow เล็ก ใช้ **Message an Agent** เรียก agent ตัวนี้ แล้วอ่าน `text`/`toolCalls` ใน output
6. เปิดแท็บ **Sessions** ย้อนดูว่า agent เรียก tool อะไร ตอบอะไร และมีรายการรออนุมัติหรือไม่

## Key takeaways

- Agent = resource อิสระใน project (สร้างครั้งเดียว ใช้ได้ทุก channel/workflow) ส่วน AI Agent node = node ใน workflow — เลือกตามความเปิดของงาน
- วงจรจริงคือ Draft → Preview → Publish (snapshot) → Versions; debug ที่แท็บ Sessions และต้นทุนนับเป็น turn

## ลงมือทำ

เปิด [exercises/26-agents/LAB.md](../../exercises/26-agents/LAB.md) — สร้าง Agent ผู้ช่วยออฟฟิศครบวงจร: โมเดล + instructions, workflow tool และ Gmail tool (พร้อม require approval), ต่อ Telegram, ตั้ง schedule, publish แล้วเรียกจาก workflow ด้วย Message an Agent

## Check understanding

1. เคสแบบไหนควรใช้ n8n Agent — เคสแบบไหนยังควรเป็น workflow กับ AI Agent node เดิม
2. workflow ต้องมีอะไรขึ้นต้นก่อน จึงจะแปะเป็น workflow tool ของ agent ได้ และต้องอยู่สถานะใดจึงถูกเรียกได้จริง
3. Publish ทำอะไรกับ draft — ถ้าเวอร์ชันใหม่พัง จะกลับไปเวอร์ชันเก่าทางไหน
4. "1 turn = 1 execution" หมายความว่าอย่างไร และจะดูว่า agent เรียก tool อะไรไปบ้างในแต่ละ turn ที่ใด

## Next

→ [exercises/26-agents](../../exercises/26-agents/README.md) — สร้างและ publish ผู้ช่วยออฟฟิศตัวแรกของคุณ
→ บทถัดไป: [27 — Build with MCP: สั่งสร้าง Workflow ด้วย Prompt](../27-build-with-mcp/README.md)
