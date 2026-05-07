# PNG Pair To FUXA Widget

ไฟล์เครื่องมือ:

- `png-pair-to-fuxa-widget.html`

## ใช้งาน

1. เปิดไฟล์ `png-pair-to-fuxa-widget.html` ด้วยเบราว์เซอร์
2. เลือกรูป PNG สถานะ `OFF`
3. เลือกรูป PNG สถานะ `ON`
4. ตั้งชื่อ widget และข้อความใต้ปุ่ม
5. กด `Generate SVG`
6. กด `Download SVG`

## หลังจากได้ไฟล์ SVG

นำไฟล์ที่สร้างได้ไปไว้ในโฟลเดอร์ widget ของ FUXA เช่น:

- `FUXA/widgets/smartfarm-examples/`

จากนั้นรีเฟรช FUXA editor แล้วเปิด `Widgets Kiosk`

## สิ่งที่ widget นี้ทำ

- มีแค่ 2 สถานะ: `OFF` และ `ON`
- ใช้ตัวแปร `_pb_state` สำหรับสลับสถานะ
- ใช้ตัวแปร `_ps_label` สำหรับข้อความใต้รูป
- กดบน widget แล้ว toggle ค่า `_pb_state` ได้

## หมายเหตุ

- ตัว widget จะฝังรูป PNG เป็น data URL ลงใน SVG เลย
- เพราะงั้นไฟล์ SVG ที่ได้จะค่อนข้างใหญ่ถ้ารูปต้นฉบับใหญ่
- ถ้าต้องการไฟล์เล็กลง ควรย่อ PNG ก่อนนำเข้า
