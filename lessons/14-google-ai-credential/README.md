# 14 — Credential Google AI Studio (Gemini) / Google AI Studio credential

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/14-google-ai-credential](../../exercises/14-google-ai-credential/README.md) |
| เวลาโดยประมาณ | ~30 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 136–142 |
| คู่มือเต็ม | [other/docs/credentials/gemini-api.md](../../other/docs/credentials/gemini-api.md) |

Gemini คือโมเดลฟรีที่สมัครง่ายที่สุดสำหรับเริ่มงาน AI — บทนี้สร้าง API key จาก Google AI Studio แล้วต่อเข้า n8n ให้ node Gemini ใช้ได้จริง พร้อมรีวิว workflow LINE Chat Gemini จากหน่วยก่อน

## ขั้นบน Google AI Studio

1. เข้า aistudio.google.com ด้วยบัญชี Google
2. เปิดหน้า **API keys** (แถบเมนูซ้าย หรือ aistudio.google.com/apikeys) → **Create API key**
3. เลือก project (สร้างใหม่ได้ในหน้าต่างเดียว เช่นชื่อ "Gemini Project") → กดสร้าง → **คัดลอก key เก็บทันที** (Google จะไม่โชว์ซ้ำ) — ห้ามส่ง/commit ลง repo เด็ดขาด

## เชื่อมใน n8n

1. สร้าง credential **Google Gemini (PaLM) API** → วาง API key
2. ทดสอบด้วย node จริง: ลาก Google Gemini Chat Model เข้า agent แล้วเลือก credential — เห็นรายชื่อโมเดลโหลดขึ้น = เชื่อมสำเร็จ
3. เข้าใจสองจุดใน node Gemini: **model** (เลือกตามงาน) และ credential แชร์ข้าม workflow ได้เหมือน credential อื่น

## ทางเลือกบน Google Cloud (สำหรับ self-host/องค์กร)

ถ้าต้องการคุม project/billing ระดับองค์กร สร้าง Gemini API key ได้จาก **Google Cloud Console** เช่นกัน (หน้า Welcome → Create Gemini API key หรือ Vertex AI สำหรับสัญญา enterprise) — key ทั้งสองทางเรียก Gemini API ได้เหมือนกัน

## ลงมือทำ

เปิด [exercises/14-google-ai-credential/LAB.md](../../exercises/14-google-ai-credential/LAB.md) — สร้าง key, ตั้ง credential, และรีวิว workflow `solution/01 - LINE Chat Gemini Model.json` ให้ Gemini ตอบแชท LINE ได้จริง

## Check understanding

1. สร้าง key แล้วทำหาย — ทำอย่างไรได้ key ใหม่ และผลต่อ key เดิมอย่างไร
2. สองทางสร้าง Gemini key (AI Studio กับ Cloud Console) เลือกเมื่อไหร่
3. ทดสอบ credential สำเร็จ/ไม่สำเร็จ ตรวจจากอะไรใน n8n

## Next

→ [exercises/14-google-ai-credential](../../exercises/14-google-ai-credential/README.md) — ต่อ Gemini ให้ agent แรกของคุณ
