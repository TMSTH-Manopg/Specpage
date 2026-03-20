
# PublishCampaign → Premium API — Full Technical Specification

*Last updated: 2026-03-20 03:02:29*

เอกสารฉบับนี้เป็นการ **รวมข้อมูลทั้งหมดที่ได้ให้ไว้ก่อนหน้า** เกี่ยวกับระบบ PublishCampaign
ตั้งแต่ภาพรวมสถาปัตยกรรม, ลำดับการทำงาน, API Contract,
ไปจนถึง **ตารางอธิบายทุกฟิลด์** และ **JSON Schema แบบเต็ม**
สำหรับข้อมูลที่ส่งเข้า **Premium API**

---

## 1) Scope
- PublishCampaign จาก API1 → Service → Premium API
- ใช้เมื่อ Campaign ผ่านการยืนยันทั้งหมด (Confirmed)

---

## 2) Workflow Overview

```
API1 (POST /api/campaign/publish)
 └─ CampaignService.PublishCampaign()
     ├─ Generate Tariff
     ├─ Generate Tariff Extra
     ├─ Save Tariff Excel
     ├─ Change Published Status (Valid SI)
     ├─ Publish To Premium  ---> Premium API (JSON)
     └─ Send Email Summary
```

---


## 10) Campaign Fields
| Field | Type | Required | Description |
|---|---|---|---|
| CampaignCode | string | Yes | รหัสแคมเปญ |
| requestedBy | string | Yes | ผู้ร้องขอการ Publish |
| requestedAt | string | Yes | วันเวลา ISO-8601 |


## 11) Tariff Fields
| Field | Type | Required | Description |
|---|---|---|---|
| CampaignCode | string | Yes | รหัสแคมเปญ |
| polmst | string | Yes | Policy master code |
| pack | string | Yes | Package code |
| SClass | string | No | Sub class |
| covcod | string | No | Coverage code |
| Vehgrp | string | No | Vehicle group |
| vehuse | string | No | Vehicle usage |
| GarageCd | string | No | Garage code |
| makdes | string | No | Vehicle make |
| moddes | string | No | Vehicle model |
| cstFlag | string | No | Customer flag Y/N |
| MinCST | number | No | Min CST |
| MaxCST | number | No | Max CST |
| MinYear | integer | No | Min vehicle year |
| MaxYear | integer | No | Max vehicle year |
| MinSI | number | No | Min sum insured |
| MaxSI | number | No | Max sum insured |
| DriverName | string | No | Driver condition |
| DrivNo | integer | No | Driver count |
| DrivAge1 | integer | No | Driver age 1 |
| DrivAge2 | integer | No | Driver age 2 |
| uom6_u | string | No | UOM 6 |
| cctv | string | No | CCTV Y/N |
| uom1_v | string | No | UOM1 |
| uom2_v | string | No | UOM2 |
| uom5_v | string | No | UOM5 |
| Seats41 | integer | No | Passenger seats |
| mv411 | number | No | Coverage 411 SI |
| mv412 | number | No | Coverage 412 SI |
| mv413 | number | No | Coverage 413 SI |
| mv414 | number | No | Coverage 414 SI |
| mv42 | number | No | Medical expense SI |
| mv43 | number | No | Bail bond SI |
| Dedod | number | No | Deductible OD |
| AdDod | number | No | Deductible AD |
| DedPD | number | No | Deductible PD |
| fleet_per | number | No | Fleet percent |
| ncbyrs | integer | No | NCB years |
| ncb_per | number | No | NCB percent |
| Dspc_per | number | No | Special discount percent |
| loadclm_per | number | No | Claim loading percent |
| dstfper | number | No | Staff discount percent |
| baseprm1 | number | No | Base premium |
| mainPrem | number | No | Main premium |
| vehicleUsePrem | number | No | Vehicle use premium |
| enginePrem | number | No | Engine premium |
| driverPrem | number | No | Driver premium |
| vehicleAgePrem | number | No | Vehicle age premium |
| accessoryPrem | number | No | Accessory premium |
| siPrem | number | No | SI premium |
| vehicleGroupPrem | number | No | Vehicle group premium |
| tpbiPersonPrem | number | No | TPBI per person premium |
| tpbiAccPrem | number | No | TPBI per accident premium |
| tppdPersonPrem | number | No | TPPD premium |
| driver411Prem | number | No | 411 driver premium |
| passenger412Prem | number | No | 412 passenger premium |
| driver413Prem | number | No | 413 driver premium |
| passenger414Prem | number | No | 414 passenger premium |
| medicalExp42Prem | number | No | Medical expense premium |
| bailbond43Prem | number | No | Bail bond premium |
| deductODPrem | number | No | Deduct OD premium |
| deductADPrem | number | No | Deduct AD premium |
| deductPDPrem | number | No | Deduct PD premium |
| fleet_amt | number | No | Fleet amount |
| ncb_amt | number | No | NCB amount |
| Dspc_amt | number | No | Special discount amount |
| loadclm_amt | number | No | Claim loading amount |
| dstfprm | number | No | Staff discount amount |
| SI22 | number | No | SI coverage 22 |
| baseprm3 | number | No | Base premium set 3 |
| prem3new | number | No | Premium set 3 |
| vehicleUse3Prem | number | No | Vehicle use premium set 3 |
| engine3Prem | number | No | Engine premium set 3 |
| si3Prem | number | No | SI premium set 3 |
| prm_tnew | number | No | Total premium new |
| prem_net_pd | number | No | Net premium |
| adjustAll | number | No | Total adjustment |
| prm_stpnew | number | No | Stamp duty |
| prm_vatnew | number | No | VAT |
| prm_gapnew | number | No | Gross premium before short rate |
| shortRate | number | No | Short rate percent |
| day | integer | No | Coverage days |
| NetInputGap | number | No | Net input amount |
| GrossInputGap | number | No | Gross input amount |
| BehaviorLV | string | No | Behavior level |
| BehaviorPercent | number | No | Behavior percent |
| WallChargeSI | number | No | Wall charger SI |
| RateWallCharge | number | No | Wall charger rate |
| NetPremiumWallCharge | number | No | Wall charger net premium |
| GrossPremiumWallCharge | number | No | Wall charger gross premium |
| BatteryYear | integer | No | Battery year |
| BatteryPrice | number | No | Battery price |
| BatterySI | number | No | Battery SI |
| RateBattery | number | No | Battery rate |
| NetPremiumBattery | number | No | Battery net premium |
| GrossPremiumBattery | number | No | Battery gross premium |
| MinEVDrivNo | integer | No | Min EV drivers |
| MaxEVDrivNo | integer | No | Max EV drivers |
| DealerGarageRate | number | No | Dealer garage rate |
| DealerGarageAmount | number | No | Dealer garage amount |


## 12) JSON Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "campaign": {
      "type": "object",
      "properties": {
        "CampaignCode": {
          "type": "string"
        },
        "requestedBy": {
          "type": "string"
        },
        "requestedAt": {
          "type": "string",
          "format": "date-time"
        }
      },
      "required": [
        "CampaignCode",
        "requestedBy",
        "requestedAt"
      ]
    },
    "tariffs": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "CampaignCode": {
            "type": "string"
          },
          "polmst": {
            "type": "string"
          },
          "pack": {
            "type": "string"
          },
          "SClass": {
            "type": "string"
          },
          "covcod": {
            "type": "string"
          },
          "Vehgrp": {
            "type": "string"
          },
          "vehuse": {
            "type": "string"
          },
          "GarageCd": {
            "type": "string"
          },
          "makdes": {
            "type": "string"
          },
          "moddes": {
            "type": "string"
          },
          "cstFlag": {
            "type": "string"
          },
          "MinCST": {
            "type": "number"
          },
          "MaxCST": {
            "type": "number"
          },
          "MinYear": {
            "type": "integer"
          },
          "MaxYear": {
            "type": "integer"
          },
          "MinSI": {
            "type": "number"
          },
          "MaxSI": {
            "type": "number"
          },
          "DriverName": {
            "type": "string"
          },
          "DrivNo": {
            "type": "integer"
          },
          "DrivAge1": {
            "type": "integer"
          },
          "DrivAge2": {
            "type": "integer"
          },
          "uom6_u": {
            "type": "string"
          },
          "cctv": {
            "type": "string"
          },
          "uom1_v": {
            "type": "string"
          },
          "uom2_v": {
            "type": "string"
          },
          "uom5_v": {
            "type": "string"
          },
          "Seats41": {
            "type": "integer"
          },
          "mv411": {
            "type": "number"
          },
          "mv412": {
            "type": "number"
          },
          "mv413": {
            "type": "number"
          },
          "mv414": {
            "type": "number"
          },
          "mv42": {
            "type": "number"
          },
          "mv43": {
            "type": "number"
          },
          "Dedod": {
            "type": "number"
          },
          "AdDod": {
            "type": "number"
          },
          "DedPD": {
            "type": "number"
          },
          "fleet_per": {
            "type": "number"
          },
          "ncbyrs": {
            "type": "integer"
          },
          "ncb_per": {
            "type": "number"
          },
          "Dspc_per": {
            "type": "number"
          },
          "loadclm_per": {
            "type": "number"
          },
          "dstfper": {
            "type": "number"
          },
          "baseprm1": {
            "type": "number"
          },
          "mainPrem": {
            "type": "number"
          },
          "vehicleUsePrem": {
            "type": "number"
          },
          "enginePrem": {
            "type": "number"
          },
          "driverPrem": {
            "type": "number"
          },
          "vehicleAgePrem": {
            "type": "number"
          },
          "accessoryPrem": {
            "type": "number"
          },
          "siPrem": {
            "type": "number"
          },
          "vehicleGroupPrem": {
            "type": "number"
          },
          "tpbiPersonPrem": {
            "type": "number"
          },
          "tpbiAccPrem": {
            "type": "number"
          },
          "tppdPersonPrem": {
            "type": "number"
          },
          "driver411Prem": {
            "type": "number"
          },
          "passenger412Prem": {
            "type": "number"
          },
          "driver413Prem": {
            "type": "number"
          },
          "passenger414Prem": {
            "type": "number"
          },
          "medicalExp42Prem": {
            "type": "number"
          },
          "bailbond43Prem": {
            "type": "number"
          },
          "deductODPrem": {
            "type": "number"
          },
          "deductADPrem": {
            "type": "number"
          },
          "deductPDPrem": {
            "type": "number"
          },
          "fleet_amt": {
            "type": "number"
          },
          "ncb_amt": {
            "type": "number"
          },
          "Dspc_amt": {
            "type": "number"
          },
          "loadclm_amt": {
            "type": "number"
          },
          "dstfprm": {
            "type": "number"
          },
          "SI22": {
            "type": "number"
          },
          "baseprm3": {
            "type": "number"
          },
          "prem3new": {
            "type": "number"
          },
          "vehicleUse3Prem": {
            "type": "number"
          },
          "engine3Prem": {
            "type": "number"
          },
          "si3Prem": {
            "type": "number"
          },
          "prm_tnew": {
            "type": "number"
          },
          "prem_net_pd": {
            "type": "number"
          },
          "adjustAll": {
            "type": "number"
          },
          "prm_stpnew": {
            "type": "number"
          },
          "prm_vatnew": {
            "type": "number"
          },
          "prm_gapnew": {
            "type": "number"
          },
          "shortRate": {
            "type": "number"
          },
          "day": {
            "type": "integer"
          },
          "NetInputGap": {
            "type": "number"
          },
          "GrossInputGap": {
            "type": "number"
          },
          "BehaviorLV": {
            "type": "string"
          },
          "BehaviorPercent": {
            "type": "number"
          },
          "WallChargeSI": {
            "type": "number"
          },
          "RateWallCharge": {
            "type": "number"
          },
          "NetPremiumWallCharge": {
            "type": "number"
          },
          "GrossPremiumWallCharge": {
            "type": "number"
          },
          "BatteryYear": {
            "type": "integer"
          },
          "BatteryPrice": {
            "type": "number"
          },
          "BatterySI": {
            "type": "number"
          },
          "RateBattery": {
            "type": "number"
          },
          "NetPremiumBattery": {
            "type": "number"
          },
          "GrossPremiumBattery": {
            "type": "number"
          },
          "MinEVDrivNo": {
            "type": "integer"
          },
          "MaxEVDrivNo": {
            "type": "integer"
          },
          "DealerGarageRate": {
            "type": "number"
          },
          "DealerGarageAmount": {
            "type": "number"
          }
        },
        "required": [
          "CampaignCode",
          "polmst",
          "pack"
        ]
      }
    }
  },
  "required": [
    "campaign",
    "tariffs"
  ]
}
```
