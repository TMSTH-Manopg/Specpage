# 📘 API Specification  

## 🔹 Overview
เอกสารนี้เป็นการออกแบบ **API Specification (เชิงแนวคิด)** จากภาพ Architecture  
เพื่ออธิบาย flow การทำงานระหว่างระบบ:

- Premium API (Progress)
- SafeSmart API
- QMOD API


---

# 🧭 System Flow 

1. SmileyQuote → ส่งข้อมูล Campaign ไป Premium API  
2. SmileyQuote → ส่งข้อมูล Campaign ไป SafeSmart API  
3. SmileyQuote → ส่งข้อมูล Campaign ไป QMOD API  

---
# 🚀 API Endpoints
---

## 1) Publish Campaign → Premium
### 🧾 Description
ส่ง Campaign จาก SmileyQuote ไป Premium (Progress Service)

### ✅ Endpoint
- **Method**: `POST`
- **URL UAT**:   `http://tmwswbip17.tmith.net:8080/soap/wsdl?targetURI=urn:WSA-Safety:Smileyquote` 
- **URL PROD**:     
- **Content-Type**: `SOAP`


### 📥 Request (Conceptual)
```json
{
  "publishCampaignID": "458",
  "publishCampaignDate": "13/05/2026 16:49:45",
  "publishCampaignTime": null,
  "CampaignDetail": [
    {
      "CampaignKeyId": 458,
      "CompanyCode": "TMSTH",
      "CampaignCode": "TEST",
      "Polmst": "458-00000001",
      "Pack": "T",
      "Sclass": "110",
      "Covcod": "1",
      "Vehgrp": "3",
      "Vehuse": "1",
      "GarageCd": "G",
      "Makdes": "TOYOTA",
      "Moddes": "CAMRY",
      "CSTFlag": "C",
      "MinYear": 2,
      "MaxYear": 2,
      "MinCst": 0.0,
      "MaxCst": 2000.0,
      "MinSi": 1350000.0,
      "MaxSi": 1350000.0,
      "DriverName": "No",
      "DrivNo": "0",
      "DrivAge1": "0",
      "DrivAge2": "0",
      "Uom6U": "",
      "Cctv": "No",
      "Uom1V": 1000000.0,
      "Uom2V": 10000000.0,
      "Uom5V": 1000000.0,
      "Seats41": 7,
      "Mv411": 50000.0,
      "Mv412": 50000.0,
      "Mv413": 0.0,
      "Mv414": 0.0,
      "Mv42": 100000.0,
      "Mv43": 100000.0,
      "Dedod": 0.0,
      "AdDod": 0.0,
      "DedPd": 0.0,
      "FleetPer": "0.00",
      "Ncbyrs": "1.00",
      "NcbPer": "20.00",
      "DspcPer": "0.00",
      "LoadclmPer": "0.00",
      "Dstfper": "0.00",
      "Baseprm1": "7617.00",
      "MainPrem": "38891.00",
      "VehicleUsePrem": "0.00",
      "EnginePrem": "914.00",
      "DriverPrem": "427.00",
      "VehicleAgePrem": "0.00",
      "AccessoryPrem": "0.00",
      "SiPrem": "25708.00",
      "VehicleGroupPrem": "3467.00",
      "TpbiPersonPrem": "450.00",
      "TpbiAccPrem": "0.00",
      "TppdPersonPrem": "306.33",
      "Driver411Prem": "25.00",
      "Passenger412Prem": "150.00",
      "Driver413Prem": "0.00",
      "Passenger414Prem": "0.00",
      "MedicalExp42Prem": "2.00",
      "Bailbond43Prem": "10.00",
      "DeductODPrem": "0.00",
      "DeductADPrem": "0.00",
      "DeductPDPrem": "0.00",
      "FleetAmt": "0.00",
      "NcbAmt": "7842.00",
      "DspcAmt": "0.00",
      "LoadclmAmt": "0.00",
      "Dstfprm": "0.00",
      "Si22": 0.0,
      "Baseprm3": "0.00",
      "Prem3new": "0.00",
      "VehicleUse3Prem": "0.00",
      "Engine3Prem": "0.00",
      "Si3Prem": "0.00",
      "PrmTnew": "31369.33",
      "PremNetPd": "31369.33",
      "AdjustAll": "-2.67",
      "PrmGapnew": "126.00",
      "PrmStpnew": "2204.67",
      "PrmVatnew": "33700.00",
      "ShortRate": "No",
      "Day": 365,
      "NetInputGap": "0.00",
      "GrossInputGap": "0.00",
      "BehaviorLV": "",
      "BehaviorPercent": "",
      "WallChargeSI": "",
      "RateWallCharge": "",
      "NetPremiumWallCharge": "",
      "GrossPremiumWallCharge": "",
      "BatteryYear": "",
      "BatteryPrice": "",
      "BatterySI": "",
      "RateBattery": "",
      "NetPremiumBattery": "",
      "GrossPremiumBattery": "",
      "MinEVDrivNo": "0",
      "MaxEVDrivNo": "0",
      "DealerGarageRate": "0.01",
      "DealerGarageAmount": "135.00",
      "EffectivePeriod": "20240101",
      "ExpiredPeriod": "20261231",
      "CampaignName": "Example Campaign"
    }
    }
  ]
}
```

### 📘 Field Dictionary – Campaign Publish JSON
### 🔹 Overview
Field Dictionary นี้อธิบายโครงสร้าง JSON สำหรับ API:
> ✅ Publish Campaign → Premium / Integration Service

แบ่งเป็น 2 ระดับ:
1. **Header Level** (ข้อมูล Campaign โดยรวม)
2. **Detail Level (CampaignDetail)** (Rate รายแถว)

---

### 🧩 1) Header Level

| Field | Type | Description | Example |
|------|------|------------|--------|
| publishCampaignID | string | รหัส Campaign ที่ถูก publish | "458" |
| publishCampaignDate | string | วันที่ publish (dd/MM/yyyy HH:mm:ss) | "13/05/2026 16:49:45" |
| publishCampaignTime | string / null | เวลา publish (แยก field) | null |
| CampaignDetail | array | รายการทั้งหมดของ campaign | [...] |

---

### 🧮 2) CampaignDetail (Rate Row Level)

#### 🔹 General Info
| Field | Type | Description | Example |
|------|------|------------|--------|
| CampaignKeyId | integer | ID reference ของ campaign | 458 |
| CompanyCode | string | รหัสบริษัท | TMSTH |
| CampaignCode | string | รหัส campaign | TEST |
| CampaignName | string | ชื่อ campaign | Example Campaign |
| Polmst | string | Policy master code | 458-00000001 |
| Pack | string | Package code | T |
| Sclass | string | Vehicle class | 110 |
| Covcod | string | Coverage code | 1 |
| Vehgrp | string | Vehicle group | 3 |
| Vehuse | string | Vehicle usage | 1 |
| GarageCd | string | Garage type | G |
| Makdes | string | Brand | TOYOTA |
| Moddes | string | Model | CAMRY |
| CSTFlag | string | Type of CST (C=cc) | C |
| MinYear | integer | อายุรถต่ำสุด | 2 |
| MaxYear | integer | อายุรถสูงสุด | 2 |
| MinCst | number | CC ต่ำสุด | 0 |
| MaxCst | number | CC สูงสุด | 2000 |
| MinSi | number | ทุนประกันต่ำสุด | 1350000 |
| MaxSi | number | ทุนประกันสูงสุด | 1350000 |
| DriverName | string | มีระบุชื่อคนขับหรือไม่ | No |
| DrivNo | string | จำนวนคนขับ | 0 |
| DrivAge1 | string | อายุคนขับ 1 | 0 |
| DrivAge2 | string | อายุคนขับ 2 | 0 |
| Uom1V | number | TPBI ต่อคน |
| Uom2V | number | TPBI ต่อครั้ง |
| Uom5V | number | TPPD |
| Seats41 | integer | จำนวนที่นั่ง (PA) |
| Mv411 - Mv414 | number | PA coverage |
| Mv42 | number | Medical |
| Mv43 | number | Bail bond |
| Dedod | number | OD deductible |
| AdDod | number | Additional deductible |
| DedPd | number | PD deductible |
| FleetPer | number | Fleet (%) |
| Ncbyrs | number | NCB ปี |
| NcbPer | number | NCB (%) |
| DspcPer | number | Discount พิเศษ |
| LoadclmPer | number | Claim loading |
| Dstfper | number | Staff discount |
| Baseprm1 | number | Base premium |
| MainPrem | number | Premium หลัก |
| EnginePrem | number | Premium engine |
| DriverPrem | number | Premium driver |
| SiPrem | number | Premium จาก SI |
| VehicleGroupPrem | number | Premium group |
| TpbiPersonPrem | number | TPBI |
| TppdPersonPrem | number | TPPD |
| Passenger412Prem | number | Passenger |
| MedicalExp42Prem | number | Medical |
| Bailbond43Prem | number | Bail |
| FleetAmt | number | Fleet amount |
| NcbAmt | number | NCB amount |
| DspcAmt | number | Discount amount |
| PrmTnew | number | Net premium | 31369.33 |
| PremNetPd | number | Net PD | 31369.33 |
| AdjustAll | number | Adjustment | -2.67 |
| PrmStpnew | number | Stamp | 2204.67 |
| PrmVatnew | number | VAT | 33700 |
| PrmGapnew | number | Gross premium | 126 |
| ShortRate | string | Short rate flag |
| Day | integer | จำนวนวัน | 365 |
| BatteryYear | number | อายุ battery |
| BatteryPrice | number | ราคา battery |
| BatterySI | number | SI battery |
| DealerGarageRate | number | Rate dealer |
| DealerGarageAmount | number | Amount dealer |
| EffectivePeriod | string | YYYYMMDD |
| ExpiredPeriod | string | YYYYMMDD |

---
### 📊 Summary
- ✅ โครงสร้างแบบ **Header + Detail**
- ✅ รองรับ **Multi-rate per campaign**
- ✅ ครอบคลุม:
  - Vehicle
  - Driver
  - Coverage
  - Premium calculation แบบละเอียด
  - EV support
---

### 📘 API Response Specification – Publish Campaign (Premium)

### 🚀 API Information
API Response นี้คือผลลัพธ์ที่ระบบ Client (SmileyQuote) ส่งข้อมูล Campaign ไปยังระบบ **Premium (Progress Service)** ระบบจะตอบกลับทันที (Synchronous Response) เพื่อยืนยันว่า:

- ระบบรับข้อมูลเรียบร้อยแล้ว  
- เริ่มกระบวนการประมวลผล  
- สร้างไฟล์สำหรับใช้ในขั้นตอนถัดไป  

> หมายเหตุ: Response นี้ไม่ใช่ผลลัพธ์สุดท้ายของการประมวลผล

---

## 📥 Response Example

```json
{
  "publishCampaignID": "458",
  "DateRs": "20260513",
  "TimeRs": "16:49:55.303",
  "ErrorRs": "",
  "Status": "SUCCESS",
  "FileRef": "CampaignID_458_20260513164955.txt"
}
```
## 📘 Field Definition (Table)

| Field | Type | Format | Description | Example |
|------|------|--------|------------|--------|
| publishCampaignID | string | - | รหัส Campaign ที่ถูกส่ง | "458" |
| DateRs | string | YYYYMMDD | วันที่ระบบตอบกลับ | "20260513" |
| TimeRs | string | HH:mm:ss.SSS | เวลาที่ระบบตอบกลับ | "16:49:55.303" |
| ErrorRs | string | - | ข้อความ error จากระบบ ("" = ไม่มี error, มีข้อความ = เกิด error) | "" |
| Status | string | - | สถานะของ API (SUCCESS / FAILED) | "SUCCESS" |
| FileRef | string | - | ชื่อไฟล์ที่ระบบสร้าง ใช้สำหรับ process ต่อ | "CampaignID_458_20260513164955.txt" |

---

## 📊 Response Scenarios

### ✅ Success
```json
{
  "publishCampaignID": "458",
  "DateRs": "20260513",
  "TimeRs": "16:49:55.303",
  "ErrorRs": "",
  "Status": "SUCCESS",
  "FileRef": "CampaignID_458_20260513164955.txt"
}
```
### ❌ Failed
```json
{
  "publishCampaignID": "458",
  "DateRs": "20260513",
  "TimeRs": "16:49:55.303",
  "ErrorRs": "Cannot Connect Datebase Premium",
  "Status": "ERROR",
  "FileRef": ""
}
```

