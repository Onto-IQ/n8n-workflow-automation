# 20 — Simple RAG + Memory / Simple RAG with memory

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/20-simple-rag-memory](../../exercises/20-simple-rag-memory/README.md) |
| เวลาโดยประมาณ | ~60 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 176–185 |
| เฉลย | `exercises/20-.../solution/03-Simple-RAG-with-Memory.json` |
| ชุดข้อมูล | [other/datasets/บริษัท สมสมัยงาน AI จำกัด/](../../other/datasets/บริษัท%20สมสมัยงาน%20AI%20จำกัด/) |

โมเดลไม่รู้เอกสารองค์กรของคุณ — **RAG (Retrieval-Augmented Generation)** แก้ด้วยการทำ "ความจำองค์กร": ยิงเอกสารเข้า Vector Store แล้วให้ agent ค้นด้วยความหมาย (ไม่ใช่ค้นคำตรง) แล้วนำข้อความที่เกี่ยวมาตอบ บทนี้สร้าง RAG อย่างง่ายด้วย In-Memory Vector Store จากนโยบายบริษัทตัวอย่าง

## RAG ทำงาน 2 ทาง

- **Ingestion (ฝั่งโหลด)** — อ่านไฟล์ → Embeddings node แปลงข้อความเป็น vector → เขียนลง Vector Store
- **Retrieval (ฝั่งถาม)** — Query Data node ค้นด้วย vector ของคำถาม → ส่ง chunk ที่เกี่ยวเข้า agent เป็นบริบท
- ทั้งสองทาง **ต้องใช้ embedding model ตัวเดียวกัน** — คนละ model = ค้นไม่เจอ (กับดักที่วางไว้ในคอร์ส ดู [INSTRUCTOR.md](../../other/docs/INSTRUCTOR.md))

## ทำไมยุค Context 1M+ ยังต้องมี RAG

- **Long Context ไม่ฟรี** — ยัดเอกสารยักษ์ทั้งก้อนเข้า prompt แพงและช้า (Context Caching ช่วยบางส่วนเมื่อข้อมูลซ้ำ)
- **Precision vs. Noise** — context ใหญ่มี noise, Lost in the Middle ทำให้สาระตรงกลางหาย; RAG กรองเอาแค่ 2–3 chunks ที่เกี่ยว (~500 คำ) ให้ AI โฟกัส
- **Economics & Latency** — ทุก chat ที่ยัด 1M tokens แพงกว่า/ช้ากว่ามาก ส่วน caching ช่วยได้กับข้อความ static เท่านั้น (ข้อมูลล้วนลึกเปลี่ยนบ่อยใน n8n)
- **สรุป: อนาคตคือ Hybrid** — Context Caching กับ System Prompt ให้ของซ้ำ และ RAG (Vector Store) สำหรับข้อมูลเฉพาะที่เปลี่ยนบ่อย

## ลงมือทำ: Simple RAG with Memory (สอง flow)

1. **Load Data Flow** — Index Trigger → อ่านไฟล์นโยบาย (Mock Policy Data / Default Data Loader) → **Insert Data to Store** (In-Memory Vector Store + OpenAI Embeddings)
2. **Retriever Flow** — Chat Trigger → AI Agent มี **Simple Memory** + **Query Data Tool** (ให้ agent ค้น Vector Store เองเมื่อจำเป็น) → OpenAI Chat Model สังเคราะห์คำตอบจากข้อมูลจริงในเอกสาร
3. ทดสอบด้วยคำถามจากนโยบาย เช่น "เบี้ยเลี้ยงไปญี่ปุ่นเท่าไหร่?" — คำตอบต้องอ้างจากเอกสาร

## ลงมือทำ

เปิด [exercises/20-simple-rag-memory/LAB.md](../../exercises/20-simple-rag-memory/LAB.md) — สร้างทั้งสอง flow, โหลดข้อมูล, แล้วถาม-ตอบผ่าน chat ด้วยข้อมูลจากเอกสารจริง

## Check understanding

1. Ingestion กับ Retrieval ต่างกันอย่างไร — ทำไมต้อง embedding model เดียวกัน
2. ทำไม context window ใหญ่ยังไม่ทำให้ RAG ตาย
3. ถ้าตอบไม่ตรงเอกสาร ตรวจจุดไหนก่อน (model / loader / query)

## Next

→ [exercises/20-simple-rag-memory](../../exercises/20-simple-rag-memory/README.md) — ทำความจำองค์กรด้วย RAG อย่างง่าย
