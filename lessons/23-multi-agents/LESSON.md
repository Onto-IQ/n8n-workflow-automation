# Lesson 23 — Multi-Agents: Linear vs Orchestration

เนื้อหาสอนประกอบ slide (slides 221–226 (หน้าจอ 214–219)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Linear (05A): เรียงลำดับ Form → Intent Classifier → Policy Validator (RAG) → Response Generator → Gmail — ง่ายแต่ย้อนแก้ไม่ได้ ไม่มี QA
- Orchestration (05B): ตัวหลักเป็น orchestrator เรียก sub-agent เป็น tools ผ่าน toolWorkflow (แนวคิด n8n 2.x): Intent Classifier / Policy Validator / Finance Calculator / QA Reviewer — loop กลับเมื่อ QA ไม่ผ่าน มี self-correction
- จุดเด่นของแบบใหม่: 20+ nodes → ~12, แยก sub-workflow ไฟล์ จัดการ/reuse ง่าย ไม่รก main, Memory (contextWindowLength 3) + Output Parser + IF gate แทน code node ซับซ้อน
- สร้าง sub-workflow: workflow ใหม่ใช้ Execute Workflow Trigger → return ผลลัพธ์ → main เรียกด้วย toolWorkflow

## Demo / walkthrough
1. รัน 05A จบสายตรง → รัน 05B แล้วสร้างเคสที่ QA สั่ง revision

## Key takeaways
- Linear สำหรับงานง่ายตายตัว / Orchestration เมื่อต้องมี QA + แก้ซ้ำ

## Check understanding
- ทำไมแยก sub-agent เป็น sub-workflow ดีกว่าซ้อนในไฟล์เดียว
