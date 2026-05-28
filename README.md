# TOYOX Hose Selector

เครื่องมือเลือกสายยาง TOYOX ตามหลัก **STAMPED**  
พัฒนาโดย **บริษัท เอ็ม วาย เอ็ม เทรดดิ้ง จำกัด (MYM Trading Co., Ltd.)** — ผู้แทนจำหน่าย TOYOX อย่างเป็นทางการ · East Thailand · since 1980

🔗 **Live:** https://kolawat-sys.github.io/toyox-hose-selector/  
🌐 **Website:** [factools.com](https://factools.com/)

---

## คืออะไร

Web app ตัวเดียวจบ (single `index.html`) ที่ load `hose-database.json` 165 records แล้วช่วย:

- ลูกค้ากรอก spec ที่รู้ → ระบบ **scoring** ทุกสายในฐาน → จัดอันดับให้ใกล้สุดก่อน
- แสดง **gap report** ทุกตัว: บอกว่าตรง / เกิน (overkill) / ขาด (เสี่ยง) — sales เอาไปคุยกับลูกค้าได้ตรงไปตรงมา
- พิมพ์ PDF ผลลัพธ์ (A4) ได้ทันที พร้อม brand header/footer ของ MYM

## STAMPED weights

| Field | Weight | หมายเหตุ |
|-------|--------|---------|
| **S** Size | 35% | ขนาด ID (mm + หุน + นิ้ว) |
| **T** Temperature | 25% | °C ของของไหล (ค่าเดียว) |
| **P** Pressure | 25% | bar / kPa / MPa / psi (convert อัตโนมัติ) |
| **A** Application | 7.5% | ส่ง / ดูด / ดูด+ส่ง |
| **M** Material + media | 7.5% | family + tag ของไหล |
| **E** Ends | 0% | informative |
| **D** Delivery | 0% | informative (footer) |

## Bucket thresholds

- **ตรงตามต้องการ:** score ≥ 95
- **ใกล้เคียง:** 70 ≤ score < 95
- **ทางเลือก:** 0 < score < 70

---

## Files in this repo

| File | Purpose |
|------|---------|
| `index.html` | App ทั้งหมด (HTML + CSS + JS) |
| `hose-database.json` | ฐานข้อมูล 165 records |
| `mym-logo.png` | Logo MYM (475x474) ที่ header |
| `favicon.png` | Browser tab icon |
| `mym-line-qr.jpg` | LINE Official QR ที่ footer |
| `.nojekyll` | บอก GitHub Pages ห้าม run Jekyll |
| `README.md` | ไฟล์นี้ |
| `CHANGELOG.md` | ประวัติ version |

---

## Deploy update

1. แก้ไฟล์ใน repo → commit → GitHub Pages อัพเดทอัตโนมัติใน ~30 วินาที
2. Hard refresh browser (`Ctrl+Shift+R`) เพื่อ bypass cache

## เปลี่ยน logo

Replace `mym-logo.png` (transparent BG, อย่างน้อย 400x400px) — commit → reload

## เปลี่ยน LINE QR

Replace `mym-line-qr.jpg` (square aspect ratio recommend)

## เปลี่ยน weights / thresholds

แก้ใน `index.html`:

```js
const WEIGHTS = { size:35, temperature:25, pressure:25, application:7.5, material:7.5 };

// ใน applyScoring()
const perfect = scored.filter(x => x.total >= 95);  // ปรับเลขนี้
const near    = scored.filter(x => x.total >= 70 && x.total < 95);
```

---

## Debug (Browser DevTools — F12 → Console)

```js
window.__hoseApp.state.filters     // filter ปัจจุบัน
window.__hoseApp.applyScoring()    // ผล scoring ทั้งหมด
window.__hoseApp.scoreHose(hoseObj, filters)  // score 1 ตัว
window.__hoseApp.toBar(0.5, 'MPa') // unit converter
```

---

## License

© 2026 บริษัท เอ็ม วาย เอ็ม เทรดดิ้ง จำกัด · All rights reserved

เครื่องมือนี้พัฒนาโดย MYM Trading เพื่อใช้ภายในและกับลูกค้าของบริษัทเท่านั้น  
ห้ามทำซ้ำ ดัดแปลง หรือเผยแพร่โดยไม่ได้รับอนุญาตเป็นลายลักษณ์อักษร  
ข้อมูล TOYOX อ้างอิงจาก TOYOX Knowledge Base 2026-04-23 (Authorized Distributor right)
