# 02 — เริ่มต้น Workflow แรก / Your first workflow

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/02-first-workflow](../../exercises/02-first-workflow/README.md) |
| เวลาโดยประมาณ | ~40 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 30–34 และ 35–42 |

หัวใจของ n8n มีแค่ประโยคเดียว: **Trigger → Node → Node** ข้อมูลเริ่มจาก trigger หนึ่งตัว ไหลผ่าน node ทีละตัว แต่ละตัวรับข้อมูล ทำงานตามหน้าที่ แล้วส่งผลต่อไป บทนี้คุณจะสร้าง workflow แรกด้วยมือตัวเองตามสูตรนี้จริง ๆ: กดปุ่ม → ส่งอีเมล

## หน้าจอที่ต้องรู้จัก

- **Overview** — ศูนย์กลางจัดการ workflow, credentials, executions
- **Canvas** — ผืนผ้าใบสำหรับวางและต่อ node ("Add first step" คือจุดเริ่มของทุก workflow)
- **Nodes panel** — คลัง node ทั้งหมด ค้นหาจากชื่อบริการได้ในช่อง search

## Trigger คืออะไร มีกี่แบบ

Trigger คือ node แรกที่ "เริ่ม workflow" ทุก workflow ต้องมีตัวเดียวเสมอ:

- **Trigger manually** — กดปุ่มรันเอง (เหมาะกับตอนเรียน/ทดสอบ)
- **On a schedule** — รันตามเวลา (ทุกวัน 09:00 ฯลฯ)
- **On app event** — เหตุการณ์จากแอป เช่น Telegram, Notion
- **On webhook call** — รับ HTTP request เข้ามา (หน่วย 08 เจาะลึก)
- **On form submission** — ฟอร์มของ n8n เอง
- **When executed by another workflow** — ถูกเรียกจาก workflow อื่น

เลือก trigger ผิด = ระบบไม่ทำงานตามโลกจริง: งานแจ้งเตือนทันเหตุการณ์ใช้ webhook/app event, งานสรุปรายวันใช้ schedule, งานทดลองใช้ manual

## หลักการทำงานของ workflow

1. ข้อมูลวิ่งเป็น **items** (รายการ) หนึ่ง trigger อาจส่งมาหลาย items
2. แต่ละ node รับ items เข้า ทำงาน แล้วส่ง items ออก
3. เส้นเชื่อม (connection) กำหนดทิศทาง — แยก branch ได้ (IF, Switch) และรวมกลับได้ (Merge)
4. **Execute step / Execute workflow** คือปุ่มทดสอบ — รันแล้วดู Input/Output ของแต่ละ node ได้ทันที นี่คือวิธี debug หลักของ n8n
5. ค่าเริ่มต้นคือรันแบบ **Sequential** — ทีละ node เรียงต่อกันจนจบ ถ้าต้องการให้บางสายทำงานพร้อมกัน (**Parallel**) ต้องตั้งค่าเพิ่ม

## Key takeaways

- ทุก workflow เริ่มที่ trigger เสมอ
- ตอนทดสอบใช้ Manual trigger ก่อนเสมอ แล้วค่อยเปลี่ยนเป็น trigger จริงเมื่อขึ้นใช้งาน

## ลงมือทำ: สร้าง "01 - Firstflow"

1. **Add workflow** ใหม่ → คลิก **Add first step…** กลาง canvas
2. เลือก **Trigger manually**
3. กด **+** ต่อจาก trigger → ค้นหา **Gmail** → เลือก action **Send a message** แล้วกรอก To / Subject / Message
4. เชื่อม credential (ถ้ายังไม่มี ทำหน่วย 09 ก่อนแล้วกลับมา)
5. กด **Execute workflow** แล้วเช็กกล่องจดหมาย (ดับเบิลคลิก node เพื่อดู Input/Output ที่ไหลผ่าน)
6. ตั้งชื่อ workflow "01 - Firstflow" แล้ว **Save**

## Check understanding

1. ทำไม workflow ต้องมี trigger หนึ่งตัวเสมอ
2. งาน "สรุปยอดขายส่งอีเมลทุกวัน 09:00" ควรใช้ trigger แบบใด
3. ปุ่ม Execute step ช่วยอะไรเวลา workflow เดินไม่ถูก

## Next

→ [exercises/02-first-workflow](../../exercises/02-first-workflow/README.md) — สร้าง Firstflow ด้วยมือตัวเองแล้วเทียบกับเฉลย
→ บทถัดไป: [03 — JSON พื้นฐาน](../03-json-basics/README.md)
