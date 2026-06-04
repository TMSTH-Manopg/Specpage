# 📘 API Specification  

## 🔹 Overview
เอกสารนี้เป็นการออกแบบ **API Specification (เชิงแนวคิด)** จากภาพ Architecture  
เพื่ออธิบาย flow การทำงานระหว่างระบบ:

- SmileyQuote Publish Campaign Service
- Premium API (Progress)
- SafeSmart API
- QMOD API
- Webhook Callback

---

# 🧭 System Flow 

1. SmileyQuote → ส่งข้อมูล Campaign ไป Premium API  
2. SmileyQuote → ส่งข้อมูล Campaign ไป SafeSmart API  
3. SmileyQuote → ส่งข้อมูล Campaign ไป QMOD API  

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
--- 


# 2) Publish Campaign → SafeSmart API

## 🔹 Flow Name
**SmileyQuote Publish Campaign → ส่งข้อมูล Campaign ไป SafeSmart API**

### 🧾 Description
เมื่อระบบ **SmileyQuote** ทำการ Publish Campaign  
ระบบจะส่งข้อมูล Campaign (รายละเอียด rate ทั้งหมด) ไปยัง  
**SafeSmart API** เพื่อ:
- ✅ บันทึกข้อมูล Campaign  
- ✅ อัปเดตข้อมูลในระบบ SafeSmart  
- ✅ ใช้เป็นข้อมูลสำหรับคำนวณหรือแสดงผลในระบบปลายทาง  

### ✅ Endpoint
- **Method**: `POST`
- **URL UAT**:   `http://10.35.99.161/API_Motor/SetMotorCampiagnDetail` 

- **Content-Type**: `SOAP`
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

## 🔹 Flow Name
**SmileyQuote Publish Campaign → ส่งข้อมูล Campaign ไป QMOD API**

---

### 3.1) Publish Campaign Detail QMOD API 

#### 🧾 Description
REST API สำหรับจัดการการตั้งค่าอัตราแคมเปญ (Campaign rate configurations) สำหรับระบบประกันภัยรถยนต์ TMSTH (TMSTH motor insurance system) โดยบริการนี้จะรองรับการจัดการข้อมูลแคมเปญในส่วนของ Commercial การอัปเดตข้อมูลแบบ Upsert (PUT) รวมถึงการผูกข้อมูลรหัสบริษัท (Company-code binding)

**Base URL (Development):**
`https://apis-dev.tokiomarinesafety.co.th/policy/parameter-setup/v1/api`

---

#### ✅ Endpoint

##### 1. Create or replace a campaign
*   **Method:** `PUT`
*   **Path:** `/campaigns/{campaignId}`
*   **Description:** สร้างแคมเปญใหม่ด้วย `campaignId` ที่กำหนด หรือแทนที่แคมเปญเดิมที่มีอยู่แล้ว (Idempotent)

##### 2. Replace company codes bound to a campaign
*   **Method:** `PUT`
*   **Path:** `/campaigns/{campaignId}/company-codes`
*   **Description:** แทนที่ชุดข้อมูลรหัสบริษัททั้งหมดที่ผูกไว้กับแคมเปญ

---

#### 📥 Request Description

คำอธิบายสำหรับการใช้งาน Endpoint: **`PUT /campaigns/{campaignId}`**

##### Semantics (หลักการทำงาน)
*   **ส่งข้อมูลทั้งหมด:** ต้องส่งข้อมูล Metadata ของแคมเปญแบบครบถ้วน พร้อมกับอาร์เรย์ของข้อมูลแถวอัตราเบี้ยประกัน (Rate rows) ทั้งหมดในส่วนของ Body
*   **ลบข้อมูลเก่า:** แถวอัตราเบี้ยประกันเดิมที่ไม่ได้ระบุมาใน Request body จะถูกลบออกทั้งหมด (เป็นการแทนที่แบบสมบูรณ์ หรือ Full replace)
*   **การกำหนด ID:** ลูกค้า (Client) จะต้องเป็นผู้ระบุค่า `campaignId` ส่งมาเอง โดยแนะนำให้ใช้รูปแบบ UUID v4

##### Constraints (ข้อจำกัดและเงื่อนไข)
*   **จำกัดจำนวนแถว:** กำหนดให้มีแถวอัตราเบี้ยประกัน (Rate rows) ได้สูงสุดไม่เกิน **10,000 แถว** ต่อหนึ่ง Request
*   **ฟิลด์ที่จำเป็น (Required):** ข้อมูลในส่วนของ `Metadata` (ประกอบด้วย `campaignName`, `effectiveSchedule`) และอาร์เรย์ของ `items` จำเป็นต้องระบุส่งมาด้วยเสมอ

##### 🔑 Parameters

###### Path Parameters
*   **`campaignId`** `string($uuid)` (*required*)
    *   **Description:** ตัวระบุแคมเปญเฉพาะ (Campaign identifier) ในรูปแบบ UUIDv4 ที่ถูกสร้างขึ้นและส่งมาจากฝั่ง Client 
    *   **Example:** `a1b2c3d4-e5f6-7890-abcd-ef1234567890`

---

##### 📥 Request Body (application/json)

ข้อมูล JSON Payload ตัวอย่างสำหรับอัปเดตและตั้งค่าแคมเปญ:

```json
{
  "campaignName": "Full Main Agent Motor Type 2",
  "description": "แคมเปญสำหรับตัวแทนหลัก ประเภท 2",
  "effectiveSchedule": {
    "effectiveDate": "2024-01-01",
    "expiryDate": "2024-12-31"
  },
  "items": [
    {
      "campaignCode": "C68/00050-2+",
      "polMst": "530-00000001",
      "pack": "T",
      "sClass": "320",
      "covCod": "2.2",
      "vehGrp": "01",
      "vehUse": "1",
      "garageCd": "TMSTH",
      "makDes": "FORD",
      "modDes": "RANGER",
      "cstFlag": "C",
      "minCst": 0,
      "maxCst": 3000,
      "minYear": 20,
      "maxYear": 20,
      "minSi": 50000,
      "maxSi": 50000,
      "driverName": "No",
      "drivNo": 0,
      "drivAge1": 0,
      "drivAge2": 0,
      "uom6U": "A",
      "cctv": "No",
      "uom1V": 500000,
      "uom2V": 10000000,
      "uom5V": 1000000,
      "seats41": 3,
      "mv411": 100000,
      "mv412": 100000,
      "mv413": 0,
      "mv414": 0,
      "mv42": 100000,
      "mv43": 200000,
      "dedOd": 0,
      "adDod": 0,
      "dedPd": 0,
      "fleetPer": 0,
      "ncbYrs": 0,
      "ncbPer": 50,
      "dspcPer": 36,
      "loadclmPer": 0,
      "dstfPer": 0,
      "basePrm1": 7721,
      "mainPrem": 7235,
      "vehicleUsePrem": 0,
      "enginePrem": -849,
      "driverPrem": 0,
      "vehicleAgePrem": 0,
      "accessoryPrem": 0,
      "siPrem": 0,
      "vehicleGroupPrem": 0,
      "tpbiPersonPrem": 363.39,
      "tpbiAccPrem": 50,
      "tppdPersonPrem": 100,
      "driver411Prem": 0,
      "passenger412Prem": 0,
      "driver413Prem": 1,
      "passenger414Prem": 20,
      "medicalExp42Prem": 0,
      "bailBond43Prem": 0,
      "deductOdPrem": 0,
      "deductAdPrem": 0,
      "deductPdPrem": 0,
      "fleetAmt": 3703,
      "ncbAmt": 1333,
      "dspcAmt": 0,
      "loadclmAmt": 0,
      "dstfPrm": 0,
      "si22": 50000,
      "basePrm3": 3400,
      "prem3New": 3400,
      "vehicleUse3Prem": 0,
      "engine3Prem": 0,
      "si3Prem": 0,
      "prmTNew": 5770.39,
      "premNetPd": 5770.39,
      "adjustAll": -0.61,
      "prmStpNew": 24,
      "prmVatNew": 405.61,
      "prmGapNew": 6200,
      "shortRate": "No",
      "day": 365,
      "netInputGap": 0,
      "grossInputGap": 0,
      "behaviorLv": "A",
      "behaviorPercent": 100,
      "wallChargeSi": 0,
      "rateWallCharge": 0,
      "netPremiumWallCharge": 0,
      "grossPremiumWallCharge": 0,
      "batteryYear": 0,
      "batteryPrice": 0,
      "batterySi": 0,
      "rateBattery": 0,
      "netPremiumBattery": 0,
      "grossPremiumBattery": 0,
      "minEvDrivNo": 0,
      "maxEvDrivNo": 0,
      "dealerGarageRate": 0,
      "dealerGarageAmount": 0
    }
  ]
}
```
##### 📤 Response Description

ระบบจะส่งผลลัพธ์กลับมาในรูปแบบ `application/json` โดยมีรายละเอียดรหัสสถานะ (HTTP Status Code) ดังนี้:

###### 1. HTTP 200: Campaign updated (existed before)
*   **Description:** อัปเดตข้อมูลแคมเปญสำเร็จ (กรณีมีข้อมูลแคมเปญนี้อยู่ในระบบเดิมอยู่แล้ว)
*   **Response Body Example:**
```json
{
  "code": "S200",
  "message": "Campaign retrieved successfully.",
  "data": {
    "campaignId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "companies": [
      {
        "id": "550e8400-e29b-41d4-a716-446655440001",
        "partnerCompanyCode": "570",
        "companyName": "Tokio Marine Insurance"
      }
    ],
    "campaignName": "Full Main Agent Motor Type 2",
    "description": "แคมเปญสำหรับตัวแทนหลัก ประเภท 2",
    "effectiveSchedule": {
      "effectiveDate": "2024-01-01",
      "expiryDate": "2024-12-31"
    },
    "total": 1213
  }
}
```

###### 2. HTTP 201: Campaign created (new)
*   **Description:** สร้างแคมเปญใหม่ในระบบสำเร็จ
*   **Response Body Example:**
```json
{
  "code": "S200",
  "message": "Campaign retrieved successfully.",
  "data": {
    "campaignId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "companies": [
      {
        "id": "550e8400-e29b-41d4-a716-446655440001",
        "partnerCompanyCode": "570",
        "companyName": "Tokio Marine Insurance"
      }
    ],
    "campaignName": "Full Main Agent Motor Type 2",
    "description": "แคมเปญสำหรับตัวแทนหลัก ประเภท 2",
    "effectiveSchedule": {
      "effectiveDate": "2024-01-01",
      "expiryDate": "2024-12-31"
    },
    "total": 1213
  }
}
```
###### 3. HTTP 400: Bad request - Invalid input
*   **Description:** คำขอไม่ถูกต้องเนื่องจากข้อมูลนำเข้า (Input data) ไม่ผ่านการตรวจสอบเงื่อนไข
*   **Response Body Example:**
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

###### 4. HTTP 401: Unauthorized - Authentication required
*   **Description:** การเข้าถึงถูกปฏิเสธเนื่องจากไม่มีข้อมูลการยืนยันตัวตน หรือข้อมูลยืนยันตัวตนไม่ถูกต้อง
*   **Response Body Example:**
```json
{
  "code": "E401",
  "message": "Unauthorized access - invalid or missing authentication credentials",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

###### 5. HTTP 500: Internal server error
*   **Description:** เกิดข้อผิดพลาดภายในระบบของเซิร์ฟเวอร์
*   **Response Body Example:**
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
### 3.2) Publish Campaign Company QMOD 

#### 🧾 Description
REST API สำหรับแทนที่ชุดข้อมูลรหัสบริษัททั้งหมดที่ผูกไว้กับแคมเปญ (Idempotent) โดยรหัสบริษัทที่ส่งมาใน Request Body จะถูกผูกเข้ากับแคมเปญ (Bound) ส่วนรหัสบริษัทเดิมที่เคยผูกไว้แต่ไม่ได้ระบุมาในคำขอครั้งนี้จะถูกยกเลิกการผูกออกไป (Unbound)

---

#### ✅ Endpoint
*   **Method:** `PUT`
*   **Path:** `/campaigns/{campaignId}/company-codes`
*   **Description:** แทนที่ชุดข้อมูลรหัสบริษัททั้งหมดที่ผูกไว้กับแคมเปญ

---

#### 📥 Request Description

คำอธิบายสำหรับการใช้งาน Endpoint: **`PUT /campaigns/{campaignId}/company-codes`**

##### Validation (หลักการตรวจสอบเงื่อนไข)
*   **ตรวจสอบความถูกต้องของรหัสบริษัท:** แต่ละรหัส `companyCode` จะต้องมีข้อมูลอยู่จริงในระบบ Partner Companies หากไม่มีอยู่จริง ระบบจะส่งผลลัพธ์กลับมาเป็น **400 Bad Request** พร้อมระบุรหัสเจ้าปัญหา
*   **ข้อจำกัดการผูกข้อมูล:** แต่ละรหัส `companyCode` สามารถผูกเข้ากับแคมเปญได้สูงสุด **1 แคมเปญ** ในเวลาเดียวกันเท่านั้น หากรหัสใดถูกผูกไว้กับแคมเปญอื่นอยู่แล้ว คำขอจะล้มเหลวและระบบจะส่งผลลัพธ์กลับมาเป็น **409 Conflict** พร้อมส่งรหัสที่เป็นปัญหาและ `campaignId` ปัจจุบันกลับมาด้วย (หากต้องการผูกใหม่ จะต้องทำการปลดการผูก หรือ Unbind จากแคมเปญเดิมก่อน)
*   **การเคลียร์ข้อมูล:** การส่งอาร์เรย์ว่าง (Empty array) จะเป็นการยกเลิกการผูกข้อมูล (Clear all bindings) ของแคมเปญนี้ทั้งหมด

##### 🔑 Parameters

###### Path Parameters
*   **`campaignId`** `string($uuid)` (*required*)
    *   **Description:** ตัวระบุแคมเปญเฉพาะ (Campaign identifier) ในรูปแบบ UUIDv4 ที่สร้างขึ้นและส่งมาจากฝั่ง Client
    *   **Example:** `a1b2c3d4-e5f6-7890-abcd-ef1234567890`

---

##### 📥 Request Body (application/json)

ข้อมูล JSON Payload ตัวอย่างสำหรับการผูกข้อมูลรหัสบริษัท:

```json
{
  "companyCodes": [
    "570",
    "TMSTH"
  ]
}
```
##### 📤 Response Description

ระบบจะส่งผลลัพธ์กลับมาในรูปแบบ `application/json` โดยมีรายละเอียดรหัสสถานะ (HTTP Status Code) ดังนี้:

###### 1. HTTP 200: Company codes replaced successfully.
*   **Description:** แทนที่ชุดข้อมูลรหัสบริษัทที่ผูกกับแคมเปญสำเร็จ
*   **Response Body Example:**
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

###### 2. HTTP 400: Bad request - Invalid input
*   **Description:** คำขอไม่ถูกต้องเนื่องจากข้อมูลนำเข้าไม่ผ่านเงื่อนไข (เช่น รหัสบริษัทไม่มีอยู่จริงในระบบ)
*   **Response Body Example:**
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
###### 3. HTTP 401: Unauthorized - Authentication required
*   **Description:** ปฏิเสธการเข้าถึงเนื่องจากไม่มีข้อมูลการยืนยันตัวตน หรือข้อมูลไม่ถูกต้อง
*   **Response Body Example:**
```json
{
  "code": "E401",
  "message": "Unauthorized access - invalid or missing authentication credentials",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

###### 4. HTTP 404: Not found - Resource does not exist
*   **Description:** ไม่พบข้อมูลแคมเปญตาม `campaignId` ที่ระบุมาในระบบ
*   **Response Body Example:**
```json
{
  "code": "E404",
  "message": "Data not found",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

###### 5. HTTP 409: Conflict - Resource already exists or version mismatch
*   **Description:** เกิดการขัดกันของข้อมูล (เช่น `companyCode` ที่ส่งมาถูกผูกไว้กับแคมเปญอื่นอยู่ก่อนแล้ว)
*   **Response Body Example:**
```json
{
  "code": "E409",
  "message": "Data is confliccted with existing records",
  "details": [],
  "timestamp": "2025-11-26T05:04:21.220Z",
  "traceId": "550e8400-e29b-41d4-a716-446655440000"
}
```

###### 6. HTTP 500: Internal server error
*   **Description:** เกิดข้อผิดพลาดที่ไม่คาดคิดภายในระบบเซิร์ฟเวอร์
*   **Response Body Example:**
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
