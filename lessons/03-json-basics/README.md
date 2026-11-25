# 03 — JSON พื้นฐาน / JSON basics

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/03-json-basics](../../exercises/03-json-basics/README.md) |
| เวลาโดยประมาณ | ~60 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 43–53 |

ข้อมูลทุกอย่างที่ไหลผ่าน n8n คือ JSON — ใครอ่าน JSON คล่อง ใช้ n8n ได้ก้าวกระโดด บทนี้สอนให้อ่าน เข้าใจโครงสร้าง และดึงค่าที่ต้องการออกมาด้วย expression ได้ครบ

## JSON คือการจับคู่ Key กับ Value

```json
{ "key": "value", "number": 123, "boolean": true, "array": [1, 2, 3], "object": { "nestedKey": "nestedValue" } }
```

- **String** — ข้อความในเครื่องหมายคำพูด เช่น `"Hello"`
- **Number** — ตัวเลข `25`, `99.5`
- **Boolean** — `true` / `false`
- **Array (List)** — รายการเรียงลำดับ ใช้เก็บหลาย item เช่น รายการลูกค้า
- **Object** — กล่อง key/value ซ้อนได้ลึก (nested)
- **Null** — ไม่มีค่า

จุดที่มือใหม่สับสนที่สุดคือ **Object กับ Array ต่างกัน**: object เข้าถึงด้วยชื่อ key (`{{ $json.name }}`) ส่วน array เข้าถึงด้วยตำแหน่ง (`{{ $json.items[0] }}`) และ array มักต้องใช้ Split Out node แยกเป็นทีละ item ก่อนประมวลผล (หน่วย 05)

## อ่าน JSON จาก API จริง

ข้อมูลจาก API มักซ้อนหลายชั้น เทคนิคคือ "ไล่จากนอกเข้าใน" และสังเกตแต่ละชั้นว่าเป็น object (จับด้วย key) หรือ array (จับด้วย index) เช่น `{{ $json.data.items[0].customer.name }}` แปลว่า key `data` → key `items` → array ช่องที่ 0 → key `customer` → key `name`

## Fixed Fields vs. Expression Fields

ทุกช่องตั้งค่าใน node มีสองโหมด:

- **Fixed** — ค่าคงที่ พิมพ์ตายตัว
- **Expression** — ค่าคำนวณสด ขึ้นต้นด้วย `=` แล้วใช้ `{{ }}` ครอบนิพจน์ เช่น `={{ $json.firstName }}`

กฎเหล็ก: **ค่าที่มี `{{ }}` ต้องขึ้นต้นด้วย `=` เสมอ** ไม่งั้น n8n ส่งข้อความตรง ๆ ออกไป (ความผิดพลาดยอดฮิต — ใน repo นี้ก็มีตัวอย่างให้ระวัง)

## วิธีเข้าถึงค่าจาก node อื่น

- `{{ $json.field }}` — ค่าจาก node ก่อนหน้า (input ปัจจุบัน)
- `{{ $('Node Name').item.json.field }}` — ดึงจาก node ใดก็ได้โดยชื่อ ใช้เมื่อข้อมูลอยู่ไกลในสาย flow
- ชื่อ node คือ key ของทุกอย่าง — เปลี่ยนชื่อ node แล้วต้องไล่แก้ expression ที่อ้างถึงด้วย

## ลงมือทำ

เปิด [exercises/03-json-basics/LAB.md](../../exercises/03-json-basics/LAB.md) — import `solution/01-Learn-JSON-Basics.json` รันดูข้อมูลจริงของ JSON ทุกประเภท แล้วลองเขียน expression เองใน node สุดท้าย

## Check understanding

1. `{{ $json.orders[2].total }}` อ่านว่าอะไร และ `orders` ต้องเป็นชนิดใด
2. จะอ้างค่า field `text` จาก node ชื่อ "Extract Job Description" ได้อย่างไร
3. เกิดอะไรขึ้นถ้าลืม `=` นำหน้าค่าที่มี `{{ }}`

## Next

→ [exercises/03-json-basics](../../exercises/03-json-basics/README.md) — เจาะ JSON ด้วยข้อมูลจริงบน canvas
