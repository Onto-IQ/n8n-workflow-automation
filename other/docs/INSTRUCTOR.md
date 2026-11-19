# Instructor notes / โน้ตสำหรับวิทยากร

Timing, demo, กับดักที่วางไว้ และ checklist ของ TA — เนื้อหา learner-facing อยู่ใน `lessons/` และ `exercises/` เท่านั้น

## Timing ต่อวัน (3 วัน)

- **วัน 1:** unit 01–09 (พื้นฐาน + credentials Google) — เผื่อเวลา setup เครื่อง 30 นาทีตาม SETUP.md; workshop #1 (unit 10) ปิดวันถ้าทัน
- **วัน 2:** unit 11–16 + workshop #2 (13), 17–20 (agents เริ่ม) — unit 13 ต้องมี Gmail + OpenAI credential ก่อน เตือนผู้เรียนตั้ง Usage limit
- **วัน 3:** unit 21–25 (MCP, Pinecone, multi-agents, agentic IDE challenge, self-host) — unit 24 challenge ให้ 45–60 นาที แล้วปิดด้วย self-host ให้ครบทุกคน

## Demos ที่ต้องเตรียมล่วงหน้า

- n8n instance สาธิต + บัญชีนักเรียน (กระดานสื่อสาร)
- credentials สาธิตที่ตั้งไว้แล้ว: Google OAuth2, LINE, OpenAI, Gemini, OpenRouter, Pinecone (index `n8n-demo-index`, dim 1536)
- workflows ทั้ง 18 ไฟล์ import ไว้ใน instance สาธิต (ใต้ `exercises/*/solution/`)
- ทดสอบ MCP endpoint ของห้องก่อนสอน unit 21

## กับดักที่วางไว้ (planted pitfalls)

- unit 05: ลืมลากเส้นกลับเข้า Loop → loop วิ่งรอบเดียวจบ
- unit 20/22: embeddings คนละ model ระหว่าง load กับ query → ค้นไม่เจอ (ให้ผู้เรียนเจอตัวเองก่อนเฉลย)
- unit 08/25: webhook ผ่าน http:// → LINE/GitHub ไม่ยิงมา — สอนแทรกเรื่อง HTTPS
- unit 15: เปิด Auto-recharge ค้าง → เตือนเรื่อง Usage limit เสมอ

## TA checklist

- [ ] ทุกเครื่องเข้า n8n ได้ทั้ง localhost และโดเมน HTTPS
- [ ] ทุกคนมี credential Google ผูกสำเร็จ (unit 09) ก่อนไป workshop #1
- [ ] เช็ค Sheets ID/Folder ID ที่ผู้เรียนวางถูกไฟล์ (workshop #1/#2/#3)
- [ ] Pinecone index พร้อม + API key ผูกแล้วก่อน unit 22
- [ ] เก็บ feedback ท้ายวัน (form)
