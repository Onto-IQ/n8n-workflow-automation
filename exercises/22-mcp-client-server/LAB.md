# Exercise 21 — MCP Client & Server

## Goal
- ต่อ MCP สำเร็จทั้งสองฝั่ง

## Setup
1. เปิด n8n แล้วอยู่ที่หน้า Overview
2. ไฟล์เริ่มต้นอยู่ใน `starter/` (ถ้ามี); ไฟล์เฉลยอยู่ใน `solution/` — ห้ามเปิดก่อนลองเอง
1. Import ไฟล์ solution/04 - MCP Client.json และ 04 - MCP Server.json
2. server: ใส่ credentials Gmail/Calendar → Activate → จด webhook URL + path
3. client: ชี้ MCP Client ไป endpoint (ของห้องเรียนหรือของคุณเอง) → Execute
4. สั่ง "จองห้องประชุมพรุ่งนี้ บ่าย 2 และส่งอีเมลบอกทีม" แล้วดูว่า tool ไหนถูกเรียก

## Check your work
- agent เรียก tools ผ่าน MCP สำเร็จและรายงานผลครบ

## Stretch (optional)
- ['เชื่อม Claude Desktop เข้า server ของคุณผ่าน mcpServers config']
