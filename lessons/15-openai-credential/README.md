# 15 — Credential OpenAI / OpenAI credential

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/15-openai-credential](../../exercises/15-openai-credential/README.md) |
| เวลาโดยประมาณ | ~30 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 144–149 |
| คู่มือเต็ม | [other/docs/credentials/openai-api.md](../../other/docs/credentials/openai-api.md) |

OpenAI ใช้กับ AI Agent ขั้นสูง (GPT-4o ขึ้นไป) และมีค่าใช้จ่ายจริง — บทนี้สร้าง credential ให้ถูกตั้งแต่ต้น ตั้ง **Usage limit กันเงินหาย** และยกระดับ **Auto-recharge** อย่างเข้าใจ

## ขั้นบน platform.openai.com

1. สมัคร/ล็อกอิน **platform.openai.com** (ไม่ใช่ ChatGPT — คนละระบบ; API key ของ ChatGPT Plus ไม่ใช้กับ API ได้)
2. **ตั้งค่าการชำระเงิน (Billing)** → Add payment details (บัตร หรือยูสส์ผ่าน Stripe) → เติมเงินขั้นต่ำ $5 สำหรับ Prepaid หรือเปิด Postpaid ตามที่เลือก
3. **ตั้ง Usage limits** — กำหนดเพดานต่อเดือน + ยืนยันด้วยอีเมล กันบิลพุ่งจากโค้ดวิ่งผิดพลาด
4. **Auto-recharge** — เติมอัตโนมัติเมื่อยอดถึงขั้นต่ำ สะดวกแต่ต้องมี limit คู่กันเสมอ (กับดักที่วางไว้ในคอร์ส: เปิด Auto-recharge ค้างโดยไม่จำกัด = บิลบาน)
5. **สร้าง API key** — หน้า API keys → Create new secret key → ตั้งชื่อ (เช่น n8n-course) → เลือก Project/Permissions → **คัดลอกเก็บทันที** (แสดงครั้งเดียว)

## เชื่อมใน n8n

1. สร้าง credential **OpenAI** → วาง API key
2. ทดสอบ: ลาก **OpenAI Chat Model** เข้า agent → เลือก credential → เลือกโมเดล (แนะนำเริ่ม gpt-4o-mini สำหรับงานเบา) — เห็นรายชื่อโมเดล = เชื่อมสำเร็จ
3. ชีตที่ node อื่นอ้าง credential นี้จะใช้ได้ทันทีทั้ง workflow

## ข้อควรระวัง

- Key คือรหัสผ่าน — ห้าม commit/ส่งต่อ ถ้ารั่วให้ Revoke ทันที
- Prepaid หมดยอด = API กลับ 429 กลางงาน — จุดให้ตรวจเวลา workflow รันเป็นระยะแล้วพัก
- เก็บ key ไว้ใน OpenAI dashboard แบบจำกัด project/permission เมื่อใช้งานจริง

## ลงมือทำ

เปิด [exercises/15-openai-credential/LAB.md](../../exercises/15-openai-credential/LAB.md) — เดินครบทั้ง billing/limit/key แล้วผูก credential กับ node OpenAI Chat Model ใน n8n

## Check understanding

1. ChatGPT Plus กับ OpenAI API ต่างกันอย่างไร
2. Usage limit ช่วยอะไร และควรตั้งก่อนหรือหลังสร้าง key เพราะอะไร
3. Auto-recharge เปิดเมื่อไหร่จึงปลอดภัย

## Next

→ [exercises/15-openai-credential](../../exercises/15-openai-credential/README.md) — ต่อ OpenAI พร้อมกันเงินหาย
