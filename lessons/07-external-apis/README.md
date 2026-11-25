# 07 — เรียกใช้ External APIs / Working with external APIs

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/07-external-apis](../../exercises/07-external-apis/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 61 |

n8n มี integration สำเร็จรูปเยอะ แต่บริการภายในองค์กรหรือ API ใหม่ ๆ ยังต้องเรียกเอง — **HTTP Request node** คือกุญแจกัญชาสากล เรียกได้ทุก API ที่พูด HTTP บทนี้ฝึกยิง GET/POST จริง และอ่าน response ให้เป็น

## องค์ประกอบของ HTTP Request

- **Method** — GET (อ่าน), POST (สร้าง), PUT/PATCH (แก้), DELETE
- **URL** — ปลายทาง ใส่ expression ได้ เช่นดึง id จาก node ก่อนหน้า
- **Authentication** — ถ้าบริการต้องยืนยันตัว สร้าง credential (Generic Credential Type: Header Auth / Query Auth / Basic) แล้วเลือกใช้ ห้ามยัด key ลง URL ตรง ๆ
- **Body (POST)** — ส่งเป็น JSON โดยใช้ expression แทรกค่าจาก node ก่อนหน้า เช่น `{{ $json.name }}`
- **Response** — รูปแบบ JSON จะถูกแปลงเป็น items ให้อัตโนมัติ พร้อมต่อด้วย node อื่น

## เคล็ดการ debug

- รันด้วย Execute step แล้วอ่าน **Output** — โค้ด 4xx = ปัญหาที่ request เรา (auth, รูปแบบ body), 5xx = ปัญหาฝั่งเซิร์ฟเวอร์
- ทดสอบ API นอก n8n ด้วย httpbin.org หรือ Postman ก่อน ช่วยแยกว่าผิดที่ request หรือที่ n8n
- API ที่จำกัดอัตรา: ใช้ Loop ทีละ batch (หน่วย 05) แล้วเว้นจังหวะด้วย Wait

## ลงมือทำ

เปิด [exercises/07-external-apis/LAB.md](../../exercises/07-external-apis/LAB.md) — import `solution/05-Working-with-External-APIs.json` ยิง GET ไป API คำคมสาธารณะ แล้ว POST ข้อมูลขึ้น httpbin ดูรำสะท้อน

## Check understanding

1. ต่างกันอย่างไรระหว่างเก็บ API key ใน credential กับพิมพ์ใส่ header เองใน URL
2. ได้รับ 401 จาก API — สาเหตุที่พบบ่อยที่สุดคืออะไร ตรวจอย่างไร
3. จะส่งค่าจาก node ก่อนหน้าไปใน body ของ POST ได้อย่างไร

## Next

→ [exercises/07-external-apis](../../exercises/07-external-apis/README.md) — ยิง GET/POST จริงและอ่าน response
