# 05 — Loop การวนซ้ำ

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/05-loops](../../exercises/05-loops/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 58–59 |

ข้อมูลมาเป็นกลุ่ม (3 คน, 100 อีเมล, 50 ใบสมัคร) แต่การประมวลผลมักต้องทำ **ทีละรายการ** — Loop คือคำตอบ ใน n8n มีสอง node คู่หู: **Split Out** แยก array ใหญ่เป็นหลาย items และ **Loop Over Items** วนทำทีละ batch

## Split Out: แยก array เป็น items

ข้อมูลจาก API มักมาเป็น array ใน key เดียว เช่น `{ "students": [ {...}, {...}, {...} ] }` — n8n มองมันเป็น item เดียว Split Out node ดึง key `students` ออกมาแตกเป็น 3 items แยกกัน ค่าหลักคือ **Field to split out** (ชื่อ key ที่เก็บ array)

## Loop Over Items: วนทีละ batch

- **Batch size** = จำนวน item ต่อรอบ (1 = ทีละชิ้น ปลอดภัยสุดกับ API ที่จำกัดอัตรา)
- มี **สองเส้นออก**: `loop` (ยังเหลือ item — งานรอบนี้ทำตรงนี้) และ `done` (ครบแล้ว — ไปสรุปผลต่อ)
- **กฎเหล็ก: ต้องลากเส้นกลับจาก node สุดท้ายของลูปเข้า Loop node อีกครั้ง** ไม่งั้นลูปวิ่งรอบเดียวจบ — เป็นกับดักยอดฮิตของคอร์ส (ดู [INSTRUCTOR.md](../../other/docs/INSTRUCTOR.md))
- เช็คผล: เปิด execution detail จะเห็นแต่ละรอบรับ item ไหน ใช้ยืนยันว่าลูปครบทุกคนจริง

## ลงมือทำ

เปิด [exercises/05-loops/LAB.md](../../exercises/05-loops/LAB.md) — import `solution/03-Flow-Control-Demo-Loop-V2.json` (หมายเหตุ: ไฟล์ V2 ใน repo ขณะนี้ยังไม่มี Loop node — ให้ดูวิธีที่ถูกต้องจาก `03-Flow-Control-Demo-Loop.json` ประกอบ) รันดูรอบการวน 3 รอบ แล้วเพิ่ม node ในวงลูปให้ทำงานจริงต่อคน เช่น เติม field greeting

## Check understanding

1. Split Out กับ Loop Over Items ต่างกันอย่างไร — จำเป็นต้องใช้คู่กันเสมอไหม
2. batch size = 2 กับ = 1 ต่างกันอย่างไร กรณีไหนควรเพิ่ม
3. ถ้าลืมเส้น loop-back ระบบจะทำงานอย่างไร และตรวจพบได้จากอะไร

## Next

→ [exercises/05-loops](../../exercises/05-loops/README.md) — วนประมวลผลนักเรียน 3 คนให้ครบทุกคน
