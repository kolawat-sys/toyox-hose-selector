# Changelog

## V4 — 2026-08-19 (ราคา 2026 + ฐานข้อมูลใหม่)

### Changed — ฐานข้อมูล 165 → 349 records
- สร้างฐานข้อมูลใหม่จาก **TOYOX Price List ฉบับครบรอบ 20 ปี (2026)** ทั้งเล่ม แทนฉบับเดิมที่มาจาก knowledge base เมษายน
- เพิ่มซีรีส์ที่เดิมไม่มีในฐาน เช่น ECOFOODS PVC · CHILLER WATER HOSE · FLAMEBLC / FLAMEBLC HYBRID UL ·
  TOYOFUSSO SOFT SPRING · FUSSOTHERMO-S100C · TOYOSILICONE STEAM / THERMO / -S2 · TOYOTOP series ·
  HYBRID TOYODROP · TTT PVC LAY FLAT · สายลม PU / PE / PTFE · สายพ่นสี
- แยกรหัสสีเป็นรายการแยกตามใบราคา (เช่น HITRUN แดง/ฟ้า/เขียว) ให้ค้นและอ้างอิงตรงกับใบสั่งซื้อ
- รวมรายการสายคู่งานเชื่อม (TWR06) ที่เดิมนับซ้ำเป็น 2 รายการ ให้เหลือรายการเดียว

### Changed — ราคาอัปเดตเป็นปี 2026
- ราคาทั้งหมดอ้างอิง **TOYOX Standard Price 2026** (มีผล 4 มิ.ย. 2026) จากเดิมที่ยังเป็นราคาปี 2025
- 288 รายการราคาเปลี่ยน · 61 รายการเท่าเดิม

### Fixed — ป้ายสถานะ VAT (สำคัญ)
- footer เดิมเขียนว่า **"ราคารวม VAT"** ซึ่ง **ไม่ถูกต้อง** — ราคาในฐานข้อมูลไม่รวม VAT มาตลอด
- แก้เป็น **"ราคาตั้ง ไม่รวม VAT"** และเปลี่ยนให้ดึงข้อความจากไฟล์ฐานข้อมูลแทนการเขียนตายในหน้าเว็บ
  เพื่อไม่ให้ป้ายค้างเป็นข้อมูลเก่าอีกเมื่อฐานข้อมูลเปลี่ยน

### Added
- **ระบบเตือนเมื่อโหลดไฟล์ผิด** — ถ้าเผลอ deploy ไฟล์ฐานข้อมูลฉบับภายใน แอปจะขึ้นแถบแดงเตือนทันที
- รองรับโครงสร้างไฟล์ฐานข้อมูลทั้งแบบเดิมและแบบใหม่
- ราคาแสดงคั่นหลักพันด้วยจุลภาค (เช่น `฿1,025.75/m`) อ่านง่ายขึ้น

---

## V3 — 2026-05-28 (Branding)

### Added — MYM Trading branding
- **Header redesign:** logo MYM (สีม่วง กรอบเทา) + ชื่อบริษัทขนาดใหญ่ + subtitle "ผู้แทนจำหน่าย TOYOX · East Thailand · since 1980"
- **Color theme:** primary = ม่วง MYM (#6B46C1), accent = แดง TOYOX (#c8102e) สำหรับรหัสสายเท่านั้น
- **Footer ขยาย:** contact block (บริษัท / เว็บไซต์ / LINE) + LINE QR (คลิกเพื่อขยาย modal)
- **Copyright notice:** "© 2026 บริษัท เอ็ม วาย เอ็ม เทรดดิ้ง จำกัด · All rights reserved"
- **Browser tab:** Title "TOYOX Hose Selector | MYM Trading" + favicon + meta description + Open Graph
- **Print A4:**
- Header ทุกหน้า: "MYM Trading · TOYOX Hose Selector" (ซ้าย) + "factools.com" (ขวา)
- Footer ทุกหน้า: "© MYM Trading · หน้า X / Y"
- Watermark สีม่วงจางๆ กลางหน้า "MYM Trading"
- **New files:** `mym-logo.png` (475x474), `favicon.png` (64x64), `mym-line-qr.jpg` (540x540)

### Anti-rebrand protection
- HTML hardcode "MYM" / "เอ็ม วาย เอ็ม" ใน 8+ จุด
- Watermark print (ยากแก้ ต้องรู้ CSS)
- Copyright notice ที่ footer (ระบุห้ามทำซ้ำ)

---

## V2 — 2026-05-28

### Changed
- **Size dropdown:** เพิ่มหน่วยหุน + นิ้ว (mixed number) เช่น `25 mm · 8 หุน (1")`
- **Temperature input:** เปลี่ยนจาก range (min-max) → ค่าเดียว "อุณหภูมิของของไหล"
- **Temperature scoring:** in-range = ok / above hose.max = short (ร้อนเกิน) / below hose.min = short (เย็นเกิน)

---

## V1 — 2026-05-28

Initial release: STAMPED form + scoring + result cards + PDF print
