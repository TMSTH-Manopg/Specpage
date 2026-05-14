# 📘 สรุป API: Policy Parameter Setup Service - Campaigns API (v2.0.0)

## 🔹 ภาพรวม
API นี้ใช้สำหรับจัดการ **Campaign Rate Configuration** ของระบบประกันรถยนต์ (TMSTH) โดยรองรับการ:
- สร้าง/แก้ไข Campaign พร้อม rate ทั้งหมด
- ผูก Company Code กับ Campaign

---

## 🔐 Security
ต้องใช้ทั้ง 2 แบบ:
- **Bearer Token (JWT)**
- **Ocp-Apim-Subscription-Key**

---

## 🌐 Base URL
```
https://apis-dev.tokiomarinesafety.co.th/policy/parameter-setup/v1/api
```

---

# 🚀 Endpoints หลัก

## 1) PUT `/campaigns/{campaignId}`
### ✅ ใช้สำหรับ:
- สร้าง Campaign ใหม่
- หรือ Replace Campaign ทั้งหมด (Idempotent)

### 🧠 Behavior
- ต้องส่ง:
  - Metadata (campaignName, effectiveSchedule)
  - รายการ rate (`items`)
- ระบบจะ:
  - **ลบรายการเก่าที่ไม่ได้ส่งมา**
  - **แทนข้อมูลทั้งหมด (Full Replace)**

### 📌 Constraints
- สูงสุด: **10,000 rows ต่อ request**
- ต้องมี:
  - `campaignName`
  - `effectiveSchedule`
  - `items`

---

## 2) PUT `/campaigns/{campaignId}/company-codes`
### ✅ ใช้สำหรับ:
- Replace Company Code ทั้งหมดของ Campaign

### 🧠 Behavior
- Full replace เช่นกัน:
  - Code ที่ไม่ส่ง = ถูก unbind
  - ส่ง array ว่าง = clear ทั้งหมด

### ⚠️ Validation
- Company Code:
  - ต้องมีอยู่จริง
  - **ห้ามอยู่ใน Campaign อื่น**
- ถ้า conflict → `409 Conflict`

---

# 🧱 โครงสร้างข้อมูลหลัก

## 🧩 Campaign (Header)
| Field | Description |
|------|------------|
| campaignId | UUID ของ Campaign |
| campaignName | ชื่อ Campaign |
| description | คำอธิบาย |
| effectiveSchedule | วันที่เริ่ม-หมดอายุ |
| companies | Company ที่ bind |
| total | จำนวน rate rows |

---

## 🧮 CampaignRate (รายละเอียด Rate)
แบ่งเป็น 16 Section เช่น:
- Policy
- Vehicle
- Range
- Driver
- Coverage
- Deductible
- Discount
- Premium
- EV fields (Battery, Charger)

---

# ❌ Error Handling

## Standard Format
```json
{
  "code": "E400",
  "message": "Invalid input data",
  "details": [],
  "timestamp": "2025-11-26T05:04:21Z",
  "traceId": "uuid"
}
```

---

# 📊 สรุป
API นี้เป็นแบบ:
- Full Replace (PUT)
- แยก Campaign กับ Company Binding ชัดเจน
- รองรับข้อมูล Rate ขนาดใหญ่ (สูงสุด 10,000 rows)
- รองรับ Motor + EV Insurance
