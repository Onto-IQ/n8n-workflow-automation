# 13 — Workshop #2: คัดกรองใบสมัครจาก Gmail / Workshop #2: Candidate screening from Gmail

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/13-workshop-candidate-screening](../../exercises/13-workshop-candidate-screening/README.md) |
| เวลาโดยประมาณ | ~90 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 124–134 |
| เฉลย | `exercises/13-.../solution/03 - Candidate Screening from Gmail.json` |
| ชุดข้อมูล | [other/datasets/JD and Resume/](../../other/datasets/JD%20and%20Resume/) |

Workshop ที่สอง: **ระบบคัดกรองผู้สมัครงานด้วย AI** — เรซูเม่หล่นเข้า Gmail → workflow ดึงมา แตกไฟล์ PDF/Word → ให้ AI อ่านเทียบกับ Job Description → ให้คะแนนความเหมาะสม บันทึกลง Sheets และตอบกลับอัตโนมัติ นี่คือ automation ที่ประหยัดเวลา HR หลายชั่วโมงต่อวัน

## ระบบประกอบด้วย 5 ขั้น

1. **Ingest — Gmail Trigger** รันเมื่ออีเมลมีคำว่า "สมัครงาน", "Resume" หรือ "CV" และมีไฟล์แนบ แล้ว Code node เตรียม candidate object รอรับ
2. **Process — Extract from File** เรซูเม่เป็นไฟล์แนบ Binary ให้ IF เช็กว่ามี resume → Loop ทีละไฟล์ → Switch แยกประเภท (.pdf / .docx / .txt) → Extract From File แตกเป็น Text (ต้องตั้ง Binary เป็น Text ให้ AI อ่านได้)
3. **Reference — ดึง Job Description** จาก Google Drive ในโฟลเดอร์ที่เตรียมไว้ (ชุดตัวอย่างอยู่ใน `other/datasets/JD and Resume/`)
4. **Analyze — AI Agent + Prompt HR Recruiter** ส่ง JD + เรซูเม่ให้ AI ตัดสินคุณสมบัติ โดยใช้ **Structured Output Parser** บังคับผลลัพธ์เป็น JSON ตาม schema ตายตัว (ชื่อ, score, recommendation) — สำคัญมาก ไม่งั้นผลลัพธ์เปลี่ยนรูปทุกครั้ง แก้ต่อยาก
5. **Output — Sheets + Gmail Send** บันทึกแถวใหม่ (Header ต้องมี Name, Score, Recommendation) และตอบกลับผู้สมัครอัตโนมัติ (อ่าน Firstname จาก AI output)

## ประเด็นเทคนิคที่ต้องระวัง

- Gmail Trigger ตั้ง filter ให้แคบพอ — อย่าดึงทุกฉบับ
- ไฟล์แนบต้องผ่าน Extract From File แปลงเป็น text ก่อนป้อน AI
- Prompt ควรระบุบทบาทชัด ("Act as an HR recruiter") + กติกาให้คะแนน 0–100 + บังคับ JSON (ใน dataset มี prompt ตัวอย่างทั้งแบบ Text และ JSON)
- ตอบกลับอีเมลต้องเป็นโทนมืออาชีพ — ระบุว่าเป็นการตอบรับเบื้องต้น ไม่ใช่ผลสุดท้าย

## Demo / walkthrough

ก่อนสร้างเอง ลอง import เฉลยจาก `solution/` แล้ว**ส่งอีเมลสมัครงานทดลอง** (หัวข้อมีคำว่า "สมัครงาน" พร้อมไฟล์แนบจาก dataset) เข้า mailbox ที่ trigger ฟังอยู่ — ดูข้อมูลวิ่งทีละขั้นตามสถาปัตยกรรม 5 ขั้นด้านบน

## Key takeaways

- สูตรรับไฟล์ที่ใช้ได้กับงานเอกสารทุกประเภท: **Binary → Text → AI → Structured output**

## ลงมือทำ

เปิด [exercises/13-workshop-candidate-screening/LAB.md](../../exercises/13-workshop-candidate-screening/LAB.md) — import เฉลยทีละ node หรือสร้างเอง ใช้ JD/Resume ตัวอย่างใน dataset ทดสอบ แล้วเช็กแถวใน Sheets + อีเมลตอบกลับ

## Check understanding

1. Structured Output Parser ช่วยอะไร และถ้าไม่ใช้ ระบบจะเปราะตรงไหน
2. เรซูเม่เป็น PDF แนบมา — ขั้นไหนแปลง และต้องแปลงเป็นอะไร
3. ทำไมต้องกรอง subject ที่ Gmail Trigger แทนปล่อยทุกฉบับเข้า AI

## Next

→ [exercises/13-workshop-candidate-screening](../../exercises/13-workshop-candidate-screening/README.md) — สร้างระบบคัดกรองที่ใช้ได้จริง
→ บทถัดไป: [14 — Credential Google AI Studio (Gemini)](../14-google-ai-credential/README.md)
