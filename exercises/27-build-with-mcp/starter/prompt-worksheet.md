# Prompt Worksheet — ออกแบบคำสั่งสร้าง Workflow ด้วย MCP

กรอกให้ครบก่อนพิมพ์ prompt จริง — prompt ที่ดีระบุครบ 5 อย่าง: ชื่อ, trigger, nodes, credential, ขอบเขต (ยังไม่ publish)

## 1. ข้อมูลของ instance คุณ (ไม่ต้องอยู่ใน prompt — อยู่ใน config ของ client)
- URL instance: `https://____________________` (ของคุณเอง ห้ามใช้คนอื่น)
- client ที่ใช้: [ ] Cursor   [ ] Claude Code   [ ] Claude Desktop   [ ] อื่น ๆ: ____
- วิธีเชื่อม: [ ] OAuth   [ ] API key

## 2. โครง workflow ที่จะสั่งสร้าง
| รายการ | ค่าที่จะใส่ใน prompt |
|---|---|
| ชื่อ workflow | `Daily RSS Digest` |
| Trigger | Schedule Trigger ทุกวัน 09:00 |
| Node ที่ 2 | RSS Read — `https://hnrss.org/frontpage` |
| Node ที่ 3 | Gmail ส่งไปที่ ______________ หัวข้อ `📰 Daily Digest` |
| Credential | Gmail (จากหน่วย 09/13) |

## 3. Prompt หลัก (รอบ 1 — สร้าง) — กรอกส่วนว่างแล้วลองพิมพ์จริง
```text
สร้าง workflow ชื่อ "Daily RSS Digest" บน instance ของฉัน:
Schedule Trigger ทุกวัน 09:00 → RSS Read (https://hnrss.org/frontpage)
→ Gmail ส่งสรุปข่าว 5 อันดับแรกไปที่ ______________ หัวข้อ "📰 Daily Digest"
ใช้ credential Gmail ที่มีอยู่ ตั้งชื่อ node ให้สื่อความหมาย
ยังไม่ต้อง publish — validate ให้เรียบร้อยก่อนแล้วรายงาน error/warning ทั้งหมด
```

## 4. คลัง prompt ทดลองแล้ว (ใช้ซ้ำได้จริง)

**ตรวจก่อนเสมอ:**
```text
validate workflow "Daily RSS Digest" แล้วแจ้ง error และ warning ทั้งหมด
ยังไม่ต้องแก้ — รายงานก่อน
```

**แก้วนซ้ำจนผ่าน:**
```text
แก้ error และ warning ทั้งหมด แล้ว validate ซ้ำจนผ่าน ยังไม่ต้อง publish
```

**หา node / ตรวจ schema ก่อนสั่งสร้าง (ลดการเดา):**
```text
หา node ใน n8n สำหรับอ่าน RSS บอกชื่อ type, version ล่าสุด และ parameter ที่ต้องใส่
```

**เช็คสภาพ instance:**
```text
list my workflows        (ต้องเห็นเฉพาะของ instance นี้)
```

**Publish — อนุมัติด้วยตัวเองก่อนเสมอ:**
```text
publish workflow "Daily RSS Digest" ตั้งชื่อเวอร์ชันว่า "first build via MCP"
```

**รันทดสอบ:**
```text
execute workflow "Daily RSS Digest" ด้วยโหมด manual แล้วสรุปผลที่ได้
```

**วินัยท้าย session:**
```text
ยกเลิกการเชื่อมต่อ / revoke client นี้จาก Connected clients หลังใช้งานเสร็จ
```

## 5. ข้อห้ามใน prompt (วินัยปลอดภัย)
- ❌ ห้ามขอให้ AI "publish เลยตอนที่ยังไม่ได้ตรวจ" — publish ต้องมาจากการอนุมัติของคุณ
- ❌ ห้ามใส่ API key / token / รหัสผ่านใน prompt — credential อยู่ใน n8n เสมอ
- ❌ ห้ามชี้ URL instance ของคนอื่น — แม้จะมี key ก็ตาม

## 6. เกณฑ์ว่า "สำเร็จ"
- [ ] prompt รอบ 1 ได้ workflow ครบ 3 node บน instance คุณ
- [ ] validate ผ่านหมดก่อน publish (รอบ 2 ถ้าจำเป็น)
- [ ] publish history มีเวอร์ชัน "first build via MCP"
- [ ] ได้อีเมลจริง 1 ฉบับจาก execution
