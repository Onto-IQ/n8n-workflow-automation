# Lesson 01 — n8n คืออะไร

เนื้อหาสอนประกอบ slide (slides 12–34 (หน้าจอ 5–27 ของไฟล์ใหม่)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- n8n เป็น workflow automation platform แบบ fair-code ใช้ visual interface ลากวาง (low-code/no-code) เชื่อมต่อ 2,300+ integrations
- Brand Refresh 2026: โลโก้ใหม่ ฟอนต์ใหม่ สีชมพูที่ปรับอ่อนลงคู่เฉดเทา — "Intelligence made visible", "AI makes intelligence possible. n8n makes intelligence operational.", "Agent-first, Workflow second" (AI Agent รับงานก่อน แล้วเสริม workflow ตายตัวเฉพาะจุดที่ต้อง deterministic)
- License: MIT (core + nodes) และ Sustainable Use License (ฟีเจอร์ enterprise/cloud — ห้ามเอาไปทำ SaaS แข่ง แต่ self-host ใช้ได้)
- n8n 2.x: Publish vs Save (แยก draft ออกจาก production), Secure-by-default Task Runners (รัน JS/Python ใน sandbox), Wait Node 2.0 (sub-workflow คืนค่าสุดท้ายถูกต้อง), SQLite pooling + filesystem binary (เร็วขึ้น ~10x, ลด database locked), AI Evaluation nodes, MCP support, Autosave, Migration Report 1.x→2.x
- 3 รูปแบบใช้งาน: n8n Cloud (€20/เดือน, ง่ายสุด), Self-host องค์กร (ควบคุมข้อมูล 100%), Self-host บน VPS (ค่าใช้จ่ายต่ำ) — เปรียบเทียบตามตารางหน้า 27 ของ slide

## Demo / walkthrough
1. เปิด n8n → รู้จักหน้า Overview (ศูนย์กลางจัดการ workflow, credentials, templates)
2. ท่อง Templates (หน้า 32) และวิธีใส่ Activation key ที่ Billing > Plan & usage (หน้า 33)

## Key takeaways
- n8n = orchestrator ที่ต่อทุกอย่างเข้าด้วยกันโดยไม่ต้องพึ่งนักพัฒนา
- ยุคใหม่ของ n8n คือแพลตฟอร์มของ workflow + AI agents ไม่ใช่แค่ workflow engine

## Check understanding
- ต่างกันอย่างไรระหว่าง MIT กับ Sustainable Use License?
- Publish กับ Save ใน n8n 2.x ต่างกันอย่างไร
- ทีม 5 คนอยากเริ่มเร็วและไม่มี DevOps ควรเลือกรูปแบบไหน
