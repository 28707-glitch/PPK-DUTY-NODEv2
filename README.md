# PPK Duty Node Backend V8

เวอร์ชันนี้ใช้โครงสร้างใหม่:

- Node.js + Socket.IO บน Render = API และ Real-time
- Google Sheets = เก็บ Users / Records / Duties / Settings แบบถาวร
- Apps Script = อัปโหลดรูปหลักฐานเข้า Google Drive ด้วยบัญชีเจ้าของสคริปต์

เหตุผลที่เปลี่ยนจาก Service Account Drive upload:

Service Account ไม่มี Drive storage quota จึงไม่ควรใช้สร้างไฟล์รูปใน My Drive โดยตรง เวอร์ชันนี้ให้ Apps Script ทำหน้าที่สร้างไฟล์ใน Drive แทน

## ไฟล์ที่ต้องอัป GitHub / Render

ต้องวางไฟล์เหล่านี้ไว้หน้าแรกของ repo `PPK-DUTY-NODE`

```text
server.js
package.json
```

ห้ามอัป ZIP อย่างเดียว เพราะ Render ไม่แตก ZIP ให้เอง

## Environment Variables บน Render

ต้องมีค่าต่อไปนี้:

```text
CLIENT_ORIGIN=*
ADMIN_ID=admin
ADMIN_PASSWORD=admin1234
GOOGLE_SHEET_ID=1aUNaQZy5M5xGKcyMjT4bjHfT5aZxwVMM81bflfb4jFI
GOOGLE_DRIVE_FOLDER_ID=1HGh0iEjxu33dokLxCy74EHqmlAm3_37m
GOOGLE_SERVICE_ACCOUNT_EMAIL=อีเมล service account
GOOGLE_PRIVATE_KEY=private_key ตัวที่ยังไม่รั่ว
ENABLE_GOOGLE_STORAGE=true
SEED_DEMO=false
APPS_SCRIPT_UPLOAD_URL=URL Web App ของ Apps Script /exec
APPS_SCRIPT_UPLOAD_TOKEN=token จาก Apps Script function setup()
```

## ตรวจผลหลัง Deploy

เปิด:

```text
https://ppk-duty-node.onrender.com
```

ควรเห็น:

```json
{
  "version": "8.0.0-sheets-appscript-drive",
  "storage": "google-sheets-appscript-drive",
  "driveUpload": "apps-script",
  "appsScriptUploadReady": true
}
```

ถ้า `appsScriptUploadReady` เป็น `false` แปลว่ายังไม่ได้ตั้ง `APPS_SCRIPT_UPLOAD_URL`
