PublishCampaign → Premium API — Technical Spec

วัตถุประสงค์: เมื่อแคมเปญถูก “ยืนยันทั้งหมด” ระบบ API1 จะทำกระบวนการ PublishCampaign เพื่อสร้างข้อมูลเบี้ย (Tariff), อัปเดตสถานะ, ส่งอีเมล และ Publish to Premium โดยแปลงข้อมูลเป็น JSON เพื่อเรียก Premium API (ชั้น SOAP/WS Premium อยู่หลัง Premium API)

1) ขอบเขต (Scope)

ครอบคลุมเฉพาะเส้นทาง PublishCampaign จาก API1 → Service → (Generate & Persist) → Publish To Premium → Premium API
ไม่ครอบคลุมการสร้าง/แก้ไขเนื้อหาแคมเปญใน Backoffice และไม่ครอบคลุม SOAP ภายในของ Premium (ถือเป็น downstream)


2) สถาปัตยกรรมภาพรวม
