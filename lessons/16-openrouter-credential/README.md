# 16 — Credential OpenRouter / OpenRouter credential

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/16-openrouter-credential](../../exercises/16-openrouter-credential/README.md) |
| เวลาโดยประมาณ | ~30 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 151–157 |
| คู่มือเต็ม | [other/docs/credentials/openrouter-api.md](../../other/docs/credentials/openrouter-api.md) |

OpenRouter คือ "ศูนย์รวมโมเดล AI" — key เดียว เรียกได้ทั้ง Claude, Llama, Meta, รวมถึงโมเดลจาก OpenAI และ Gemini ในอินเทอร์เฟซเดียว เหมาะกับงานที่อยากสลับโมเดล/ลองของใหม่โดยไม่สมัครหลายบริการ และมีโมเดลฟรีให้ทดลอง

## ขั้นบน openrouter.ai

1. สมัครสมาชิก (Sign in ผ่าน Google หรืออีเมล) → เข้า Dashboard
2. **เติมเครดิต (ทางเลือก)** — Settings → Credits → Add credit (เติมขั้นต่ำ ~$5 เมื่อจะใช้รุ่นเสียง); โมเดลฟรีใช้ได้โดยไม่ต้องเติม แต่มีโควตา/ข้อจำกัดตามระดับบัญชี
3. **สร้าง API key** — หน้า Keys → Create Key → ตั้งชื่อ (เช่น "n8n Router Key") → (Optional) ตั้ง Credit limit ต่อ key เพื่อกันใช้เกิน → สร้างแล้ว **คัดลอกเก็บทันที** (แสดงครั้งเดียว)

## เชื่อมใน n8n

1. สร้าง credential **OpenRouter** → วาง API key
2. ผูกกับ **OpenRouter Chat Model** node ใน agent → เลือกโมเดล (ฟรี: โมเดลที่ติดป้าย free; เสียง: Claude/GPT/Gemini ตามเครดิต) — เห็นรายการโมเดลโหลดขึ้น = สำเร็จ
3. สลับโมเดลเพื่อเทียบคุณภาพ/ราคาได้ใน node เดียวโดยไม่แก้ logic

## ข้อควรระวัง

- เครดิตหมด = request ล้มเหลวกลาง flow ระวังตอนรันงานจำนวนมาก
- โมเดลฟรีมีข้อจำกัดเรื่องอัตราและคุณภาพ — เหมาะกับทดลอง ไม่ใช่ production
- เก็บ key ใน credential เท่านั้น ห้าม commit

## ลงมือทำ

เปิด [exercises/16-openrouter-credential/LAB.md](../../exercises/16-openrouter-credential/LAB.md) — สมัคร, สร้าง key, ตั้ง credential แล้วทดลองสลับโมเดลใน agent เดียว

## Check understanding

1. OpenRouter ต่างจากสมัครตรงกับผู้ให้บริการอย่างไร — จุดดี/จุดเสีย
2. Credit limit ต่อ key ช่วยอะไร และควรตั้งเมื่อไหร่
3. โมเดลฟรีใช้ทำงานจริงได้ไหม จำกัดตรงไหน

## Next

→ [exercises/16-openrouter-credential](../../exercises/16-openrouter-credential/README.md) — key เดียว เข้าถึงหลายโมเดล
