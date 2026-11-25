# 11 — Credential LINE OA / LINE OA credential

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/11-line-oa-credential](../../exercises/11-line-oa-credential/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 94–112 |
| คู่มือเต็ม | [other/docs/credentials/line-oa.md](../../other/docs/credentials/line-oa.md) |

LINE Official Account (OA) คือช่องทางลูกค้าหลักขององค์กรไทย — บทนี้เตรียมทุกอย่างให้ n8n ส่ง/รับข้อความ LINE ได้: สร้าง Provider และ Messaging API channel บน LINE Developers Console, ออก Channel Secret + Channel Access Token, ติดตั้ง community node ฝั่ง n8n และเชื่อม webhook สองฝั่งให้คุยกันได้

## ขั้นฝั่ง LINE Developers Console

1. เข้า developers.line.biz ล็อกอินด้วยบัญชี LINE Business ID
2. **สร้าง Provider** — คือนิติบุคคล/หน่วยงานที่เป็นเจ้าของ channel (ตั้งชื่อตามองค์กร) กด Create
3. **สร้าง Messaging API channel** ภายใต้ Provider นั้น กรอกชื่อ/รูป/คำอธิบาย
4. **สร้าง LINE OA Account** — ถ้ายังไม่มี OA ให้สร้างจากหน้าเดียวกัน (Create a LINE Official Account)
5. เข้า **LINE OA Manager → Messaging API** เลือก Provider ที่สร้างไว้ → กด Enable Messaging API (ยินยัม)
6. ออกค่ารับรองสองค่า: **Channel Secret** (ที่แท็บ Basic settings กด Issue) และ **Channel Access Token** (แท็บ Messaging API กด Issue — มีอายุ ยืนยันตอนออก)

## ขั้นฝั่ง n8n

1. **ติดตั้ง Community node "LINE Messaging"** (`@aotoki/n8n-nodes-line-messaging`) — Settings → Community nodes → Install (สำคัญ: self-host ต้องติดตั้งเอง และหลังติดตั้งต้อง restart)
2. ตรวจการติดตั้งใน Settings → Community nodes ให้เห็นรายการ
3. **สร้าง Credential "Line Messaging API"** — วาง Channel Access Token และ Channel Secret สองค่าจากขั้นบน
4. **เชื่อม Webhook สองฝั่ง** — คัดลอก Production Webhook URL ของ workflow ฝั่ง n8n (ต้องเป็น https จริง) ไปวางใน Messaging API ของ LINE แล้วกด Update; ทดสอบโดยกด "Listen for test event" ฝั่ง n8n แล้วส่งข้อความหา OA — ต้องเห็น event มาถึง

## ข้อควรระวัง

- Webhook ต้องเป็น HTTPS เท่านั้น — self-host ต้องมี Cloudflare Tunnel (หน่วย 25)
- สองฝั่งต้องพร้อมพร้อมกัน: ฝั่ง LINE เปิด "Use webhook" และฝั่ง n8n workflow active
- Token หมดอายุ/ถูกออกใหม่ = credential ใช้ไม่ได้ ต้องออกใหม่และวางใหม่

## Key takeaways

- Webhook URL ของ n8n ต้องไปอยู่ฝั่ง LINE ด้วย — สองฝั่งพร้อมพร้อมกันจึงคุยกันได้

## ลงมือทำ

เปิด [exercises/11-line-oa-credential/LAB.md](../../exercises/11-line-oa-credential/LAB.md) — เดิน console ทีละหน้า ติดตั้ง node, สร้าง credential, และยืนยันว่าข้อความหา OA มาถึง n8n

## Check understanding

1. Channel Secret กับ Channel Access Token ใช้ทำอะไรต่างกัน
2. ข้อความเข้า OA แต่ n8n ไม่เห็น event — ไล่ตรวจจุดไหนก่อน
3. ทำไม self-host ต้องติดตั้ง community node เอง และตรวจยังไงว่าติดตั้งสำเร็จ

## Next

→ [exercises/11-line-oa-credential](../../exercises/11-line-oa-credential/README.md) — ต่อ LINE OA ให้ n8n ครบสองทาง
→ บทถัดไป: [12 — สถานการณ์ LLM ปี 2026](../12-llm-landscape/README.md)
