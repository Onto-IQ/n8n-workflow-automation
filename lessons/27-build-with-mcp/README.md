# 27 — สร้าง Workflow ด้วย MCP + Prompt / Build with MCP

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/27-build-with-mcp](../../exercises/27-build-with-mcp/README.md) |
| เวลาโดยประมาณ | ~60 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 264–269 |
| เฉลย | `exercises/27-.../solution/01 - Daily RSS Digest.json` (ผลลัพธ์ปลายทางที่ prompt ต้องสร้างได้) |

หน่วย 21 เราใช้ MCP "ภายใน workflow" (n8n เป็นลูกค้าที่ไปเรียก server อื่น) หน่วยนี้กลับด้าน: เปิด **Instance-level MCP** ให้ **AI client ของคุณ** (Cursor, Claude Code/Desktop) ต่อเข้ามาสั่ง n8n ของคุณโดยตรง — ค้น node, เขียน workflow, validate, สร้าง, publish และรัน ทั้งหมดผ่าน **prompt** บน **instance ส่วนตัวของผู้เรียนแต่ละคน** (ไม่ปะปนกัน)

## Instance-level MCP — ต่างจาก MCP ใน workflow

- หน่วย 21: node **MCP Client** ใน workflow เรียก tool จาก server ภายนอก — n8n เป็นผู้ "ใช้"
- หน่วยนี้: MCP server ของตัว instance เอง เปิดให้ client ภายนอก (IDE/chat/CLI) มา **จัดการ instance** — สร้าง/แก้/publish workflow, สั่ง execute, ดู validation — n8n เป็นผู้ "ถูกสั่ง"
- ทั้งสองแบบใช้มาตรฐานเดียวกัน (MCP) แต่คนละทิศ อย่าสับสน — ตัว MCP นี้ยังสร้าง/จัดการ **Agents** จากหน่วย 26 ได้ด้วย

## เตรียม Instance ของคุณ (เจ้าของ instance เท่านั้น)

ผู้เรียนแต่ละคนทำบน instance ตัวเองจากหน่วย 25 — ต้องเป็น **owner/admin** จึงเปิดได้:

1. **Settings > Instance-level MCP** → กด **Enable MCP access**
2. หน้าจอมี 3 ส่วน: **Connection details**, **Access**, **Connected clients**
3. **Server URL** อยู่ใน **Connect a client** — ลงท้ายด้วย `/mcp-server/http` (URL นี้เป็นของ instance คุณเท่านั้น ผู้เรียนแต่ละคน URL ไม่ซ้ำกัน)
4. ปิดเมื่อไหร่ก็ได้ด้วย **MCP status → Disable** (จะตัดทุก client ที่เชื่อมอยู่)

## เชื่อม Client: OAuth หรือ API key

ใน **Connection details → Connect** เปิด dialog **Connect a client** เลือกได้ 2 ทาง:

- **OAuth (แนะนำ)** — เลือก client จาก dropdown (จัดกลุ่ม **CLI / Web / IDE** เช่น Claude Code, Cursor, VS Code, Windsurf) ทำ one-click setup หรือรันคำสั่งที่หน้าจอให้ แล้วกลับมากดอนุมัติใน n8n — client ที่เชื่อมจะโผล่ใน **Connected clients** ให้ยกเลิกได้ทีหลัง
- **API key** — แท็บ **API key** สร้าง token ให้อัตโนมัติ (ผูกกับ user account ของคุณ) copy **Configuration JSON** ที่ใส่ URL + `Authorization: Bearer` มาให้พร้อม ออกจากแท็บแล้ว token ถูกซ่อน — หาย/รั่วให้กด generate ใหม่ (ตัวเก่าถูก revoke ทันที)

**ใส่ config ที่ client ของคุณ** — Cursor: Settings → **Tools & MCP** → เพิ่ม server; Claude Code: รัน `/mcp` แล้วเพิ่มด้วย URL เดียวกัน ทดสอบด้วย prompt แรก: `"list my workflows"` — ต้องเห็น workflow ใน instance ตัวเองเท่านั้น

## เปิดให้ MCP มองเห็น workflow

- ค่าเริ่มต้น client **แตะ workflow ไม่ได้** จนกว่าจะเปิด per-workflow: toggle **Available in MCP** ในหน้า editor หรือ **Workflows enabled** / **Manage MCP access** แบบกลุ่ม
- ยกเว้น `search_workflows` — ลิสต์/พรีวิวได้ทุก workflow ที่ account คุณมองเห็น
- อยากให้ workflow ใหม่ที่สร้างผ่าน MCP ใช้ต่อได้เลย เปิด **Auto-expose new workflows** (2.36+)

## วงจรสั่งงาน: Prompt → Search → Validate → Create → Publish

วินัย 5 รอบที่ใช้ได้กับงานจริง (และใช้ใน LAB ของหน่วยนี้):

1. **Describe** — บอกชื่อ workflow, trigger, node ที่เกี่ยว, credential ที่มี และสั่งชัดว่า "ยังไม่ต้อง publish"
2. **Validate & fix** — สั่งให้ AI validate กับ instance จริงแล้วแก้ error/warning ให้หมดก่อน
3. **Review** — เปิด workflow ใน editor ตรวจตาเอง: node ครบ, credential ถูกตัว, ข้อความ/ที่อยู่ผู้รับถูกต้อง
4. **Publish (ต้องอนุมัติเสมอ)** — publish = ขึ้นใช้งานจริง ห้ามให้ AI ตัดสินใจแทน
5. **Execute** — รันทดสอบ (หรือรอ schedule) แล้วดู execution; จำว่า workflow จริงมี **side effect** (ส่งเมลจริง โพสต์จริง)

กติกาความปลอดภัย: API key/token ของ instance คุณคือ **secret ส่วนตัว** ห้ามแชร์ให้เพื่อน copy config ติดตั้งเฉพาะเครื่องตัวเอง credentials ทั้งหมดอยู่ใน credential store ของ n8n เสมอ — AI ไม่จำเป็นต้องเห็น key

## เขียน Prompt ให้เวิร์ก

โครง prompt ที่ดี (ภาษาไทยก็ได้ เครื่องมือเข้าใจ):

```text
สร้าง workflow ชื่อ "Daily RSS Digest" บน instance ของฉัน:
Schedule Trigger ทุกวัน 09:00 → RSS Read (https://hnrss.org/frontpage)
→ Gmail ส่งสรุปไปที่ YOUR_EMAIL หัวข้อ "📰 Daily Digest"
ใช้ credential Gmail ที่มีอยู่ ตั้งชื่อ node ให้สื่อความหมาย
ยังไม่ต้อง publish — validate ให้เรียบร้อยก่อนแล้วรายงานผล
```

- บอก **ชื่อ workflow + ทุก node + trigger + credential** ที่ควรใช้ ยิ่งเจาะจงยิ่งได้ workflow ตรงใจ
- แยกสั่งทีละรอบ: สร้าง → แก้ → publish อย่ารวมทุกอย่างใน prompt เดียว
- ติดขัดตรงไหนให้ AI "search node" ที่เกี่ยวก่อน (เช่น "หา node สำหรับอ่าน RSS และบอก version ที่รองรับ") แล้วค่อยสั่งสร้าง — ลดการเดา schema
- ชุด prompt ทดลองแล้วอยู่ใน [starter/prompt-worksheet.md](../../exercises/27-build-with-mcp/starter/prompt-worksheet.md)

## Key takeaways

- Instance-level MCP เปลี่ยน n8n จาก "เครื่องมือที่คุณคลิก" เป็น "ระบบที่คุณสั่งด้วย prompt" — แต่ owner ยังต้องตรวจและกดอนุมัติ publish เอง
- Instance ส่วนตัว = สนามฝึกปลอดภัย: URL และ token ของใครของมัน workflow ไม่ปะปน ลองผิดลองถูกได้เต็มที่

## ลงมือทำ

เปิด [exercises/27-build-with-mcp/LAB.md](../../exercises/27-build-with-mcp/LAB.md) — เปิด MCP access บน instance ตัวเอง เชื่อม client แล้วสั่งสร้าง Daily RSS Digest ด้วย prompt 3 รอบ (สร้าง → validate/แก้ → publish) และรันจริงจนได้อีเมล

## Check understanding

1. Instance-level MCP ต่างจาก MCP Client node ใน workflow (หน่วย 21) อย่างไร — ใครเป็นผู้สั่งในแต่ละแบบ
2. ทำไม workflow ที่สร้างแล้ว client ยัง "สั่งไม่ได้" จนกว่าจะเปิด **Available in MCP** — และ toggle ไหนช่วยให้ข้ามขั้นนี้กับ workflow ใหม่
3. เมื่อไรควรเลือก OAuth แทน API key ในการเชื่อม client — ข้อดีของ OAuth ใน **Connected clients** คืออะไร
4. ทำไมขั้น "Publish" ต้องมาจากการอนุมัติของคุณเสมอ แม้ AI เขียน workflow เสร็จและ validate ผ่านหมดแล้ว

## Next

→ [exercises/27-build-with-mcp](../../exercises/27-build-with-mcp/README.md) — เปิด MCP access บน instance ของคุณ แล้วสร้าง workflow แรกด้วย prompt ล้วน ปิดคอร์สด้วยทักษะที่ใช้ต่อได้จริงทุกวัน
