# 08 — Webhooks & Triggers / Webhooks & triggers

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/08-webhooks](../../exercises/08-webhooks/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 62 |

Webhook คือ "ประตูรับข้อมูลจากภายนอก" — ระบบอื่นยิง HTTP POST เข้า URL ของเราเมื่อเกิดเหตุการณ์ (ข้อความ LINE, commit ใน GitHub, คำสั่ง Shopify) แล้ว workflow เราทำงานทันที นี่คือหัวใจของ automation แบบเรียลไทม์ และเป็นจุดเริ่มของ AI Agent ที่โต้ตอบกับผู้ใช้ได้

## Test URL กับ Production URL

Webhook node มี **สอง URL ต่างกันเสมอ**:

- **Test URL** (`/webhook-test/...`) — ใช้ตอนกด "Listen for test event" ใช้ได้เฉพาะตอนกำลังกดฟัง
- **Production URL** (`/webhook/...`) — ใช้งานจริง ทำงานเมื่อ workflow ถูก **Publish/Activate** แล้วเท่านั้น

สับสนสอง URL นี้ = อาการ "ยิงแล้วไม่มา" ยอดฮิตอันดับหนึ่งของผู้เรียน

## ขั้นตอนทดสอบที่ถูกต้อง

1. เปิด workflow ที่มี Webhook node → กด **Listen for test event**
2. ยิง request ด้วย curl หรือ Postman ไปที่ Test URL เช่น `curl -X POST <test-url> -H "Content-Type: application/json" -d '{"name":"ชื่อคุณ"}'`
3. n8n จับ payload → เดิน flow ตามที่ต่อไว้ (ในตัวอย่างคอร์ส: Set สร้างข้อความตอบกลับ → Respond to Webhook ส่งกลับผู้เรียก)
4. **Respond to Webhook node** ตอบกลับผู้ยิงได้เลย (ต้องตั้ง Webhook response mode = Using Respond to Webhook Node)

## กับดัก HTTPS (สำคัญกับ self-host)

Production webhook ของบริการภายนอก (LINE, Telegram, GitHub) รับเฉพาะ `https://` และฟีเจอร์เบราว์เซอร์ที่ต้อง secure context (chat, notifications) ใช้ได้เฉพาะ HTTPS หรือ localhost — self-host ต้องตั้ง Cloudflare Tunnel ตามหน่วย 25 และตั้ง `WEBHOOK_URL` ใน `.env` ให้เป็น URL เต็ม `https://`

## ลงมือทำ

เปิด [exercises/08-webhooks/LAB.md](../../exercises/08-webhooks/LAB.md) — import `solution/06-Webhooks-and-Triggers.json` ฟัง test event ยิง curl ที่มี JSON ตัวอย่าง แล้วดูข้อมูลไหลผ่าน Respond to Webhook

## Check understanding

1. Test URL กับ Production URL ต่างกันอย่างไร ใช้ช่วงเวลาไหน
2. ยิง webhook แล้ว n8n ไม่ตอบสนอง — ไล่ตรวจ 3 อย่างแรกอะไร
3. ทำไม LINE ยิง webhook มาไม่ได้เมื่อ n8n รันผ่าน `http://` (ไม่ใช่ localhost)

## Next

→ [exercises/08-webhooks](../../exercises/08-webhooks/README.md) — รับข้อมูลจากภายนอกด้วย webhook จริง
