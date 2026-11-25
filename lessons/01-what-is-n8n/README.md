# 01 — n8n คืออะไร / What is n8n

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/01-what-is-n8n](../../exercises/01-what-is-n8n/README.md) |
| เวลาโดยประมาณ | ~45 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 5–27 |

ก่อนจะลากวาง workflow ตัวแรก เราต้องเข้าใจก่อนว่า n8n คืออะไร ทำไมองค์กรทั่วโลกถึงใช้ และมีรูปแบบการใช้งานแบบไหนให้เลือก บทนี้เป็นทฤษฎีล้วน ไม่ต้องเขียนโค้ด — อ่านจบแล้วคุณจะเลือกรูปแบบการใช้งานให้เหมาะกับตัวเองได้ และเห็นภาพว่า n8n ยุค 2.x + brand refresh ปี 2026 ต่างจากเดิมอย่างไร

## n8n คืออะไร

n8n (อ่านว่า "เอ็น-เอท-เอ็น") คือ **workflow automation platform** แบบ fair-code ที่ให้คุณต่อทุกอย่างเข้าด้วยกันด้วยการลากวาง (low-code/no-code) บนผืนผ้าใบ (canvas) แทนการเขียนสคริปต์เอง ในตัวมี integration สำเร็จรูปมากกว่า 2,300 บริการ — Gmail, Google Sheets, LINE, Slack, OpenAI, ฐานข้อมูล, HTTP API ทั่วไป — จุดขายคือคนที่ไม่ใช่นักพัฒนาก็สร้างระบบอัตโนมัติได้ แต่ถ้าต้องการความละเอียดสูงก็ยังฝังโค้ด JavaScript/Python ใน Code node ได้

## ประโยชน์และตัวอย่างการใช้งาน

งานที่ n8n ทำได้ดีคืองานที่ "เกิดขึ้นแล้วต้องตามด้วยอะไรบางอย่างเสมอ" เช่น ลูกค้ากรอกฟอร์ม → บันทึกลงชีต → สร้างนัดหมาย → แจ้งทีมทาง LINE หรือ อีเมลใบสมัครเข้ามา → AI อ่านและให้คะแนน → บันทึกผล → ตอบกลับผู้สมัคร ทุกตัวอย่างในคอร์สนี้คืองานแบบนี้ทั้งหมด

## License: MIT กับ Sustainable Use

- **MIT** ครอบคลุม core engine และ nodes — ใช้ แก้ แจกจ่ายได้เต็มที่
- **Sustainable Use License** ครอบคลุมฟีเจอร์ enterprise/cloud — source available แต่ห้ามนำไปเปิด SaaS แข่งกับ n8n Cloud; self-host ใช้ภายในองค์กรได้ปกติ

## รูปแบบการใช้งาน 3 แบบ

| รูปแบบ | เหมาะกับ | ข้อควรรู้ |
|---|---|---|
| **n8n Cloud** (~€20/เดือน) | ทีมเล็กที่อยากเริ่มเร็ว ไม่มี DevOps | ไม่ต้องดูแลเซิร์ฟเวอร์ แต่รันบนโครงสร้างของ n8n |
| **Self-host องค์กร** | องค์กรที่ต้องควบคุมข้อมูล 100% | ต้องมีคนดูแล Docker/backup (หน่วย 25 สอนเอง) |
| **Self-host บน VPS** | งบจำกัด ทีมเทคนิคเล็ก | ค่าใช้จ่ายต่ำ รับผิดชอบความปลอดภัยเอง |

## สิ่งใหม่ของ n8n ยุค 2.x และ brand refresh 2026

- **Publish vs Save** — แยกฉบับ draft ออกจากฉบับที่ production กำลังรันจริง แก้/ทดสอบได้โดยไม่กระทบงานที่บินอยู่ (หลักการเดียวกับ CI/CD)
- **Secure-by-default Task Runners** — โค้ดใน Code node รันใน sandbox แยก กัน infinite loop หรือ memory leak ลาก instance หลักล้ม
- **Wait Node 2.0** — sub-workflow ที่รอ (เช่น รอ approval) คืนผลลัพธ์สุดท้ายให้ parent ได้ถูกต้อง
- **ประสิทธิภาพ** — SQLite pooling และ binary data บน filesystem เร็วขึ้นราว 10×
- **MCP (Model Context Protocol)** — เปิดเครื่องมือของเราให้ AI ตัวอื่นเรียกใช้ (หน่วย 21 และ 24)
- **Brand refresh** — "Agent-first, Workflow second": AI Agent รับงานก่อน แล้วเสริมด้วย workflow ที่ deterministic เฉพาะจุด สรุปเต็มที่ [other/reference/n8n-2026-rebrand-and-2x.md](../../other/reference/n8n-2026-rebrand-and-2x.md)

## ลงมือทำ

เปิด [exercises/01-what-is-n8n/LAB.md](../../exercises/01-what-is-n8n/LAB.md) — ลองเข้า n8n ครั้งแรก ทำความรู้จัก 3 จุด (Overview / Canvas / Nodes panel) และนำเข้า workflow ไฟล์แรกจาก repo นี้

## Check understanding

1. MIT กับ Sustainable Use License ต่างกันอย่างไร และมีผลต่อการนำ n8n ไปใช้ในองค์กรอย่างไร
2. Publish กับ Save ใน n8n 2.x ต่างกันอย่างไร และช่วยงาน production อย่างไร
3. ทีม 5 คน ไม่มี DevOps อยากเริ่มเร็ว ควรเลือกรูปแบบใด เพราะอะไร

## Next

→ [exercises/01-what-is-n8n](../../exercises/01-what-is-n8n/README.md) — ลงมือใช้ n8n ครั้งแรก
