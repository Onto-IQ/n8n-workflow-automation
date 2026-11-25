# 24 — Big Bonus: สร้าง Flow ด้วย Agentic IDE / Bonus: agentic IDE

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/24-agentic-ide-bonus](../../exercises/24-agentic-ide-bonus/README.md) |
| เวลาโดยประมาณ | ~60 นาที (challenge 45–60 นาที) |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 220–222 |

Big Bonus ของคอร์ส: **สร้าง/จัดการ n8n workflow ด้วย Agentic IDE** — ให้ AI coding assistant (Claude Code, Cursor, VS Code + Copilot, Windsurf, Antigravity) ต่อเข้ากับ n8n instance ของเราผ่าน MCP แล้วสั่งงานด้วยภาษาคน นี่คือวิธีสร้าง flow ยุคใหม่ 2026

## เครื่องมือ Agentic IDE ที่นิยม

- **Cursor**, **VS Code + Cline extension**, **Windsurf**, **Antigravity**
- ใช้ n8n skill/เครื่องมือเสริม เช่น [github.com/czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills) และ [github.com/czlonkowski/n8n-mcp](https://github.com/czlonkowski/n8n-mcp)
- ต้องมี n8n API key ของ instance ตัวเอง (Settings → n8n API หรือ Instance-level MCP)

## ต่อ Claude Code เข้า n8n ผ่าน MCP

n8n มีปุ่มพร้อมขั้นตอนในตัว: **Settings → Instance-level MCP → Connect → เลือก Claude Code** แล้วทำตาม (สองวิธี):

1. **คำสั่ง** — รัน `claude mcp add --transport http n8n https://<instance>/mcp-server/http`
2. **Config มือ** — เพิ่มในไฟล์ config: `{ "mcpServers": { "n8n": { "type": "http", "url": "https://<instance>/mcp-server/http" } } }`
3. **Authenticate** — รัน `/mcp` ใน Claude Code แล้วเลือก n8n เพื่อ grant access (หรือใช้วิธี API key ตามแท็บ API key ใน dialog เดียวกัน)

หลังต่อสำเร็จ ใน Claude Code สั่งได้เลย เช่น "list my workflows", "สร้าง workflow ตามที่เราคุยกัน" — agent จะเรียก MCP tools ของ n8n (search/execute/create workflow) แทนเรา

## Challenge: สร้าง n8n workflow ด้วย Agentic IDE

**งาน: เลือกหนึ่ง workflow จากที่เรียนมาแล้ว สร้างมันใหม่ผ่าน Agentic IDE** — เริ่มจาก describe ที่ต้องการเป็นภาษาคน ให้ AI วาง node ต่อ connection ตั้ง credential ผ่านชื่อ แล้วรันทดสอบ จากนั้นประเมิน: AI วางผิดตรงไหน, แก้ด้วยคำสั่งไหน, และเทียบเวลากับการสร้างด้วยมือ

## ลงมือทำ

เปิด [exercises/24-agentic-ide-bonus/LAB.md](../../exercises/24-agentic-ide-bonus/LAB.md) — ต่อ MCP ให้เครื่องมือที่ตัวเองใช้ แล้วทำ challenge ตามเวลา 45–60 นาที และจด lesson learned

## Check understanding

1. MCP ในบริบทนี้ช่วยให้ Agentic IDE ทำอะไรได้บ้างกับ n8n
2. ขั้น authenticate (OAuth หรือ API key) ทำเมื่อไหร่ และเก็บ key อย่างไรให้ปลอดภัย
3. งานแบบไหนให้ AI สร้างแทนได้ดี งานไหนควรคุมเอง

## Next

→ [exercises/24-agentic-ide-bonus](../../exercises/24-agentic-ide-bonus/README.md) — challenge สร้าง flow ด้วย AI
