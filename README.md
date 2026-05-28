# TOYOX Hose Selector

เครื่องมือเลือกสายยาง TOYOX ตามหลัก **STAMPED** สำหรับฝ่ายขายและลูกค้า

🔗 **Live:** _(ใส่ลิงค์ GitHub Pages ของคุณตรงนี้หลัง deploy)_

---

## คืออะไร

Web app ตัวเดียวจบ (single `index.html`) ที่ load `hose-database.json` 165 records แล้วช่วย:

- ลูกค้ากรอก spec ที่รู้ → ระบบ **scoring** ทุกสายในฐาน → จัดอันดับให้ใกล้สุดก่อน
- แสดง **gap report** ทุกตัว: บอกว่าตรง / เกิน (overkill) / ขาด (เสี่ยง) — sales เอาไปคุยกับลูกค้าได้ตรงไปตรงมา
- พิมพ์ PDF ผลลัพธ์ (A4) ได้ทันที

## STAMPED weights

| Field | Weight | หมายเหตุ |
|-------|--------|---------|
| **S** Size | 35% | ขนาด ID (mm) |
| **T** Temperature | 25% | ช่วง °C ใช้งาน |
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

## Deploy to GitHub Pages (5 นาที)

### ครั้งแรก

1. สร้าง repo ใหม่บน GitHub (เช่น `toyox-hose-selector`) — เลือก **Public**
2. Clone หรือ upload ไฟล์ทั้งหมดใน folder นี้:
   ```
   index.html
   hose-database.json
   .nojekyll
   .gitignore
   README.md
   ```
3. ไปที่ repo → **Settings** → **Pages**
4. ใต้ **Source** เลือก: `Deploy from a branch`
5. **Branch:** `main` · **Folder:** `/ (root)` → **Save**
6. รอ ~1-2 นาที — GitHub จะให้ URL หน้าตา `https://<username>.github.io/toyox-hose-selector/`

### อัพเดทฐานข้อมูล

แทนที่ `hose-database.json` แล้ว commit → push → GitHub Pages อัพเดทอัตโนมัติใน ~30 วินาที

### Custom domain (optional)

สร้างไฟล์ `CNAME` ที่ root ใส่ domain เช่น `hose.toyoxthai.com` แล้วตั้ง DNS CNAME ชี้ไปที่ `<username>.github.io`

---

## โครงสร้าง schema

`hose-database.json`:
```json
{
  "version": "2026-05-28",
  "last_updated": "2026-05-28",
  "source": "TOYOX Knowledge Base 2026-04-23 (165 hose models)",
  "price_date": "2025-05",
  "currency": "THB (VAT included)",
  "schema_version": "1.0",
  "hoses": [ ... ]
}
```

แต่ละ hose:
```json
{
  "code": "TR-15",
  "series": "TOYORON",
  "category": "สายทั่วไป",
  "size": { "nominal": "15", "id_mm": 15, "od_mm": 22 },
  "temperature": { "min_c": -5, "max_c": 60 },
  "application": {
    "flow_type": "ส่ง",
    "vacuum_capable": false,
    "media_tags": ["อเนกประสงค์"],
    "raw_label": "..."
  },
  "material": { "specific": "Soft PVC", "family": "PVC" },
  "pressure": {
    "at_23c": { "min": 0, "max": 10, "unit": "bar", "kind": "working" },
    "at_60c": { ... }
  },
  "ends": { "recommended": ["TC3-B", "TC6-B"], "fitting_family": "..." },
  "certifications": { "fda": false, "rohs2": true },
  "pricing": { "per_meter_thb": 145, "per_roll_thb": 7250, "roll_length_m": 50 },
  "notes": null
}
```

---

## เปลี่ยน weights / thresholds

แก้ใน `index.html`:

```js
const WEIGHTS = { size:35, temperature:25, pressure:25, application:7.5, material:7.5 };

// ใน applyScoring()
const perfect = scored.filter(x => x.total >= 95);  // ปรับเลขนี้
const near    = scored.filter(x => x.total >= 70 && x.total < 95);
```

## เปลี่ยนจำนวนตัวที่แสดงต่อ bucket

```js
const MAX_PER_BUCKET = { perfect: 50, near: 30, alt: 20 };
```

---

## Debug

เปิด DevTools (F12) → Console:

```js
window.__hoseApp.state.filters     // ดู filter ปัจจุบัน
window.__hoseApp.applyScoring()    // ดูผล scoring ทั้งหมด
window.__hoseApp.scoreHose(hoseObj, filters)  // score 1 ตัว
window.__hoseApp.toBar(0.5, 'MPa') // unit converter
```

---

## License

Internal use ของ TOYOX Thailand — ใช้ข้อมูลจาก TOYOX Knowledge Base 2026-04-23
