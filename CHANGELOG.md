# Changelog

## Unreleased

- **หน่วยใหม่ 27 — Build with MCP: สั่งสร้าง Workflow ด้วย Prompt** (`lessons/27-build-with-mcp/` + `exercises/27-build-with-mcp/`): เปิด Instance-level MCP (Settings > Instance-level MCP > Enable MCP access) เชื่อม client (Cursor/Claude ผ่าน OAuth หรือ API key) แล้วสั่งสร้าง workflow ด้วย prompt ตามวงจร describe → validate & fix → review → publish (อนุมัติเอง) → execute; **ออกแบบบนหลักผู้เรียน 1 คน 1 instance** (URL/token ของใครของมัน ห้ามปะปน) พร้อมคลัง prompt ทดลองแล้วใน `starter/prompt-worksheet.md` และ workflow เป้าหมาย 1 ไฟล์ใน `solution/`
- **Deck v7 ขยายเป็น 270 หน้า** (หน่วย 27 อยู่หน้า 264–269): อัปเดต TOC ทั้งสองหน้า, slides README, การอ้างอิงช่วงหน้าใน COURSE.md และ root README
- **แก้ trigger ของ `05B-Sub-*` ทั้ง 4 ไฟล์** สำหรับ n8n 2.48.5: เติม `workflowInputs.values` ให้ Execute Workflow Trigger — รูปแบบเก่า (`event: onReceived` แล้วจบ) import ได้แต่ runtime บล็อกทันที ("At least 1 field is required") ชื่อ field ตั้งให้ตรงกับ `workflowInputs.mapping` ที่ 05B ส่งผ่าน toolWorkflow ทุกตัว (orderId/reason, orderId/purchaseDate/reason, amount/policyPassed, draftEmail/finalAmount) และพิสูจน์ด้วย execution จริงบน instance แล้วว่าเรียกผ่าน Execute Sub-workflow ได้
- **หน่วยใหม่ 26 — n8n Agents: Agent Builder** (`lessons/26-agents/` + `exercises/26-agents/`): บทเรียน n8n Agents (resource ลำดับแรกใน project, Agent Builder, channels/schedules, draft→publish→versions, node Message an Agent, เงื่อนไข self-hosted ≥ 2.32.3) + LAB สร้างผู้ช่วยออฟฟิศครบวงจร (โมเดล, workflow tool + Gmail tool พร้อม require approval, Telegram channel, schedule, publish แล้วเรียกจาก workflow) พร้อม workflow สำเร็จรูป 2 ไฟล์และ worksheet ใน starter
- **อัปเกรด Docker stack เป็น n8n 2.48.5** (`docker-compose.yml` เดิม 2.28.6): ฟีเจอร์ n8n Agents ต้องใช้ n8n ≥ 2.32.3 และภาพหน้าจอใน deck ก็มาจาก 2.48.5 แล้ว; workflow JSON เดิมทั้ง 22 ไฟล์ยังใช้ได้ (node version เป็น minimum)
- **Deck v7 เพิ่มช่วงหน่วย 26** — ขยายจาก 258 เป็น 264 หน้า (divider + สไลด์เนื้อหาหน้า 258–263, แก้สารบัญหน้า 3 และเลขหน้าปิดเล่ม); อัปเดตการอ้างอิงเลขหน้าใน COURSE.md, root README และ `other/slides/README.md`
- **Deck v7** (`other/slides/N8N-L1-Onto-IQ-v7.pptx`): จัดลำดับการเล่าใหม่ให้ตรงโครง repo (ย้ายบล็อก JSON หลังหน่วย 02), แทนภาพหน้าจอเก่าด้วยภาพจริงปี 2026-11 (n8n 2.48.5 จาก n8n.ontoiq.tech, Google Cloud/Google Auth Platform, Pinecone, Cloudflare Tunnel, OpenRouter), แก้สารบัญให้ตรงหน้าใหม่; v6 เก็บไว้เป็นฐานอ้างอิง
- **เขียน README บทเรียนใหม่ทั้ง 25 หน่วย** — `lessons/NN-slug/README.md` มีเนื้อหาบทเรียนเต็ม (จาก LESSON.md ขยาย) พร้อมขั้นตอนลงมือทำและช่วง slide ตาม v7; **ยุบ LESSON.md เข้า README.md แล้วลบทิ้ง** — แต่ละบทเป็นหนังสืออ่านจบในไฟล์เดียว (Demo / walkthrough + Key takeaways ย้ายเข้า README, Check understanding รวมกัน, เติมลิงก์บทถัดไป), ปรับ check_structure.sh, CONTRIBUTING.md, AGENTS.md และลิงก์ใน exercise README ให้สอดคล้อง
- ปรับโครงสร้าง repo ตาม [course-template](https://github.com/phakkhaphong/course-template): `lessons/` + `exercises/` แยกคู่กัน 25 หน่วย, เอกสารประกอบรวมใต้ `other/`, เพิ่ม `COURSE.md` / `SETUP.md` / `CONTRIBUTING.md` และ structure check (bash + CI)
- ย้าย workflow ทั้ง 22 ไฟล์เดิมจาก `workflows/` ไปเป็น `solution/` ของหน่วยที่เกี่ยวข้อง; case studies ไป `other/datasets/`; คู่มือ credentials ไป `other/docs/credentials/`
- Slide deck เวอร์ชัน Onto-IQ (`other/slides/N8N-L1-Onto-IQ-v6.pptx`, 258 หน้า): ลบหน้าโฆษณาหัว/ท้าย ลบ footer ลิขสิทธิ์และโลโก้เดิมออกจากทุกหน้า/master/layout ปรับแบรนด์เป็น Onto-IQ และตัด media ที่ไม่ใช้แล้ว (101.8 MB → 29.9 MB)
- เพิ่มเนื้อหาใหม่จาก n8n brand refresh 2026 และ n8n 2.x (Publish vs Save, secure task runners, Wait 2.0, MCP, evaluation nodes) — สรุปใน `other/reference/n8n-2026-rebrand-and-2x.md`

## 2026-11 (ก่อนปรับโครงสร้าง)

- อัปเกรด workflow และ docker stack สำหรับ n8n 2.28.6 + สคริปต์ migrate node schemas
- เพิ่มคู่มือ HTTPS (Cloudflare Tunnel) สำหรับ webhook และ chat
