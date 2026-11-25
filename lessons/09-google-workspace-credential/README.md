# 09 — Credential Google Workspace (OAuth2) / Google Workspace credential

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/09-google-workspace-credential](../../exercises/09-google-workspace-credential/README.md) |
| เวลาโดยประมาณ | ~60 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 64–83 |
| คู่มือเต็ม | [other/docs/credentials/google-oauth.md](../../other/docs/credentials/google-oauth.md) |

Gmail, Sheets, Calendar, Docs, Drive ใช้ OAuth2 เหมือนกันทั้งชุด — สร้าง credential ครั้งเดียว ใช้ซ้ำได้ทุก node Google บทนี้เดินทีละขั้นบน **Google Cloud Console** (UI ปี 2026 จัดอยู่ภายใต้ Google Auth Platform) จนได้ Client ID + Client Secret มาเชื่อมใน n8n

## Credential คืออะไร

Credential คือที่เก็บกลางของ secret (API key / OAuth2 / ฐานข้อมูล) ของ n8n — ปลอดภัยกว่าการยัด key ใน node, หมุนเวียน (rotate) ง่าย และ reuse ข้าม workflow ได้ ประเภทที่เจอบ่อย: API key/token, OAuth2 (n8n refresh token ให้เอง) และ database

## ขั้นเตรียมใน Google Cloud Console

1. **สร้าง Project** — เข้า console.cloud.google.com → เลือก/สร้าง project (ในเดคใช้ชื่อแนว `n8n-student-course`) ยืนยันว่าอยู่ใน project ที่ถูกตลอด (ดูมุมบน)
2. **Google Auth Platform → Branding** (เดิมคือ OAuth consent screen) — ตั้ง App name, support email, app logo; บันทึกแล้วรอสถานะ verified หรือ testing
3. **Audience** — ตั้ง **User type = External** (หรือ Internal ถ้ามี Google Workspace องค์กร) แล้วกด **Publish app** เพื่อเลิกระบุรอบ 7 วันของ token; สำคัญ: เพิ่มตัวเองเป็น **Test users** ก่อน publish ถ้ายังอยู่โหมด Testing
4. **Enable APIs** — APIs & Services → Library → เปิดให้ครบตามที่จะใช้: **Gmail, Google Sheets, Google Drive, Google Docs, Google Calendar**
5. **Clients (สร้าง OAuth credentials)** — สร้าง OAuth Client ID ประเภท **Web application** พร้อม Authorized Redirect URI ที่ n8n แสดงให้ในหน้าสร้าง credential (คัดลอกจากหน้า n8n ไปวาง — อย่าเดาเอง)
6. เก็บ **Client ID** และ **Client Secret** — นำไปใส่ใน n8n credential "Google OAuth2 API"

## เชื่อมกลับใน n8n

1. เปิด node Gmail ใด ๆ → Credential → Create New → เลือก Google OAuth2 API
2. วาง Client ID/Secret → **Sign in with Google** → ยินยัมสิทธิ์ → กลับมาสถานะ Account connected
3. ชีต test: ให้ n8n อ่าน Google Sheet ตัวอย่างได้ 1 แถว = เสร็จ

## Demo / walkthrough

เปิดสองแท็บคู่กัน: **Google Cloud Console** ด้านหนึ่ง และหน้าสร้าง credential ใน **n8n** อีกด้าน (ค้างไว้เลย) แล้วเดินทีละขั้นตามหัวข้อด้านบน — ทุกครั้งที่ n8n ขอค่า (Redirect URI) ให้ก๊อปจากแท็บ n8n ไปวางใน Console ทันที

## ข้อควรระวัง

- Redirect URI ผิดแม้ตัวเดียว = error `redirect_uri_mismatch` — ก๊อปจาก n8n ตรง ๆ
- ลืม Enable API ที่จะใช้ = error 403 ตอนรัน node
- ห้าม commit Client Secret ลง repo — เก็บใน n8n credential เท่านั้น

## Key takeaways

- ลืม Publish App → token หมดอายุทุก 7 วัน; ลืม/ผิด Redirect URL → connect ไม่ผ่านตั้งแต่แรก
- Client ID + Secret ชุดเดียวใช้ได้ทุก service ของ Google Workspace

## ลงมือทำ

เปิด [exercises/09-google-workspace-credential/LAB.md](../../exercises/09-google-workspace-credential/LAB.md) — เดิน flow เต็มตามข้างบน จบด้วยการอ่าน Google Sheet ตัวอย่างผ่าน node ใน n8n สำเร็จ

## Check understanding

1. ทำไมต้อง Publish app ก่อนใช้งานจริง — ถ้าไม่ publish เกิดอะไรขึ้นหลังใช้ไป 7 วัน
2. เจอ `redirect_uri_mismatch` ตรวจจุดไหนก่อน
3. สิทธิ์ scope ที่ credential ขอมีผลอย่างไรกับการอนุมัติของผู้ใช้
4. OAuth Redirect URL เอามาจากที่ไหน
5. ทำไมต้อง Enable APIs เฉพาะตัวที่จะใช้

## Next

→ [exercises/09-google-workspace-credential](../../exercises/09-google-workspace-credential/README.md) — ต่อ Google Workspace ให้ n8n ได้จริง
→ บทถัดไป: [10 — Workshop #1: ฟอร์ม → Google Workspace + LINE](../10-workshop-form-to-workspace-line/README.md)
