# 21 — MCP Client & Server / MCP client & server

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/21-mcp-client-server](../../exercises/21-mcp-client-server/README.md) |
| เวลาโดยประมาณ | ~60 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 186–195 |
| เฉลย | `exercises/21-.../solution/04 - MCP Server.json`, `04 - MCP Client.json` |

**MCP (Model Context Protocol)** คือมาตรฐานเปิด (open standard) จาก Anthropic ที่ทำให้ AI agent สื่อสารกับเครื่องมือ/แหล่งข้อมูลภายนอกได้แบบสองทาง — เปรียบเป็น "ปลั๊กไฟมาตรฐาน" ของโลก AI: ต่อครั้งเดียว ใช้ได้ทุกไคลเอนต์ที่รองรับ (Claude, Cursor, n8n ฯลฯ) บทนี้สอนทั้งสองฝั่ง: เปิด **MCP Server** (ให้ AI อื่นใช้ tools ของเรา) และเรียก **MCP Client** (ใช้ tools จากภายนอก)

## มาตรฐานใหม่ของการเชื่อมต่อ AI

- **Universal Interface** — เขียน tool ครั้งเดียว AI หลายตัวใช้ร่วมได้
- **Scalability** — เพิ่มเครื่องมือได้แบบ plug-and-play ไม่ต้องแก้ agent ทุกตัว
- **Flow**: `[AI Agent] ↔ [MCP Client] ↔ [MCP Server] ↔ [Tools/Services]` — client อยู่ใน n8n, server เป็น workflow ของเราที่เปิด endpoint ให้เรียก

## ฝั่ง MCP Server (ผู้ให้บริการ — "โรงงานผลิตเครื่องมือ")

ตัวอย่างคอร์ส: workflow **04 - MCP Server** มี

1. **MCP Server Trigger** — รับ request จาก AI ภายนอก (สร้าง Webhook URL + path เช่น `mcp-server-demo`)
2. **เครื่องมือจริง**: Gmail, Calendar, Code node (Calculator)
3. **ตั้งค่าสำคัญ** — เปิดช่อง MCP ใน node (Available in MCP), publish workflow แล้วคัดลอก **MCP Server URL** ที่ระบบให้
4. AI ภายนอก (Claude/Cursor) จะเห็นเครื่องมือของเราและเรียกใช้ได้ (tool ที่ถูกเรียกจะอ้างค่าผ่าน `$fromAI()`)

## ฝั่ง MCP Client (ผู้เรียกใช้ — "เรียก Grab แทนซื้อรถ")

ตัวอย่างคอร์ส: workflow **04 - MCP Client** มี

1. Chat Trigger + AI Agent + OpenAI Chat Model
2. **MCP Client Tool** node — ชี้ endpoint URL ของ MCP Server (คอร์สใช้ endpoint ห้อง เช่น `https://n8n.datafabric.app/mcp/mcp1`)
3. Agent จะ **discovery เลือกเรียก tools จาก server เอง**: คำนวณเลข → Calculator, อ่านอีเมล → Gmail, จองประชุม → Calendar

## Function Calling vs. MCP

| หัวข้อ | Function Calling | MCP |
|---|---|---|
| คอนเซปต์ | ฟีเจอร์เฉพาะ model — โมเดลสั่ง tool ใน code เราเอง | มาตรฐานกลาง open protocol |
| การเชื่อมต่อ | เขียนโค้ด (hard code) bind ต่อทีละเครื่องมือ | single endpoint, client discover tools เอง |
| การขยายระบบ | มือแก้ทุกจุด (และติด vendor lock-in) | เพิ่ม server/tools ใหม่โดยไม่แก้ agent |

## Key takeaways

- server workflow ต้อง **Active/Publish** ก่อนจึงจะรับการเชื่อมต่อจาก client ได้

## ลงมือทำ

เปิด [exercises/21-mcp-client-server/LAB.md](../../exercises/21-mcp-client-server/LAB.md) — สร้าง MCP Server (จับ request ให้เห็น), สร้าง MCP Client (ให้ agent เรียก tool จาก server) และยิงคำสั่งที่ต้องใช้หลายเครื่องมือต่อกัน

## Check understanding

1. MCP แก้ปัญหาอะไรที่ Function Calling แบบเดิมทำได้ยาก
2. MCP Server Trigger ทำหน้าที่อะไร และ AI ภายนอกรู้ได้อย่างไรว่าเรามี tools อะไร
3. Flow จากคำสั่งผู้ใช้จนถึง tool เรียกตัวไหนทำงานบ้าง เรียงตามลำดับ
4. อธิบายความต่าง client กับ server ด้วยคำเดียว

## Next

→ [exercises/21-mcp-client-server](../../exercises/21-mcp-client-server/README.md) — เปิดและเรียกเครื่องมือผ่าน MCP จริง
→ บทถัดไป: [22 — Workshop #3: RAG ด้วย Pinecone](../22-workshop-rag-pinecone/README.md)
