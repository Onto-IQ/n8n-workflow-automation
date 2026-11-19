# Lesson 22 — Workshop #3: RAG ด้วย Pinecone

เนื้อหาสอนประกอบ slide (slides 204–220 (หน้าจอ 197–213)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Pinecone = vector DB ยอดนิยม: ถาวร ขยายได้ ค้นแม่น; เทียบกับ Simple Vector Store (in-memory หายตอน restart, ฟรี, ใช้ prototyping)
- Index pipeline: Manual Trigger → Drive Search/Download → Default Data Loader (chunk อัตโนมัติ) → Embeddings text-embedding-3-small → Insert; ต้องตั้ง Dimension 1536 ให้ตรง model
- Query pipeline: Chat → AI RAG Agent (system prompt: ตอบเฉพาะที่มีในเอกสาร) → Pinecone Retrieve as Tool (Top K = 5)
- จุดตาย: embedding model ต้องเหมือนกันทั้ง load และ query; index n8n-demo-index; dimension 1536; metric cosine

## Demo / walkthrough
1. Load data จาก Drive folder → ถามผ่าน Chat

## Key takeaways
- เลือก store ตามงาน: ทดลองใช้ in-memory, ของจริงใช้ Pinecone

## Check understanding
- ถ้า query ใช้ embedding-002 แต่ load ใช้ text-embedding-3-small จะเกิดอะไร
