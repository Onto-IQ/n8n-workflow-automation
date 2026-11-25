# n8n 2026 — Brand Refresh & 2.x Essentials

สิ่งใหม่สำคัญที่หลักสูตรนี้อัปเดตตาม (อิง slide หน้า 12–27) — ใช้ประกอบ unit 01 และอ้างอิงข้ามหน่วย

## Brand refresh (ต.ค. 2026, ประกาศที่งาน In The Loop)

- **โลโก้ใหม่** — ย้ายจุดโฟกัสจาก "โหนดที่ต่อกัน" ไปสู่สิ่งที่เกิดขึ้น *ระหว่าง* การเชื่อมต่อ: activity, agents, ระบบที่ตอบสนองแบบ real time สะท้อนการเดินทางจาก "workflow ที่ต่อของ" สู่ "ระบบที่ตอบสนอง ปรับตัว และลงมือทำ"
- **Typeface ใหม่** — สมดุลระหว่าง technical precision กับความเป็นมนุษย์ฝั่ง builder ("technical without feeling sterile, precise without feeling rigid")
- **สี** — ชมพูเซ็นเนเจอร์เดิมปรับละเอียดขึ้น คู่กับชุดเฉดเทาที่เพิ่ม range ของระบบดีไซน์
- ของที่ไม่เปลี่ยน: community, pink, การเลือกโมเดลเอง, Community Edition นิยามเชิงแบรนด์: "a zhush, not a rebuild" — วิวัฒนาการ ไม่ใช่รื้อใหม่; brand guidelines ที่ guidelines.n8n.design

## Messaging ที่คอร์สยึดเป็นแกน (Agent-first)

1. **"More capable AI should create more capable people"** — AI เก่งขึ้นต้องทำให้คนเก่งขึ้นตาม
2. **"Intelligence made visible"** — มองเห็น → สร้างความเข้าใจ → ควบคุมได้ → รักษาอำนาจกำหนดทิศทาง
3. **"AI makes intelligence possible. n8n makes intelligence operational."** — AI ทำให้ฉลาดเกิดได้ n8n ทำให้ฉลาดทำงานจริง
4. **"Agent-first, Workflow second"** — ให้ AI Agent เป็นด่านแรกที่รับ/จัดการงาน ใช้ workflow deterministic เฉพาะจุดที่ต้องการผลลัพธ์ซ้ำได้

n8n ปัจจุบันวางตัวเป็นแพลตฟอร์มสร้าง **workflows + AI agents** (ไม่ใช่ workflow tool เฉย ๆ) และเติบโตเป็นบริษัท multi-product

## n8n 2.x — สิ่งที่ผู้เรียนต้องรู้

### Core architecture

- **Publish vs Save:** แยก draft ออกจาก published ชัดเจน — แก้/debug ใน draft ได้โดยไม่กระทบ production ที่รันอยู่ (หลัก CI/CD)
- **Secure-by-default Task Runners:** JS/Python ใน Code node รันใน sandbox แยก กัน infinite loop / memory leak ลาก instance หลักล่ม
- **Wait Node 2.0:** sub-workflow ที่ติด Wait (เช่น รอ approve) คืนผลลัพธ์สุดท้ายให้ parent ได้ถูกต้อง (เดิมคืนแค่ input)

### Performance & AI-native

- SQLite pooling driver → เร็วขึ้นราว 10x ลดปัญหา "database locked"; binary data (รูป/PDF) ย้ายไป filesystem-based เพื่อความเสถียร
- **AI Evaluation nodes** — ทดสอบ/ประเมิน AI agent ใน n8n โดยตรง
- **MCP support** — ต่อ MCP servers ให้ AI เข้าถึง data/tools ภายนอก (unit 21)
- Autosave กันงานหาย; **Migration Report** วิเคราะห์ workflow 1.x หา breaking changes ก่อนอัปเกรด (repo นี้ใช้ n8n 2.48.5 แล้ว ดู `other/scripts/migrate_workflows_2_28_6.py`)

### n8n Agents (Agent Builder) — ฟีเจอร์ใหม่ยุค 2.x

- Agent เป็น **resource ลำดับแรก** ใน project (แท็บ **Agents** ข้าง workflow) มี instructions, โมเดล, tools, skills, memory, channels (Telegram/Slack/Linear/Teams) และ schedules ของตัวเอง — แยกจาก AI Agent node ที่ติดอยู่ใน workflow
- วงจร draft → publish (snapshot) → publish history คล้าย Publish vs Save ของ workflow; เรียกจาก workflow ด้วย node **Message an Agent** (1 turn = 1 execution)
- เงื่อนไข self-hosted: n8n ≥ 2.32.3, โหมด regular (ยังไม่รองรับ queue mode), เปิดที่ **Settings > Agents > Enable Agents**, channel ต้องมี `WEBHOOK_URL` สาธารณะ — สถานะ Preview
- สอนครบใน **unit 26** (`lessons/26-agents/`)

## License สั้น ๆ

- **MIT:** core engine + nodes — ใช้/แก้ได้เต็มที่
- **Sustainable Use License:** ฟีเจอร์ enterprise/cloud — source available แต่ห้ามเอาไปเปิด SaaS แข่งกับ n8n Cloud; self-host ใช้ภายในได้ปกติ

## อ้างอิง

- Blog: blog.n8n.io/n8n-brand-refresh-2026 · Community: community.n8n.io (thread "Our brand refresh, and why the logo changed") · guidelines.n8n.design
- ความเชื่อมกับหลักสูตร: unit 01 (ภาพรวม), unit 21 (MCP), unit 23 (multi-agent + toolWorkflow), unit 25 (self-host 2.48.5), unit 26 (n8n Agents)
