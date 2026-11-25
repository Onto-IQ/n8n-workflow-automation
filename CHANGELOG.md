# Changelog

## Unreleased

- **Deck v7** (`other/slides/N8N-L1-Onto-IQ-v7.pptx`): จัดลำดับการเล่าใหม่ให้ตรงโครง repo (ย้ายบล็อก JSON หลังหน่วย 02), แทนภาพหน้าจอเก่าด้วยภาพจริงปี 2026-11 (n8n 2.48.5 จาก n8n.ontoiq.tech, Google Cloud/Google Auth Platform, Pinecone, Cloudflare Tunnel, OpenRouter), แก้สารบัญให้ตรงหน้าใหม่; v6 เก็บไว้เป็นฐานอ้างอิง
- **เขียน README บทเรียนใหม่ทั้ง 25 หน่วย** — `lessons/NN-slug/README.md` มีเนื้อหาบทเรียนเต็ม (จาก LESSON.md ขยาย) พร้อมขั้นตอนลงมือทำและช่วง slide ตาม v7; LESSON.md ยังอยู่เป็นสรุปย่อ
- ปรับโครงสร้าง repo ตาม [course-template](https://github.com/phakkhaphong/course-template): `lessons/` + `exercises/` แยกคู่กัน 25 หน่วย, เอกสารประกอบรวมใต้ `other/`, เพิ่ม `COURSE.md` / `SETUP.md` / `CONTRIBUTING.md` และ structure check (bash + CI)
- ย้าย workflow ทั้ง 22 ไฟล์เดิมจาก `workflows/` ไปเป็น `solution/` ของหน่วยที่เกี่ยวข้อง; case studies ไป `other/datasets/`; คู่มือ credentials ไป `other/docs/credentials/`
- Slide deck เวอร์ชัน Onto-IQ (`other/slides/N8N-L1-Onto-IQ-v6.pptx`, 258 หน้า): ลบหน้าโฆษณาหัว/ท้าย ลบ footer ลิขสิทธิ์และโลโก้เดิมออกจากทุกหน้า/master/layout ปรับแบรนด์เป็น Onto-IQ และตัด media ที่ไม่ใช้แล้ว (101.8 MB → 29.9 MB)
- เพิ่มเนื้อหาใหม่จาก n8n brand refresh 2026 และ n8n 2.x (Publish vs Save, secure task runners, Wait 2.0, MCP, evaluation nodes) — สรุปใน `other/reference/n8n-2026-rebrand-and-2x.md`

## 2026-11 (ก่อนปรับโครงสร้าง)

- อัปเกรด workflow และ docker stack สำหรับ n8n 2.28.6 + สคริปต์ migrate node schemas
- เพิ่มคู่มือ HTTPS (Cloudflare Tunnel) สำหรับ webhook และ chat
