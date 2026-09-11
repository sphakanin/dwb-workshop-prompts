# From 2 Photos to a Scroll-driven Cinematic Website

**English** · [ภาษาไทย](#ภาษาไทย) · [All workshops](../../README.md)

Turn your own photos into a website whose image sequence responds to scrolling.

**Scroll = Timeline:** scroll down to move forward, scroll up to reverse, and stop scrolling to pause.

[Watch the original workshop (Thai)](https://youtu.be/TcfffXhX1Bw)

## What you need

- Two images showing the same subject at the beginning and end of a transition.
- A video generation tool that accepts both first and last frames.
- FFmpeg with WebP encoding support.
- A coding agent that can read and edit your project files.

Choose any compatible tools. Free options depend on each service’s quotas and terms.

## Step by step

1. Prepare matching start and end images with consistent camera angle, lighting, and scale. Use 16:9 images for a landscape website. Our example changes seasoned rice into the same bowl topped with tamagoyaki and grilled unagi.
2. Open the [video prompt](video-prompt.md). Replace `[START STATE]` and `[END STATE]`, attach both images in the first/last frame inputs, and generate the transition. The copyable prompt is in English. Check distortion, flicker, missing objects, and the final frame.
3. Save the video as `source.mp4` in your project folder.
4. Extract frames using the commands below.
5. Open your project in a coding agent and give it the English block in the [website prompt](website-prompt.md). Adapt the Japan-trip example to your own subject.
6. Run the website and test desktop, mobile, reverse scrolling, and reduced motion.

## Extract frames — Windows PowerShell

Install FFmpeg and add it to PATH, or use its full executable path. Open a new terminal after changing PATH. Replace the sample project path below. Use a fresh `frames` folder so old and new images do not mix. The command refuses to overwrite existing files.

```powershell
ffmpeg -version
Set-Location -LiteralPath 'C:\path\to\my-cinematic-website'
Get-Item -LiteralPath '.\source.mp4'
New-Item -ItemType Directory -Path '.\frames' -Force | Out-Null
ffmpeg -n -i "source.mp4" -an -vf "fps=15,scale=1280:-2:flags=lanczos" -c:v libwebp -quality 76 -compression_level 4 -start_number 0 "frames/frame-%04d.webp"
(Get-ChildItem -LiteralPath '.\frames' -Filter 'frame-*.webp' -File).Count
```

This extracts 15 images per second, scales them to 1280 pixels wide with proportional height, and saves WebP files starting at `frame-0000.webp`. Adjust frame rate, dimensions, and quality for your images, file size, and target devices.

An 8-second clip at 15 FPS produces approximately 120 frames; use the actual file count. Inspect first, middle, and last images. `Unknown encoder 'libwebp'` means your FFmpeg build lacks this encoder. The [detailed FFmpeg guide](ffmpeg-commands.md) has the same commands with Thai explanations.

## Project structure

```text
my-cinematic-website/
├── source.mp4
├── frames/
│   ├── frame-0000.webp
│   ├── frame-0001.webp
│   └── ...
└── website-prompt.md
```

All documents use **`frames`**. If your folder is named `frame`, rename it or update the commands and prompts consistently.

## Adapt the example

For coffee, shoes, or another product, replace the subject, visual progression, mood, and story while keeping scrolling, performance, accessibility, and verification requirements. Only describe states present in your actual frames. Do not invent restaurant facts, prices, history, or reviews.

This kit contains prompts and commands; bring your own photos, video, and frames. The workshop ends with a website running locally on localhost. Deployment is a separate next step.

## Quality checks

- Forward and reverse scrolling follow the sequence without white flashes.
- Images and text fit mobile screens.
- Text remains HTML and does not obscure important visual details.
- Frame loading and the in-memory image cache are bounded.
- A poster and fallback work when frames fail or reduced motion is enabled.
- Website copy contains no invented facts.

---

## ภาษาไทย

# จาก 2 รูป สู่ Scroll-driven Cinematic Website

ชุดพรอมป์ต์และคำสั่งประกอบคลิปของ **Dev with Bebz** สำหรับเปลี่ยนภาพที่คุณมีให้เป็นเว็บไซต์ที่ภาพเคลื่อนไหวตามการเลื่อนหน้าจอ

**Scroll = Timeline** — เลื่อนลงภาพเดินหน้า เลื่อนกลับภาพย้อนตาม และหยุดเลื่อนภาพก็หยุด

ไม่ผูกกับรุ่นหรือค่าย AI เลือกเครื่องมือสร้างวิดีโอที่รับภาพเริ่มต้นและภาพสุดท้ายได้ และ Coding Agent ที่ทำงานกับไฟล์โปรเจกต์ได้ เริ่มด้วยตัวเลือกใช้ฟรีได้ตามโควตาและเงื่อนไขของบริการที่คุณเลือก

## เริ่มตรงนี้

1. เตรียมภาพเริ่มต้นและภาพสุดท้ายของวัตถุหรือฉากเดียวกัน พยายามให้มุมกล้อง แสง และสัดส่วนใกล้กัน เช่น ข้าวเปล่า → ข้าวหน้าไข่และปลาไหล หากต้องการเว็บแนวนอน ให้เตรียมภาพ 16:9 ทั้งคู่
2. เปิด [พรอมป์ต์สร้างวิดีโอ](video-prompt.md) เปลี่ยน `[START STATE]` และ `[END STATE]` แล้วส่งพร้อมภาพทั้งสองให้เครื่องมือสร้างวิดีโอ ตรวจผลก่อนใช้จริง
3. ดาวน์โหลดวิดีโอที่เลือก ตั้งชื่อ `source.mp4` แล้ววางในโฟลเดอร์โปรเจกต์
4. ทำตาม [คำสั่ง FFmpeg](ffmpeg-commands.md) เพื่อแตกภาพลงใน `frames/`
5. เปิดโฟลเดอร์โปรเจกต์ใน Coding Agent แล้วส่ง [พรอมป์ต์สร้างเว็บ](website-prompt.md) ให้ Agent ที่มีสิทธิ์อ่านไฟล์ในโฟลเดอร์นี้
6. เปิดเว็บจริงและตรวจทั้ง desktop/mobile รวมถึงการเลื่อนย้อนกลับและ reduced motion

## โครงสร้างก่อนสร้างเว็บ

```text
my-cinematic-website/
├── source.mp4
├── frames/
│   ├── frame-0000.webp
│   ├── frame-0001.webp
│   └── ...
└── website-prompt.md
```

ทุกไฟล์ในชุดนี้ใช้ชื่อโฟลเดอร์ **`frames`** เหมือนกัน หากโปรเจกต์เดิมของคุณใช้ `frame` ให้เปลี่ยนชื่อโฟลเดอร์ หรือแก้ชื่อในพรอมป์ต์และคำสั่งให้ตรงกับของจริง

## เปลี่ยนเป็นเรื่องของคุณ

พรอมป์ต์วิดีโอใช้กับหลายหัวข้อได้ ส่วนพรอมป์ต์เว็บเป็นตัวอย่างฉบับเต็มของทริปญี่ปุ่น หากจะทำเรื่องกาแฟ รองเท้า หรือสินค้าอื่น ให้เปลี่ยนคำอธิบายวัตถุ ลำดับภาพ โทนภาพ และเรื่องเล่าที่เกี่ยวข้องก่อนส่ง โดยคงข้อกำหนดเรื่อง scroll, performance, accessibility และการตรวจงานไว้

อย่าบอกให้เว็บแสดงสถานะกลางที่ไม่มีในวิดีโอหรือเฟรมจริง และอย่าให้ AI แต่งข้อมูลร้าน ราคา ประวัติ หรือรีวิวที่คุณไม่ได้ให้ไว้

ชุดนี้มีเฉพาะเอกสารพรอมป์ต์และคำสั่ง ไม่ได้รวมรูป วิดีโอ เฟรม หรือเว็บสำเร็จรูป ให้เตรียมภาพของคุณเอง

คลิปตอนนี้จบที่เว็บไซต์รันบนเครื่องผ่าน localhost ส่วนการ Deploy ขึ้นออนไลน์เป็นขั้นตอนถัดไป

## ก่อนส่งงาน

- เลื่อนลงและย้อนกลับแล้วภาพเดินตาม ไม่มีเฟรมขาววาบ
- ภาพและข้อความไม่ล้นจอบนมือถือ
- ข้อความเป็น HTML และไม่บังจุดสำคัญของภาพ
- ไม่โหลดทุกเฟรมพร้อมกัน และมีขอบเขตการเก็บภาพในหน่วยความจำ
- มี poster และ fallback เมื่อโหลดเฟรมไม่ได้หรือผู้ใช้เลือก reduced motion
- ตรวจข้อความบนเว็บว่าไม่มีข้อมูลที่ AI แต่งขึ้น

Dev with Bebz
