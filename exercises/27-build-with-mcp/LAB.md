# Exercise 27 — Build with MCP: สั่งสร้าง Workflow ด้วย Prompt

## Goal
- เชื่อม MCP client เข้ากับ instance ส่วนตัวของคุณ แล้วสร้าง workflow "Daily RSS Digest" ครบวงจรด้วย prompt: สร้าง → validate/แก้ → publish → รันจริงจนได้อีเมล

## Setup
1. เข้า instance ของคุณเอง (URL จากหน่วย 25) ด้วยบัญชี owner — ยืนยันว่าไม่ได้ใช้ instance คนอื่น (ดูชื่อ workflow ใน Overview ต้องเป็นของคุณ)
2. ไปที่ **Settings > Instance-level MCP** → กด **Enable MCP access**
3. กด **Connect** ใน **Connection details** → เลือกวิธี: **OAuth** (แนะนำ เลือก client จากกลุ่ม CLI/Web/IDE แล้วอนุมัติกลับมาที่ n8n) หรือแท็บ **API key** (copy **Configuration JSON** ไปวางใน client)
4. ตั้งค่าฝั่ง client: Cursor → Settings → **Tools & MCP** เพิ่ม server ด้วย config ที่ copy มา; Claude Code → รัน `/mcp` แล้วเพิ่มด้วย URL เดียวกัน
5. ทดสอบการเชื่อมด้วย prompt: `list my workflows` — ต้องเห็นรายชื่อ workflow **ของ instance คุณเอง** เท่านั้น
6. เปิด worksheet `starter/prompt-worksheet.md` กรอกโครง prompt ของคุณก่อนพิมพ์จริง (ชื่อ workflow, trigger, nodes, credential, email ผู้รับ)
7. **Prompt รอบ 1 — สร้าง:** สั่งตามโครงใน worksheet โดยปิดท้ายทุกครั้งด้วย "ยังไม่ต้อง publish — validate ให้เรียบร้อยก่อนแล้วรายงานผล"
8. **Prompt รอบ 2 — แก้:** ถ้ามี error/warning สั่ง "แก้ error และ warning ทั้งหมด แล้ว validate ซ้ำจนผ่าน ยังไม่ต้อง publish"
9. เปิด workflow ใน editor ของ n8n ตรวจตาเอง: 4 node ครบ (Schedule → RSS → Code → Gmail), credential Gmail ถูกตัว, อีเมลผู้รับเป็นของคุณ
10. **Prompt รอบ 3 — publish:** อนุมัติด้วยตัวเองแล้วค่อยสั่ง `publish workflow "Daily RSS Digest" ตั้งชื่อเวอร์ชันว่า "first build via MCP"`
11. สั่งรันทดสอบ `execute workflow "Daily RSS Digest" ด้วยโหมด manual` — หรือรอ schedule 09:00 ของพรุ่งนี้
12. เช็คกล่องเมลของคุณ: ต้องได้อีเมลหัวข้อ "📰 Daily Digest" จาก Hacker News
13. ปิดท้าย: เปิด workflow ดู **publish history** และลองสั่ง `unpublish` แล้ว `publish` กลับ เพื่อเห็นวงจรควบคุมเวอร์ชันผ่าน prompt

## Check your work
- การเชื่อมเห็นเฉพาะ workflow ของ instance คุณ (ถ้าเพื่อน list workflows แล้วเห็นของคุณ = config ปนกัน ให้หยุดแก้ทันที)
- workflow "Daily RSS Digest" ถูกสร้างบน instance คุณด้วย prompt โดยคุณไม่ได้ลาก node เองแม้แต่ node เดียว
- validate ผ่านหมดก่อน publish และ publish history มีเวอร์ชันชื่อ "first build via MCP"
- execution สำเร็จและได้อีเมลจริง 1 ฉบับ

## Stretch (optional)
- สั่งเพิ่ม node สรุปข่าวด้วย AI (LLM Chain + credential จากหน่วย 14/15) แล้ว publish เวอร์ชันใหม่ — ดู publish history ว่าต่างกันอย่างไร
- สร้าง **n8n Agent** (จากหน่วย 26) ด้วย prompt ผ่าน MCP ตัวเดียวกัน: โมเดล + instructions + workflow tool ชี้ไปที่ Daily RSS Digest
- ติดตั้ง n8n Skills (repo `n8n-io/skills`) ให้ coding agent ของคุณ แล้วเทียบคุณภาพ workflow ที่ได้ก่อน–หลัง
