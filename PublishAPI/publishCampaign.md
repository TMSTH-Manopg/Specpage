# 📘 API Specification  

## 🔹 Overview
เอกสารนี้เป็นการออกแบบ **API Specification ** จากภาพ 
เพื่ออธิบาย flow การทำงานระหว่างระบบ  SmileyQuote Publish Campaign Service
- Premium API 
- QMOD API 

---

# 🧭 System Flow 

1. SmileyQuote → ส่งข้อมูล Campaign ไป Premium API   
2. SmileyQuote → ส่งข้อมูล Campaign ไป QMOD API  

---
# 🚀 API Endpoints
---
# 1) Publish Campaign → Premium
### 🧾 Description
ส่ง Campaign จาก SmileyQuote ไป Premium (Progress Service)
### ✅ Endpoint
- **Method**: `POST`
- **URL UAT**:   `http://tmwswbip17.tmith.net:8080/soap/wsdl?targetURI=urn:WSA-Safety:Smileyquote` 
   
- **Content-Type**: `SOAP`


### 📥 Request (Conceptual)
```json
{
  "publishCampaignID": "458",
  "publishCampaignDate": "04/06/2026 10:16:22",
  "publishCampaignTime": null,
  "EffectivePeriod": "2024-08-01T00:00:00",
  "ExpiredPeriod": "2024-12-31T00:00:00",
  "CampaignName": "HYUNDAI : First year renew",
  "CampaignDetail": [
    {
      "CampaignKeyId": 458,
      "CompanyCode": "TMSTH",
      "CampaignCode": "C67/00308",
      "Polmst": "458-00000001",
      "Pack": "T",
      "Sclass": "110",
      "Covcod": "1",
      "Vehgrp": "3",
      "Vehuse": null,
      "GarageCd": "G",
      "Makdes": "HYUNDAI",
      "Moddes": "ELANTRA",
      "CSTFlag": "C",
      "MinYear": 2,
      "MaxYear": 2,
      "MinCst": 0,
      "MaxCst": 2000,
      "MinSi": 1950000,
      "MaxSi": 1950000,
      "DriverName": "No",
      "DrivNo": "0",
      "DrivAge1": "0",
      "DrivAge2": "0",
      "Uom6U": "",
      "Cctv": "No",
      "Uom1V": 1000000,
      "Uom2V": 10000000,
      "Uom5V": 5000000,
      "Seats41": 7,
      "Mv411": 200000,
      "Mv412": 200000,
      "Mv413": 0,
      "Mv414": 0,
      "Mv42": 200000,
      "Mv43": 200000,
      "Dedod": 0,
      "AdDod": 0,
      "DedPd": 0,
      "FleetPer": "0.00",
      "Ncbyrs": "0.00",
      "NcbPer": "0.00",
      "DspcPer": "0.00",
      "LoadclmPer": "0.00",
      "Dstfper": "0.00",
      "Baseprm1": "7671.00",
      "MainPrem": "51082.00",
      "VehicleUsePrem": "0.00",
      "EnginePrem": "921.00",
      "DriverPrem": "430.00",
      "VehicleAgePrem": "0.00",
      "AccessoryPrem": "0.00",
      "SiPrem": "36175.00",
      "VehicleGroupPrem": "4520.00",
      "TpbiPersonPrem": "587.00",
      "TpbiAccPrem": "0.00",
      "TppdPersonPrem": "779.00",
      "Driver411Prem": "100.00",
      "Passenger412Prem": "600.00",
      "Driver413Prem": "0.00",
      "Passenger414Prem": "0.00",
      "MedicalExp42Prem": "2.00",
      "Bailbond43Prem": "20.00",
      "DeductODPrem": "0.00",
      "DeductADPrem": "0.00",
      "DeductPDPrem": "0.00",
      "FleetAmt": "0.00",
      "NcbAmt": "0.00",
      "DspcAmt": "0.00",
      "LoadclmAmt": "0.00",
      "Dstfprm": "0.00",
      "Si22": 0,
      "Baseprm3": "0.00",
      "Prem3new": "0.00",
      "VehicleUse3Prem": "0.00",
      "Engine3Prem": "0.00",
      "Si3Prem": "0.00",
      "PrmTnew": "52000.00",
      "PremNetPd": "52000.00",
      "AdjustAll": "-1.00",
      "PrmGapnew": "208.00",
      "PrmStpnew": "3654.56",
      "PrmVatnew": "55862.56",
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
      "DealerGarageAmount": "195.00"
       
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
--- 


# 2) PREMIUM API → SafeSmart API

## 🔹 Flow Name
** Premium Database Campaign → ส่งข้อมูล Campaign ไป SafeSmart API**

### 🧾 Description
เมื่อระบบ **SmileyQuote** ทำการ Publish Campaign ไปยัง Premium 
ระบบ Premium จะทำการ Process ส่งข้อมูล Campaign (รายละเอียด rate ทั้งหมด) ไปยัง  
**SafeSmart API** เพื่อ:
- ✅ บันทึกข้อมูล Campaign  
- ✅ อัปเดตข้อมูลในระบบ SafeSmart  
- ✅ ใช้เป็นข้อมูลสำหรับคำนวณหรือแสดงผลในระบบปลายทาง  

### ✅ Endpoint
- **Method**: `POST`
- **URL UAT**:   `http://10.35.99.161/API_Motor/SetMotorCampiagnDetail` 
 
---

## 📥 Request Description
- ใช้ส่งข้อมูล Campaign Detail
- มี structure เป็น array (`campaigndetail`)
- รองรับหลายรายการ (Multiple Rate Rows)

---
### 📥 Request (Conceptual)
```json
{
  "campaigndetail": [
    {
      "si31": "135.00",
      "AttachTextTha": "",
      "VehicleWeight": 0.0,
      "CCTVFlag": "No",
      "ComPersi": "",
      "AccessoryFlag": "",
      "ClaimPrem": 0.00,
      "FleetPrem": 0.00,
      "PATempDriv": "0",
      "MaxSumIns": 1350000.0,
      "MedicalExp": "2.00",
      "chargvat": "",
      "PromotionCode": "",
      "chargstp": "",
      "levcod": "",
      "rate31": "0.01",
      "VehicleSize": 0,
      "BailBond": "10.00",
      "CampaignCode": "TEST",
      "VehicleSeat": 7,
      "PALifeDriv": "50000",
      "ComAccsi": "",
      "AccessorySumIns": 0.0,
      "VehicleBody": "",
      "PlanNumber": "",
      "DriverAge1Max": 0,
      "TotDiscPrem": 0.00,
      "battflg": "",
      "charflg": "",
      "PackCode": "T",
      "OtherText": "",
      "PlanName": "",
      "battnetprm": "",
      "VehicleMaxCST": 2000.0,
      "PATempPass": "0",
      "CoverTypeCode": "1",
      "NetPrem": 38891.00,
      "watts": "",
      "MinSumIns": 1350000.0,
      "SubBusClass": "110",
      "NcbPrem": 7842.00,
      "DriverAge2Max": 0,
      "battsi": "",
      "PALifePass": "50000",
      "DriverAge2Min": 0,
      "Stamp": 126.00,
      "battnum": "",
      "VehicleDoorNumber": "",
      "gapprm31": "126.00",
      "chargnetprm": "",
      "DiscPrem": 0.00,
      "pdprm31": "135.00",
      "VehicleUseTha": "ใช้ส่วนบุคคล ไม่ใช้รับจ้างหรือให้เช่า",
      "chargtot": "",
      "VehicleGarage": "G",
      "charggrossprm": "",
      "TPpdacc": "1000000",
      "TPbiacc": "10000000",
      "DriverNumber": 0,
      "SumInsFt": "",
      "ExpiryDate": "20261231",
      "battprice": "",
      "Seat411": "",
      "DedPrem": 0.00,
      "Tax": 2204.67,
      "SumInsOd": "",
      "AddPrem": 0.0,
      "battvat": "",
      "chargnum": "",
      "battyr": "",
      "battstp": "",
      "PromotionName": "",
      "AttachTextEng": "",
      "Seat414": "",
      "Seat413": "",
      "Seat412": "",
      "DriverType": "",
      "GrossPrem": 0.0,
      "battrate": "",
      "chargrate": "",
      "VehicleGroup": "3",
      "VehicleModel": "CAMRY",
      "VehicleMinCST": 0.0,
      "Premium3": 427.00,
      "Premium2": 0.00,
      "Premium1": 38891.00,
      "batttot": "",
      "maksi": "",
      "PolicyMaster": "458-00000001",
      "CampaignName": "Example Campaign",
      "DriverAge1Min": 0,
      "VehicleUseCode": "1",
      "DeductPd": "0.00",
      "battgrossprm": "",
      "PlanCode": "",
      "TPbips": "1000000",
      "chargsi": "",
      "VehicleBrand": "TOYOTA",
      "DayCover": "365",
      "DeductOd": "0.00",
      "levper": "",
      "VehicleAge": 0,
      "fgtariff": "",
      "VehicleUseEng": "For personal use not for rent or let on hire",
      "EffectiveDate": "20240101",
      "battper": ""
    }
  ]
}
```

### 📥 Response Example
```json
{
  "Status": "SUCCESS",
  "Message": "บันทึกข้อมูลสำเร็จ(14/14)",
  "ErrorList": []
}
```

---
# 3) Publish Campaign → QMOD API  

## Overview
Policy Parameter Setup Service - QMOD Campaigns API
REST API สำหรับจัดการข้อมูล Campaign Rate Configuration ของระบบประกันภัยรถยนต์ TMSTH

รองรับ:

- Create / Update Campaign
- Import Campaign Rate แบบ Asynchronous
- ตรวจสอบสถานะ Import
- จัดการ Company Codes ที่ผูกกับ Campaign

---

## Authentication

ทุก Endpoint ต้องผ่านการ Authentication

Response กรณีไม่ได้รับอนุญาต:

```json
{
  "code": "E401",
  "message": "Unauthorized access - invalid or missing authentication credentials",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

---

## Endpoints

### 1. Create or Replace Campaign

#### PUT `/campaigns/{campaignId}`

สร้าง Campaign ใหม่ หรือแทนที่ Campaign เดิมทั้งหมด โดยเป็นการทำงานแบบ Idempotent

#### Behavior

- เป็น Async Process
- Response กลับด้วย HTTP `202 Accepted`
- คืนค่า `jobId` สำหรับติดตามสถานะ
- ผู้เรียกต้องส่ง Rate Rows ทั้งชุด
- ระบบประมวลผลข้อมูลตามกฎดังนี้

| กรณี | ผลลัพธ์ |
|---|---|
| `campaignCode + polMst` ตรงกับข้อมูลเดิม | Update |
| ไม่พบข้อมูลเดิม | Insert |
| มีข้อมูลเดิมแต่ไม่ถูกส่งมาใน Request | Delete |
| Request มี `campaignCode + polMst` ซ้ำ | ใช้ Record แรก |

#### Transaction Rule

Campaign, Rate Rows และ Company Codes จะถูกบันทึกภายใต้ Transaction เดียวกัน

หาก Import ล้มเหลว:

- Rollback การเปลี่ยนแปลงทั้งหมด
- ไม่มีข้อมูลบางส่วนถูกบันทึก

#### Path Parameter

| Name | Type | Required | Description |
|---|---|---|---|
| `campaignId` | UUID | Yes | Campaign identifier ที่ Client เป็นผู้กำหนด แนะนำ UUID v4 |

ตัวอย่าง:

```text
a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

#### Request Body

```json
{
  "campaignName": "Full Main Agent Motor Type 2",
  "description": "แคมเปญสำหรับตัวแทนหลัก ประเภท 2",
  "effectiveSchedule": {
    "effectiveDate": "2024-01-01",
    "expiryDate": "2024-12-31"
  },
  "companyCodes": [
    "570",
    "TMSTH"
  ],
  "items": [
    {
      "campaignCode": "C68/00050-2+",
      "polMst": "530-00000001"
    }
  ]
}
```

#### Company Codes Behavior

- หากส่ง `companyCodes` ระบบจะแทนที่ Company Codes เดิมทั้งหมดภายใน Import เดียวกัน
- หากไม่ส่ง หรือส่งเป็น `null` ระบบจะคง Company Codes เดิมไว้
- หากส่งเป็น Array ว่าง หรือมี Code ว่าง ระบบตอบ `400 Bad Request`

#### Validation

##### HTTP 400 Bad Request

เกิดขึ้นเมื่อ:

- Request Body ไม่ถูกต้อง
- `campaignName` ไม่มีค่า
- `effectiveSchedule` ไม่มีค่า
- `items` ว่าง หรือไม่มีอย่างน้อย 1 Record
- `companyCodes` ถูกส่งเป็น `[]`
- `companyCodes` มีค่าว่าง

##### HTTP 409 Conflict

เกิดขึ้นเมื่อ Company Code อย่างน้อยหนึ่งรายการไม่มีใน Partner Companies

- Response จะแสดง Company Code ที่ไม่พบทั้งหมด
- ระบบจะไม่เริ่ม Import
- ไม่มีข้อมูลถูกเปลี่ยนแปลง

#### Success Response

##### HTTP 202 Accepted

```json
{
  "jobId": "3f2c9a8e-1b7d-4c55-9e0a-6d2f4b8c1a90",
  "status": "Success",
  "rowCount": 1213
}
```

> `status: Success` หมายถึง Request ถูกยอมรับเข้าสู่กระบวนการ Import แล้ว ไม่ได้หมายความว่า Import เสร็จสมบูรณ์ ผู้เรียกต้องตรวจสอบผลผ่าน Status API

#### Response Header

| Header | Description |
|---|---|
| `Location` | URL ของ `GET /campaigns/{campaignId}/imports/{jobId}` สำหรับตรวจสอบสถานะ Import |

---

### 2. Get Import Status

#### GET `/campaigns/{campaignId}/imports/{jobId}`

ตรวจสอบสถานะการ Import Campaign ที่เริ่มจาก `PUT /campaigns/{campaignId}`

#### Path Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `campaignId` | UUID | Yes | Campaign identifier |
| `jobId` | UUID | Yes | Job identifier ที่ได้รับจาก Create or Replace Campaign API |

#### Status Values

| Status | Description |
|---|---|
| `Queued` | Request ถูกยอมรับและกำลังรอประมวลผล |
| `Processing` | กำลังประมวลผล |
| `Succeeded` | Campaign, Rate Rows และ Company Bindings ถูกบันทึกสำเร็จ |
| `Failed` | Import ล้มเหลวและไม่มีข้อมูลถูกเปลี่ยนแปลง ให้ตรวจสอบ `error` |

Infrastructure Failure จะถูก Retry อัตโนมัติ และสถานะอาจกลับไปเป็น `Processing`

#### Success Response

##### HTTP 200 OK

```json
{
  "jobId": "3f2c9a8e-1b7d-4c55-9e0a-6d2f4b8c1a90",
  "campaignId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "status": "Succeeded",
  "rowCount": 1213,
  "error": null,
  "createdAt": "2026-11-07T05:04:21.220Z",
  "updatedAt": "2026-11-07T05:04:29.410Z"
}
```

#### Error Responses

##### HTTP 401 Unauthorized

Authentication ไม่ถูกต้องหรือไม่มี Credentials

##### HTTP 404 Not Found

เกิดขึ้นเมื่อ:

- ไม่พบ `jobId`
- `jobId` ไม่ได้อยู่ภายใต้ `campaignId` ที่ระบุ

```json
{
  "code": "E404",
  "message": "Data not found",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

---

### 3. Replace Campaign Company Codes

#### PUT `/campaigns/{campaignId}/company-codes`

แทนที่รายการ Company Codes ทั้งหมดที่ผูกกับ Campaign โดยเป็นการทำงานแบบ Idempotent

#### Rules

- Company Code ที่อยู่ใน Request จะถูก Bind กับ Campaign
- Company Code ที่เคย Bind แต่ไม่อยู่ใน Request จะถูก Unbind
- Company หนึ่งรายการสามารถผูกกับ Campaign ได้หลาย Campaign
- Duplicate Codes จะถูก Ignore โดยเปรียบเทียบแบบ Case Insensitive
- การเปลี่ยนแปลงเป็นแบบ All-or-Nothing

#### Path Parameter

| Name | Type | Required | Description |
|---|---|---|---|
| `campaignId` | UUID | Yes | Campaign identifier |

#### Request Body

```json
{
  "companyCodes": [
    "570",
    "TMSTH"
  ]
}
```

#### Validation

| HTTP Status | Condition |
|---|---|
| `400 Bad Request` | `companyCodes` ไม่มีอย่างน้อย 1 Code ที่ไม่เป็นค่าว่าง |
| `401 Unauthorized` | Authentication ไม่ถูกต้องหรือไม่มี Credentials |
| `404 Not Found` | ไม่พบ Campaign |
| `409 Conflict` | พบ Company Code ที่ไม่มีใน Partner Companies |

กรณี `409 Conflict` ระบบจะแสดง Code ที่ไม่พบทั้งหมด และจะไม่เปลี่ยน Binding ใด ๆ

#### Success Response

##### HTTP 200 OK

```json
{
  "code": "S200",
  "message": "Company codes retrieved successfully.",
  "data": {
    "campaignId": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "companies": [
      {
        "id": "550e8400-e29b-41d4-a716-446655440001",
        "partnerCompanyCode": "570",
        "companyName": "Tokio Marine Insurance"
      }
    ]
  }
}
```

---

## Standard Error Model

```json
{
  "code": "E400",
  "message": "Invalid input data",
  "details": [
    {
      "field": "ErrorField",
      "message": "ErrorMessage"
    }
  ],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

### Conflict Response Example

```json
{
  "code": "E409",
  "message": "Company codes 9999, 8888 do not exist in the system.",
  "details": [
    {
      "field": "companyCodes",
      "message": "Company code 9999 does not exist in the system."
    },
    {
      "field": "companyCodes",
      "message": "Company code 8888 does not exist in the system."
    }
  ],
  "timestamp": "2026-11-07T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

---

## Technical Constraints

| Item | Value |
|---|---|
| Request Body Size | สูงสุด 64 MB |
| Tested Import Size | ประมาณ 13,000 Rate Rows ต่อ Request |
| `campaignName` | Required |
| `effectiveSchedule` | Required |
| `items` | ต้องมีอย่างน้อย 1 Record |
| `campaignId` | Client-generated UUID แนะนำ UUID v4 |
| Import Concurrency | Import ทำงานครั้งละ 1 Job |

```

