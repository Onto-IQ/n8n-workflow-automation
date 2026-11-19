# Lesson 21 — MCP Client & Server

เนื้อหาสอนประกอบ slide (slides 193–202 (หน้าจอ 186–195)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- MCP = มาตรฐานเปิดของ Anthropic เชื่อม AI ↔ ข้อมูล/เครื่องมือ: [AI Agent] ↔ [MCP Client] ↔ [MCP Server] ↔ [Tools] — เขียน tool ครั้งเดียว ใช้ได้ทุก AI (Claude, Cursor, n8n)
- Client = "ไปใช้ tools คนอื่น" (เหมือนเรียก Grab แทนซื้อรถ): Agent + MCP Client tool ชี้ endpoint server แล้ว discovery tools เอง
- Server = "ให้คนอื่นใช้ tools เรา" (โรงงานผลิตเครื่องมือ): MCP Server Trigger + Calculator/Gmail/Calendar แล้ว AI ภายนอกเรียกผ่าน URL/path เช่น mcp-server-demo (tools ถูกเรียกผ่าน $fromAI())
- Function Calling vs MCP: ฟีเจอร์เฉพาะ model + bind เอง + vendor lock-in  เทียบกับ มาตรฐานเปิด + single endpoint + discovery เอง

## Demo / walkthrough
1. Import workflow ทั้งสองจาก solution/ → Activate server → สั่งผ่าน client

## Key takeaways
- server workflow ต้อง Active จึงรับการเชื่อมต่อได้

## Check understanding
- อธิบายความต่าง client/server ด้วยคำเดียว
