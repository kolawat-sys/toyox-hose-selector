# Changelog

## V2 — 2026-05-28

### Changed
- **Size dropdown:** เพิ่มหน่วย หุน + นิ้ว (mixed number format) ติดทุก option
  - เช่น `25 mm · 8 หุน (1")`, `38 mm · 12 หุน (1-1/2")`, `50 mm · 16 หุน (2")`
  - ขนาดที่ไม่ตรงหุนเป๊ะ แสดงประมาณ เช่น `8 mm · ≈2.5 หุน`
- **Temperature input:** เปลี่ยนจาก range (min-max) → ค่าเดียว "อุณหภูมิของของไหล"
  - ปกติลูกค้าบอกอุณหภูมิ material ที่ส่ง/ดูด เป็นค่าเดียว
  - ระบบเช็คว่า `hose.min ≤ user_temp ≤ hose.max`
- **Temperature scoring:**
  - In-range = ok (100)
  - In-range + margin ≥ 50°C = over (100, marked overkill)
  - Above hose.max = short (เสี่ยง, score ลด 3 pts/°C)
  - Below hose.min = short (สายอาจแข็ง/แตก)

### Notes
- Database schema ไม่เปลี่ยน — ไม่ต้องอัพเดท `hose-database.json`

---

## V1 — 2026-05-28

Initial release: STAMPED form + scoring + result cards + PDF print
