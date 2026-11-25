# 23 — Multi-Agents: Linear vs Orchestration / Multi-agents

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/23-multi-agents](../../exercises/23-multi-agents/README.md) |
| เวลาโดยประมาณ | ~90 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 214–219 |
| เฉลย | `exercises/23-.../solution/05A - Linear Multi-Agent Refund & Claim.json`, `05B - Orchestration Multi-Agent Refund & Claim.json` (+ 05B-Sub-* 4 ไฟล์) |

เมื่องานซับซ้อนเกิน agent ตัวเดียว องค์กรมีสองสถาปัตยกรรมให้เลือก: **Linear** (เรียง agent ต่อกันเป็นสาย) กับ **Orchestration** (agent แม่เรียก sub-agent ผ่าน toolWorkflow) เคสตัวอย่างคอร์ส: **ระบบรับเรื่อง Refund & Claim** — จำแนกเจตนา, ตรวจนโยบาย (RAG), คำนวณเงิน, ตรวจทานคุณภาพ ก่อนส่งอีเมล

## แบบ A: Linear (Sequential)

เรียง agent ต่อกันตามสายการผลิต: Form → **Intent Classifier** → (IF) → **Policy Validator** (มี Vector Store ตรวจนโยบาย) → **Finance Calculator** → **Mail Reviewer** → Output Parser → IF → ส่งอีเมล

- จุดดี: อ่านง่าย ตามได้ แก้จุดเดียวง่าย เหมาะกระบวนการที่ขั้นตอนแน่นอน
- จุดจำกัด: agent มากกว่า ~20 nodes/6+ agents เริ่มแน่น ไฟล์ยักษ์ ต่อ/แก้ยาก และไม่ยืดหยุ่นต่อเคสที่เส้นทางเปลี่ยน

## แบบ B: Orchestration (2026 Pattern)

Main Agent (Orchestrator) รับงานแล้ว **เรียก sub-workflows ผ่าน toolWorkflow (n8n 2.x)**: Intent Classifier, Policy Validator, Finance Calculator, QA Reviewer — แต่ละตัวเป็น workflow แยกไฟล์ (Sub-Agent เล็ก: Chat Manager + Code Node + Memory + Agent / Loop Code + Gatekeeper + IF + Nodes session | 120+ nodes | 10-12 nodes เหมาะกับสายงาน)

- จุดดี: ไฟล์เล็ก รักษาง่าย ส่งต่อทีมได้ ขยายเพิ่ม sub-agent ใหม่ได้โดยไม่แตะ main (แนวทางมาตรฐาน 2026)
- จุดพิจารณา: ต้องวางสัญญา input/output ระหว่าง workflow ให้ชัด (sub-agent มี Execute Workflow Trigger รับอินพุต และ Return เป็น output กลับ)

## ความต่างที่วัดได้จริง (ให้ผู้เรียนวัดเองจาก execution)

- รันเคสเดียวกันทั้งสองแบบ เก็บ **execution data**: จำนวนรอบ, เวลาต่อขั้น, tokens, และพฤติกรรมเมื่อนโยบายไม่ผ่าน (เคสที่นโยบายไม่ผ่าน แล้วเทียบพฤติกรรมสองแบบ) — เป้าหมายของหน่วย: อธิบายผลต่างได้ด้วยข้อมูล ไม่ใช่ความรู้สึก

## ลงมือทำ

เปิด [exercises/23-multi-agents/LAB.md](../../exercises/23-multi-agents/LAB.md) — import ทุกไฟล์จาก `solution/` (05A, 05B และ Sub 4 ตัว) รันเคสทดลองทั้งสองแบบ สร้างเคสที่นโยบายไม่ผ่าน แล้วเทียบพฤติกรรมจาก execution

## Check understanding

1. เคสไหนควรเลือก Linear — เคสไหนควร Orchestration เกณฑ์อะไร
2. toolWorkflow แก้ปัญหาไฟล์ยักษ์อย่างไร และต้องวางอะไรระหว่าง main กับ sub ให้ชัด
3. เวลา debug orchestration มอง execution ตรงไหนก่อน (main หรือ sub)

## Next

→ [exercises/23-multi-agents](../../exercises/23-multi-agents/README.md) — รันสองสถาปัตยกรรมแล้วอธิบายผลต่างด้วยข้อมูล
