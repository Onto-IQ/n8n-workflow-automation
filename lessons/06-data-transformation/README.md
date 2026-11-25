# 06 — Data Transformation / Data transformation

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/06-data-transformation](../../exercises/06-data-transformation/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 60 |

ข้อมูลที่ได้มาแทบไม่เคยอยู่ในรูปที่พร้อมใช้ — ต้องแปลง รวม เติม ตัด Data Transformation ใน n8n มีเครื่องมือหลัก 3 กลุ่ม บทนี้คุณจะเลือกใช้ให้ถูกงาน และรู้ว่าเมื่อไหร่ควรใช้ Code node

## เครื่องมือ 3 กลุ่ม

1. **Edit Fields (Set) node** — สร้าง/เปลี่ยน/ลบ field โดยไม่ต้องเขียนโค้ด ใช้บ่อยที่สุด: mapping ข้อมูลให้ตรงรูปที่ปลายทางต้องการ, เติมค่าคงที่, แปลงชนิดข้อมูล เวอร์ชันปัจจุบัน (3.4) ใช้โครงสร้าง `assignments` ระบุ `name / value / type` ต่อ field
2. **Expression ใน field ของ node อื่น** — งานแปลงเล็ก ๆ ทำในที่เดียวจบ เช่น `={{ $json.firstName + ' ' + $json.lastName }}`, `={{ $json.date.split('T')[0] }}` ไม่ต้องเพิ่ม node
3. **Code node** — JavaScript/Python เต็มรูปแบบ เมื่อ logic ซับซ้อนเกิน expression เช่น วนคำนวณ เงื่อนไขซ้อน จัดโครงสร้างใหม่ทั้งก้อน (n8n 2.x รันใน task runner sandbox แยก ปลอดภัยขึ้น)

## เทคนิคที่ใช้บ่อย

- **Formatting วันที่**: แปลง ISO timestamp เป็นรูปอ่านง่ายก่อนส่งอีเมล/ชีต
- **Mapping ก่อนส่งต่อ**: ปลายทาง (Sheets, LINE) ต้องการชื่อ field ตายตัว — Set node ชื่อให้ตรงก่อนเสมอ ลดข้อผิดพลาดปลายทาง
- **Condition pre-check**: คำนวณ field ช่วยตัดสิน เช่น `priority` จากคำใน subject แล้วให้ IF อ่าน field นี้ต่อ (แยก logic ออกจากเงื่อนไข อ่านง่ายกว่า)

## ลงมือทำ

เปิด [exercises/06-data-transformation/LAB.md](../../exercises/06-data-transformation/LAB.md) — import `solution/04-Data-Transformation.json` (mock data → Set แปลงรูป → Code เขียน logic) แล้วแก้ expression เพิ่ม field ของตัวเอง

## Check understanding

1. กรณีไหนควรใช้ Set node แล้วไปต่อใน Expression เลยไม่ได้
2. Code node รันโค้ดที่ไหนใน n8n 2.x และทำไมจึงปลอดภัยขึ้น
3. ทำไมควร map ชื่อ field ให้ตรงปลายทางตั้งแต่ต้นสาย

## Next

→ [exercises/06-data-transformation](../../exercises/06-data-transformation/README.md) — แปลงข้อมูลด้วย Set และ Code
