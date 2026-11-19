# Workflow Automation with n8n — L1 (Onto-IQ)

หลักสูตรอบรม **Automation ด้วย n8n ตั้งแต่เริ่มต้นจนถึง AI Agents** — เรียนแบบทำตามมือ (hands-on) ทีละหน่วย (unit) โดยเนื้อหาอิง slide deck ประกอบการสอน (271 หน้า) และอัปเดตให้ตรงกับ **n8n 2.x + Brand Refresh ปี 2026**

> จัดโดย Onto-IQ · ภาษาไทยอธิบาย + คำสั่ง/เครื่องมือเป็นอังกฤษ

## 1. Overview

คอร์สนี้ครอบคลุมตั้งแต่การสร้าง workflow แรก การจัดการข้อมูล JSON การต่อ Google Workspace / LINE ไปจนถึงการสร้าง AI Agents (memory, tools, RAG, MCP, multi-agents) และการ self-host n8n ด้วย Docker + Cloudflare Tunnel

ผู้เรียนจะได้:

- สร้าง automation ของตัวเองบน n8n canvas ได้ตั้งแต่วันแรก
- ต่อบริการจริง (Gmail, Sheets, Calendar, Docs, Drive, LINE, OpenAI, Gemini, OpenRouter, Pinecone)
- สร้าง AI Agent ที่มี memory ใช้ tools และตอบจากเอกสารองค์กร (RAG) ได้
- เข้าใจสิ่งใหม่สำคัญของ n8n ยุค 2.x และ rebrand 2026 (Agent-first) — สรุปใน [n8n 2026 rebrand & 2.x notes](other/reference/n8n-2026-rebrand-and-2x.md)
- เปิดให้ AI อื่นใช้เครื่องมือของเราผ่าน MCP และสร้าง workflow ด้วย agentic IDE

## 2. Audience / กลุ่มเป้าหมาย

**เหมาะกับ:** ผู้ไม่เคยใช้ n8n มาก่อน, พนักงานออฟฟิศที่อยากทำ automation, นักพัฒนาที่อยากใช้ low-code ต่อ AI, ทีม IT/HR/Marketing

**ไม่เหมาะกับ:** ผู้ต้องการสอนการเขียนโปรแกรมเชิงลึก (คอร์สนี้ใช้ JS/Python เพียงเล็กน้อยใน Code node)

## 3. Prerequisites / สิ่งที่ต้องเตรียม

ดูรายละเอียดและคำสั่งตรวจสอบทั้งหมดใน [SETUP.md](SETUP.md)

- **ความรู้:** ใช้คอมพิวเตอร์/เบราว์เซอร์เป็น, มีความเข้าใจ JSON เบื้องต้นจะสบายขึ้น (สอนซ้ำใน unit 03)
- **ซอฟต์แวร์/บัญชี:** บัญชี Google, LINE, Docker Desktop, โดเมนของตัวเอง + Cloudflare (สำหรับ self-host), คีย์ AI (เราสร้างระหว่างเรียน)
- **ฮาร์ดแวร์:** เครื่อง Windows/macOS RAM ≥ 8 GB สำหรับรัน Docker

## 4. Lesson outline / หัวข้อการเรียน

เรียนตามลำดับ 25 หน่วย — ทุกหน่วยมี lesson (ทฤษฎี) และ exercise (ลงมือทำ) แยกโฟลเดอร์กัน

| # | หัวข้อ | Lesson | Exercise | ~นาที |
|---|--------|--------|----------|-------|
| 01 | n8n คืออะไร (+ rebrand 2026) | [01-what-is-n8n](lessons/01-what-is-n8n/) | [exercise](exercises/01-what-is-n8n/) | 45 |
| 02 | เริ่มต้น Workflow แรก | [02-first-workflow](lessons/02-first-workflow/) | [exercise](exercises/02-first-workflow/) | 40 |
| 03 | JSON พื้นฐาน | [10-json-basics](lessons/10-json-basics/) | [exercise](exercises/10-json-basics/) | 60 |
| 04 | Flow Control (IF/Switch/Merge) | [12-flow-control](lessons/12-flow-control/) | [exercise](exercises/12-flow-control/) | 45 |
| 05 | Loop | [13-loops](lessons/13-loops/) | [exercise](exercises/13-loops/) | 45 |
| 06 | Data Transformation | [11-data-transformation](lessons/11-data-transformation/) | [exercise](exercises/11-data-transformation/) | 40 |
| 07 | External APIs | [14-external-apis](lessons/14-external-apis/) | [exercise](exercises/14-external-apis/) | 40 |
| 08 | Webhooks & Triggers | [15-webhooks](lessons/15-webhooks/) | [exercise](exercises/15-webhooks/) | 40 |
| 09 | Credential Google Workspace | [16-google-workspace-credential](lessons/16-google-workspace-credential/) | [exercise](exercises/16-google-workspace-credential/) | 60 |
| 10 | Workshop #1: ฟอร์ม → Workspace + LINE | [19-workshop-form-to-workspace-line](lessons/19-workshop-form-to-workspace-line/) | [exercise](exercises/19-workshop-form-to-workspace-line/) | 90 |
| 11 | Credential LINE OA | [18-line-oa-credential](lessons/18-line-oa-credential/) | [exercise](exercises/18-line-oa-credential/) | 45 |
| 12 | สถานการณ์ LLM ปี 2026 | [03-llm-landscape](lessons/03-llm-landscape/) | [exercise](exercises/03-llm-landscape/) | 40 |
| 13 | Workshop #2: คัดกรองใบสมัครจาก Gmail | [17-workshop-candidate-screening](lessons/17-workshop-candidate-screening/) | [exercise](exercises/17-workshop-candidate-screening/) | 90 |
| 14 | Credential Google AI (Gemini) | [04-google-ai-credential](lessons/04-google-ai-credential/) | [exercise](exercises/04-google-ai-credential/) | 30 |
| 15 | Credential OpenAI | [05-openai-credential](lessons/05-openai-credential/) | [exercise](exercises/05-openai-credential/) | 30 |
| 16 | Credential OpenRouter | [06-openrouter-credential](lessons/06-openrouter-credential/) | [exercise](exercises/06-openrouter-credential/) | 30 |
| 17 | AI Agent คืออะไร | [07-ai-agents-concepts](lessons/07-ai-agents-concepts/) | [exercise](exercises/07-ai-agents-concepts/) | 40 |
| 18 | Chat Agent + Memory | [08-chat-agent-memory](lessons/08-chat-agent-memory/) | [exercise](exercises/08-chat-agent-memory/) | 45 |
| 19 | Agent + Tools (Function Calling) | [09-agent-with-tools](lessons/09-agent-with-tools/) | [exercise](exercises/09-agent-with-tools/) | 45 |
| 20 | Simple RAG + Memory | [20-simple-rag-memory](lessons/20-simple-rag-memory/) | [exercise](exercises/20-simple-rag-memory/) | 60 |
| 21 | MCP Client & Server | [22-mcp-client-server](lessons/22-mcp-client-server/) | [exercise](exercises/22-mcp-client-server/) | 60 |
| 22 | Workshop #3: RAG ด้วย Pinecone | [21-workshop-rag-pinecone](lessons/21-workshop-rag-pinecone/) | [exercise](exercises/21-workshop-rag-pinecone/) | 90 |
| 23 | Multi-Agents (Linear vs Orchestration) | [23-multi-agents](lessons/23-multi-agents/) | [exercise](exercises/23-multi-agents/) | 90 |
| 24 | Bonus: สร้าง Flow ด้วย Agentic IDE | [24-agentic-ide-bonus](lessons/24-agentic-ide-bonus/) | [exercise](exercises/24-agentic-ide-bonus/) | 60 |
| 25 | Self-Hosting n8n (Docker + Cloudflare) | [25-self-hosting](lessons/25-self-hosting/) | [exercise](exercises/25-self-hosting/) | 90 |

Workshop หลัก 3 ชิ้น: **#1** ระบบรับเรื่องฟอร์ม → Google Workspace + LINE (unit 10), **#2** คัดกรองใบสมัครด้วย AI (unit 13), **#3** ระบบถาม-ตอบจากเอกสารองค์กรด้วย RAG (unit 22)

## 5. How to run the exercises / วิธีทำแบบฝึกหัด

1. อ่าน `lessons/NN-slug/` ก่อน แล้วเปิด `exercises/NN-slug/`
2. ทำตาม `LAB.md` — สร้าง workflow เอง (หรือ import จาก `starter/` ถ้ามี)
3. **พยายามเองก่อน** แล้วค่อยเทียบกับ `solution/` (มี workflow .json พร้อมรัน 18 ไฟล์)
4. เช็คความสำเร็จด้วยหัว "Check your work" ท้าย LAB ทุกหน่วย

นำเข้า workflow เร็ว ๆ: เปิดไฟล์ `.json` → copy ทั้งหมด → วางบน canvas ของ n8n (หรือ Workflow → Import from File / URL)

## 6. Slide deck

Deck ประกอบการสอน (258 หน้า หลังตัดหน้าโฆษณา): [`other/slides/N8N-L1-Onto-IQ-v6.pptx`](other/slides/) — ทุก lesson ระบุช่วง slide อ้างอิงไว้ในตารางด้านบนของหน้า lesson

## 7. Course description (JD)

สำเนาคำอธิบายคอร์สอยู่ที่ [other/docs/JD.md](other/docs/JD.md) (source of truth: Obsidian `Courses/n8n-workflow-automation-L1.md`)

## 8. Repository layout / โครงสร้าง

```text
├── README.md                # outline คอร์ส (ไฟล์นี้)
├── COURSE.md                # manifest ของคอร์ส (เครื่องมืออ่านค่าจากนี้)
├── SETUP.md                 # สิ่งที่ต้องเตรียมก่อนวันแรก
├── CONTRIBUTING.md          # วิธีเพิ่ม/แก้เนื้อหา
├── CHANGELOG.md
├── lessons/NN-slug/         # ทฤษฎี: README.md + LESSON.md
├── exercises/NN-slug/       # ลงมือทำ: README.md + LAB.md + starter/ + solution/
├── org/                     # โน้ต topic-family ขององค์กร (onto-iq / datafabric-academy)
├── other/
│   ├── slides/              # deck ประกอบการสอน
│   ├── datasets/            # ข้อมูลตัวอย่าง + case studies (ชื่อไทยได้)
│   ├── docs/                # JD, instructor notes, คู่มือ credentials
│   ├── reference/           # สรุป n8n 2026 rebrand + 2.x, cheat sheets
│   ├── assets/              # รูป/แผนภาพ
│   └── scripts/             # check_structure.sh + migrate scripts
├── docker-compose.yml       # รัน n8n (n8n + postgres + cloudflared)
└── .env.example             # ตั้งค่า .env ก่อน compose up
```

กฎ: lesson กับ exercise แยกโฟลเดอร์, ชื่อหน่วยเป็น `NN-slug` ASCII เท่านั้น, ไฟล์ประกอบอื่นใส่ใต้ `other/` เท่านั้น — ตรวจโครงสร้างด้วย `bash other/scripts/check_structure.sh` (รันใน CI ผ่าน `.github/workflows/structure-check.yml`)

## 9. Self-host รัน n8n ของคุณเอง (สรุป)

```bash
git clone https://github.com/Onto-IQ/n8n-workflow-automation.git
cd n8n-workflow-automation
cp .env.example .env        # แก้ POSTGRES_PASSWORD / N8N_HOST / WEBHOOK_URL / CLOUDFLARE_TUNNEL_TOKEN
docker compose up -d        # local: http://localhost:5678
```

HTTPS จำเป็นสำหรับ webhook/chat — ตั้ง Cloudflare Tunnel ตาม [SETUP.md](SETUP.md) และ unit 25

### การจัดการ n8n

```bash
docker compose down                # หยุด
docker compose logs -f n8n         # ดู log
docker compose pull && docker compose up -d   # อัปเดตเวอร์ชัน
docker compose exec n8n n8n user-management:reset   # ลืมรหัสผ่าน
```

**สำรองข้อมูล** — `data/postgres/` (DB: workflows, credentials, executions) และ `data/n8n/` (config + **Encryption Key** ใช้ถอดรหัส credentials) ต้องมีทั้งคู่จึง restore ได้ครบ:

```bash
cp -r data data-backup-$(date +%Y%m%d)
```

> อย่าลบ `data/` ถ้าต้องการเก็บ workflow/credentials ที่สร้างไว้ — restore: นำโฟลเดอร์กลับมาเป็น `data/` ใช้ `.env` เดิม (อย่างน้อย `POSTGRES_USER/PASSWORD/DB`) แล้ว `docker compose up -d`

### ทำไมต้อง HTTPS

Webhook production ของบริการภายนอก (LINE, Telegram, Shopify, GitHub) รับเฉพาะ `https://`; ฟีเจอร์เบราว์เซอร์ที่ต้อง secure context (chat, notifications) ใช้ได้เฉพาะ HTTPS/localhost; ข้อมูลที่ไม่เข้ารหัสเสี่ยง MITM และกระทบความน่าเชื่อถือขององค์กร โปรเจกต์นี้จึงใช้ Cloudflare Tunnel ให้ HTTPS โดยไม่ต้องจัด certificate เอง

## 10. License / Credits

เนื้อหาเพื่อการศึกษา © 2026 Onto-IQ — สไลด์และโครงสร้างหลักสูตรจัดทำโดย Aj. Phakkhaphong Krittawat; workflow ตัวอย่างใช้ MIT license เว้นแต่ระบุอื่น อ้างอิง [n8n docs](https://docs.n8n.io/) และ [n8n community](https://community.n8n.io/)
