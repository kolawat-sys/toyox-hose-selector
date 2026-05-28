# Changelog

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
