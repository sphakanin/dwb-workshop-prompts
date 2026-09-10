# Prompt สร้างวิดีโอจากภาพเริ่มต้นและภาพสุดท้าย

แนบภาพทั้งสองในช่อง First/Start Frame และ Last/End Frame ของเครื่องมือที่รองรับ แล้วแทนข้อความในวงเล็บด้านล่างก่อนคัดลอกพรอมป์ต์

ตัวอย่างในคลิป:

- `[START STATE]` → `seasoned rice in the bowl`
- `[END STATE]` → `the same bowl completed with tamagoyaki and glazed grilled unagi`

ภาพทั้งสองควรเป็นฉากเดียวกัน มุมกล้องและแสงใกล้เคียงกัน พรอมป์ต์นี้ใช้บอกการเคลื่อนไหวระหว่างภาพ ไม่ได้ทดแทนภาพอ้างอิง

## คัดลอกพรอมป์ต์นี้

```text
Create a smooth cinematic transition from the first image to the last image.
Preserve the same subject, environment, camera angle, lighting direction, color mood, scale, and overall realism so the result feels like one continuous shot in the same world.
Show a clear, natural progression from [START STATE] to [END STATE].
Use restrained, believable motion appropriate to the subject. Keep the camera mostly stable unless a subtle push-in or parallax helps connect the two frames.
Preserve object identity and spatial continuity throughout the transition.
Avoid sudden cuts, flicker, duplicated objects, disappearing objects, shape distortion, melting, aggressive morphing, or unnecessary camera movement.
End cleanly on the supplied final image.
Duration: 5–8 seconds. Style: cinematic, smooth, realistic, seamless.
```

หากเครื่องมือมีช่องกำหนดความยาว ให้ตั้งค่าผ่านช่องนั้นด้วย โดยเลือกความยาวที่บริการรองรับ ตรวจวิดีโอจริงว่าภาพไม่บิดเบี้ยว วัตถุไม่หาย และจบใกล้ภาพสุดท้ายก่อนดาวน์โหลด

บันทึกไฟล์ที่เลือกเป็น `source.mp4` แล้วไปต่อที่ [คำสั่ง FFmpeg](ffmpeg-commands.md)
