# แตกวิดีโอเป็นภาพด้วย FFmpeg

ตัวอย่างคำสั่งสำหรับ **PowerShell บน Windows** ใช้ไฟล์ `source.mp4` และโฟลเดอร์ผลลัพธ์ `frames`

## 1. ตรวจว่าเรียก FFmpeg ได้

```powershell
ffmpeg -version
```

ถ้าไม่พบคำสั่ง ต้องติดตั้ง FFmpeg และเพิ่มโฟลเดอร์ที่มี `ffmpeg.exe` ลงใน PATH ก่อน แล้วเปิด Terminal ใหม่ หรือเรียกผ่านพาธเต็มของโปรแกรมที่ติดตั้งไว้

## 2. เข้าโฟลเดอร์โปรเจกต์

เปลี่ยนพาธตัวอย่างนี้ให้ตรงกับโฟลเดอร์ของคุณ และวางวิดีโอชื่อ `source.mp4` ไว้ในนั้น

```powershell
Set-Location -LiteralPath 'C:\path\to\my-cinematic-website'
Get-Item -LiteralPath '.\source.mp4'
```

## 3. สร้างโฟลเดอร์ แล้วแตกเฟรม

ใช้ `frames` ที่ยังไม่มีภาพจากการแตกเฟรมครั้งก่อน เพื่อไม่ให้ภาพเก่าปะปนกับชุดใหม่ คำสั่งนี้ใช้ `-n` เพื่อไม่เขียนทับไฟล์เดิม

```powershell
New-Item -ItemType Directory -Path '.\frames' -Force | Out-Null
ffmpeg -n -i "source.mp4" -an -vf "fps=15,scale=1280:-2:flags=lanczos" -c:v libwebp -quality 76 -compression_level 4 -start_number 0 "frames/frame-%04d.webp"
```

| ส่วนของคำสั่ง | ความหมาย |
|---|---|
| `-i "source.mp4"` | ไฟล์วิดีโอต้นทาง เปลี่ยนชื่อให้ตรงกับไฟล์ของคุณได้ |
| `-an` | ไม่ใช้เสียงในผลลัพธ์ |
| `fps=15` | ดึงภาพ 15 ใบต่อวินาที |
| `scale=1280:-2` | ปรับความกว้างเป็น 1280 พิกเซล และคำนวณความสูงตามสัดส่วนให้เป็นเลขคู่ |
| `-c:v libwebp` | บันทึกเป็นภาพ WebP |
| `-quality 76` | ค่าคุณภาพการบีบอัดภาพในตัวอย่าง |
| `-start_number 0` | เริ่มลำดับที่ 0 |
| `frame-%04d.webp` | ตั้งชื่อเป็น frame-0000.webp, frame-0001.webp และต่อไป |

15 FPS และความกว้าง 1280 เป็นจุดเริ่มต้นของตัวอย่าง ไม่ใช่ค่าที่เหมาะกับทุกงาน ลองปรับตามรายละเอียดภาพ ขนาดไฟล์ และความลื่นบนอุปกรณ์เป้าหมาย

## 4. ตรวจภาพที่ได้

```powershell
(Get-ChildItem -LiteralPath '.\frames' -Filter 'frame-*.webp' -File).Count
Get-ChildItem -LiteralPath '.\frames' -Filter 'frame-*.webp' -File | Sort-Object Name | Select-Object -First 5 Name
```

เปิดดูภาพแรก ภาพกลาง และภาพท้ายด้วย คลิป 8 วินาทีที่ดึง 15 FPS จะได้ประมาณ 120 ภาพ แต่ให้ใช้จำนวนไฟล์จริงเป็นหลัก

หากคำสั่งแจ้งว่าไม่พบโฟลเดอร์ ให้ตรวจว่าอยู่ในโปรเจกต์ที่ถูกต้องและสร้าง `frames` แล้ว หากพบ `Unknown encoder 'libwebp'` แสดงว่า FFmpeg ชุดที่ใช้อยู่ไม่มี encoder นี้

เมื่อได้ภาพครบแล้ว ใช้ [พรอมป์ต์สร้างเว็บ](website-prompt.md) ใน Coding Agent ที่เข้าถึงโฟลเดอร์โปรเจกต์นี้ได้
