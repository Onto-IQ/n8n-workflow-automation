# 04 — Flow Control: IF, Switch, Merge

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/04-flow-control](../../exercises/04-flow-control/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 54–57 |

ระบบจริงไม่ได้วิ่งเส้นตรง — ต้องเลือกทาง แยกกรณี และรวมผลกลับ Flow Control ใน n8n มี 3 ตัวหลัก: **IF** แยกสองทาง (จริง/เท็จ), **Switch** แยกหลายทางตามค่า, **Merge** รวมสายข้อมูลกลับมาบรรจบกัน

## IF Node (v2.3)

ตรรกศาสตร์ง่ายที่สุด: เงื่อนไขหนึ่งข้อ ผลลัพธ์สองทาง (true / false)

- รูปแบบเงื่อนไข v2: `{ id, leftValue, rightValue, operator { type, operation } }` เช่น `leftValue = {{ $json.priority }}`, operator `string equals`, `rightValue = HIGH`
- หลายเงื่อนไขต่อกันด้วย **AND** (ต้องจริงทุกข้อ) หรือ **OR** (จริงข้อใดข้อหนึ่ง) — AND เข้มกว่า ใช้เมื่ออยาก "กันพลาด"
- operation ที่ใช้บ่อย (ชื่อมาตรฐานหลัง migrate เป็น 2.x): `equals`, `notEquals`, `contains`, `startsWith`, `isEmpty`, `notEmpty`, `gt`, `gte`, `lt`, `lte`, `regex`
- `typeValidation: strict` ช่วยจับข้อมูลชนิดไม่ตรง เช่น เทียบเลขกับข้อความ

## Switch Node

IF ที่มีหลายประตู — เหมาะกับงานจัดเกรด/จัดหมวด เช่น score ≥ 80 → ทาง A, ≥ 50 → ทาง B, ที่เหลือ → fallback ตั้งได้หลายทาง และมีทาง fallback สำรองเสมอ

## Merge Node

รวมสองสายกลับด้วยโหมดต่างกัน: **Append** (ต่อท้ายกัน), **Combine** (จับคู่ตาม key), **Choose branch** (รอสายแรกที่มาถึง) ใช้บ่อยเมื่อ "ข้อมูลจากสองแหล่งต้องมาอยู่ด้วยกันก่อนส่งต่อ"

## สูตรคิดก่อนวาง

เขียนเงื่อนไขเป็นประโยคก่อนเสมอ: "ถ้า priority เท่ากับ HIGH → ส่ง LINE ทันที ไม่งั้น → เข้าคิวปกติ" แล้วแปลงเป็น IF หนึ่งตัว ทาง true/false ชัดเจน ค่อยต่อ branch ปลายทางต่อจากนั้น

## ลงมือทำ

เปิด [exercises/04-flow-control/LAB.md](../../exercises/04-flow-control/LAB.md) — import `solution/02-Flow-Control-Demo.json` (ระบบจัดเกรดนักเรียน: mock data → IF เช็ก VIP → Switch แยกเกรด → Merge) รันดูข้อมูลแยกทางจริง แล้วเพิ่มเงื่อนไขของตัวเอง

## Check understanding

1. กรณีไหนต้องใช้ Switch แล้ว IF ไม่พอ
2. AND กับ OR ใน IF ต่างกันอย่างไร — ยกตัวอย่างเงื่อนไขที่ต้องใช้ OR
3. Merge แบบไหนใช้เมื่อ "รอข้อมูลสองสายมาครบแล้วค่อยทำต่อ"

## Next

→ [exercises/04-flow-control](../../exercises/04-flow-control/README.md) — เดินข้อมูลผ่าน IF และ Switch ด้วยมือ
