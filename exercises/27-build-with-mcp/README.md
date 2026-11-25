# Exercise 27 — Build with MCP: สั่งสร้าง Workflow ด้วย Prompt

คู่กับ [lessons/27-build-with-mcp](../../lessons/27-build-with-mcp/) — ชื่อโฟลเดอร์ `NN-slug` ตรงกันเสมอ

| | |
|--|--|
| Hands-on | [LAB.md](LAB.md) |
| Starter | [starter/](starter/) |
| Solution | [solution/](solution/) |

ไฟล์ workflow สำเร็จรูป:
- `solution/01 - Daily RSS Digest.json`

หมายเหตุ: ไฟล์นี้คือ **ผลลัพธ์ปลายทาง** ที่ผู้เรียนต้องได้จากการสั่งด้วย prompt บน instance ตัวเอง (ไม่ใช่ไฟล์สำหรับ import ตามหน่วยก่อน ๆ) — ทำเสร็จแล้วค่อยเปิดเทียบ

## Goal / เป้าหมาย
- เปิด Instance-level MCP บน instance ส่วนตัวของคุณ เชื่อม MCP client (Cursor หรือ Claude) แล้วสั่งสร้าง workflow "Daily RSS Digest" ด้วย prompt ล้วน ผ่าน validate แก้ error publish และรันจริงจนได้อีเมล

## Before you start
- เรียน lesson คู่กันจบก่อน (หรืออ่าน [README.md](../../lessons/27-build-with-mcp/README.md))
- **instance ต้องเป็นของคุณเองและคุณเป็น owner** (หน่วย 25) — ห้ามใช้ instance ร่วมกับผู้อื่น URL และ token ของใครของมัน
- มี MCP client พร้อม (Cursor หรือ Claude Code/Desktop) และ credential Gmail ผูกไว้แล้วจากหน่วย 09/13
- อย่าเปิด `solution/` จนกว่าจะลองเองก่อน
