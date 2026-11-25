# 22 — Workshop #3: RAG ด้วย Pinecone / Workshop #3: RAG with Pinecone

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/22-workshop-rag-pinecone](../../exercises/22-workshop-rag-pinecone/README.md) |
| เวลาโดยประมาณ | ~90 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 197–213 |
| เฉลย | `exercises/22-.../solution/04 - RAG with Pinecone (Load + Query).json` |
| คู่มือเต็ม | [other/docs/credentials/pinecone.md](../../other/docs/credentials/pinecone.md) |

Workshop ปิดท้าย: **RAG ระดับ production บน Pinecone** — อัปเกรดจาก In-Memory (หน่วย 20) เป็น Vector Database จริง: ข้อมูลรอด restart, ค้นเร็ว, ขยายได้ เอกสารจาก Google Drive ถูกโหลดเข้า index แล้ว agent ตอบจากเอกสารจริงผ่าน chat

## ระบบประกอบด้วย (Workshop Components)

- **Data Source** — Google Drive (โฟลเดอร์ PDF/Doc นโยบายองค์กร)
- **Vector Database** — Pinecone (ถาวร, ขยายตามการใช้งาน)
- **LLM & Embeddings** — OpenAI (GPT-4o-mini + text-embedding-3-small)
- ตั้งชื่อ workflow ตัวอย่าง: "Chatbot ตอบคำถามจากเอกสารของฉัน"

## ความจำแบบไหนเหมาะกับ AI ของคุณ (ตัดสินใจให้ถูก)

| คุณสมบัติ | Simple Vector Store (In-Memory) | Pinecone (Vector Database) |
|---|---|---|
| การเก็บข้อมูล | ในหน่วย RAM (session นั้น) | ระบบ cloud ของ Pinecone (ถาวร) |
| ความถนัด | ตัวอย่าง RAG สาธิต ทดสอบเร็ว | Production: รองรับข้อมูลจำนวนมากและผู้ใช้หลายคน |
| ความถนัด (persist) | เป็นระยะ (หมดเมื่อ restart) | การ (ข้อมูลไม่หาย) |
| ความยืดหยุ่น | จำกัด (resource เครื่อง) | ขยายอัตโนมัติ (scale) |
| ความเร็ว | แช่ง (Zero Setup) | ยืดหยุ่น (มี network hop) |
| หลังไม่คิด | ฟรี (ในตัว) | มี Free Tier |

**เลือกใช้**: In-Memory สำหรับ prototyping/สอน (session สั้น ข้อมูลหลายไม่สำคัญ) Pinecone เมื่อต้อง production (ข้อมูลถาวร หลายผู้ใช้ อัปโหลดเอกสารใหม่บ่อย) — อัปเกรดยังไงก็ได้: เปลี่ยน Vector Store กับเพิ่ม credential Pinecone

## ขั้นเตรียม Pinecone (Credential สำหรับ Vector DB)

1. สมัคร pinecone.io (**Start Free** ระดับ Starter) — กรอกชื่อ/อีเมล/Password/Organization "Personal"
2. สร้าง **Project** (เช่น `n8n-rag-course`, Region us-east-1)
3. หากได้ Default API key ให้คัดลอกเก็บไว้; **สร้าง Index** (เก็บข้อมูล vector) — Index name `n8n-demo-index`, Dimension **1536** (ตรง text-embedding-3-small), Metric cosine, Serverless; **สำคัญ: ถ้าใช้ embedding model อื่น ตั้ง Dimension ให้ตรง (เช่น large = 3072) — จุดตายที่ทำให้ค้นไม่เจอ**
4. ขอ/คัดลอก API key → สร้าง Credential ใน n8n

## สอง pipeline ใน workflow เฉลย (Load + Query)

- **Indexing Pipeline** — Manual Trigger → ค้นหาไฟล์ใน Drive Folder → Download (binary) → Default Data Loader (chunk) → Embeddings OpenAI → **Vector Store (Pinecone Insert)** — ระวังตั้ง Dimension ให้ตรงโมเดล
- **Query Pipeline** — Chat Trigger (รับคำถามจาก chat) → AI Agent (The Brain) + System Prompt "ตอบพื้นฐานเฉพาะที่มีในเอกสาร" → **Pinecone Query (as Tool)** — Top K = 5

## จุดตายที่ห้ามพลาด (Critical Settings)

| ช่องปรับค่า | ค่าที่ต้องตรงกัน (Value) |
|---|---|
| Embeddings Model | text-embedding-3-small (ห้าม Load ใช้ตัวหนึ่ง Query อีกตัวหนึ่ง) |
| Pinecone Index | n8n-demo-index (ชื่อ index ที่สร้าง) |
| Dimensions | 1536 (ต้องตรงกับ embedding model) |
| Credentials | OpenAI, Pinecone API, Google Drive OAuth2 |

## ลงมือทำ

เปิด [exercises/22-workshop-rag-pinecone/LAB.md](../../exercises/22-workshop-rag-pinecone/LAB.md) — สมัคร/ตั้ง Pinecone ให้ครบ, รัน Load, แล้วถามผ่าน Chat ให้ตอบจากเอกสารจริง

## Check understanding

1. In-Memory กับ Pinecone ใช้ตัวไหนเมื่อไหร่ — เกณฑ์ตัดสินสองข้อ
2. Dimension ไม่ตรงกับ embedding model เกิดอะไรขึ้น ตรวจจากไหน
3. ทำไม Load กับ Query ต้องใช้ embedding model เดียวกัน

## Next

→ [exercises/22-workshop-rag-pinecone](../../exercises/22-workshop-rag-pinecone/README.md) — RAG ระดับ production จริงบน Pinecone
