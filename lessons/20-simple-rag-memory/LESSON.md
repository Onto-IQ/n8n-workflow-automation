# Lesson 20 — Simple RAG + Memory

เนื้อหาสอนประกอบ slide (slides 183–192 (หน้าจอ 176–185)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- RAG = ดึงข้อมูลเกี่ยวข้องจาก knowledge base มาแปะ prompt ก่อนส่ง LLM
- Ingestion: Mock Policy Data → Default Data Loader → Embeddings → Insert ลง vector store; Retrieval: Chat → Agent → Query Data Tool → คำตอบ
- เหล็กกล้า: Insert กับ Retrieve ต้องใช้ embeddings node model/settings เดียวกัน ไม่งั้น vector ไม่ตรง ค้นไม่เจอ
- Long context (1M+) ไม่ได้ฆ่า RAG: Lost in the Middle (noise ลดความแม่น), cost/latency สูง, cache คุ้มเมื่อข้อมูลนิ่ง — best practice คือ Hybrid: cache สิ่งนิ่ง + RAG สำหรับฐานความรู้ใหญ่ที่ค้นเฉพาะจุด

## Demo / walkthrough
1. Import จาก solution/ → Execute ส่วน load → เปิด Chat ถามนโยบายบริษัทจำลอง (สมสมัยงาน AI จำกัด — ไฟล์ใน other/datasets/)

## Key takeaways
- ถาม "เบี้ยเลี้ยงไปญี่ปุ่นเท่าไหร่?" แล้วตามด้วย "แล้วเกาหลีล่ะ?" — agent ต้องรู้ context ว่าหมายถึงเบี้ยเลี้ยง

## Check understanding
- ทำไม embedding ทั้งสองฝั่งต้องเป็น model เดียวกัน
