# Prompt 2 — Visual polish with Astra

[Workshop guide / วิธีใช้](README.md) · [Prompt 1 — Structural model](structural-prompt.md)

Use this only after you have reviewed and approved the structural model in the browser. Keep the outputs from Prompt 1 in the same workspace and add `style-reference.jpg`. The video uses Astra for this stage.

ใช้หลังจากตรวจและยืนยันโครงในเบราว์เซอร์แล้วเท่านั้น เก็บผลลัพธ์จาก Prompt 1 ไว้ใน Workspace เดิม และเพิ่ม `style-reference.jpg` เพื่อบอกวัสดุ สี แสง และสไตล์ ห้ามใช้ภาพนี้เปลี่ยนโครงที่ยืนยันแล้ว

## Copy this prompt / คัดลอกพรอมป์ต์นี้

```text
The structural model has already been approved through the browser viewer.

Read:
- `room-structural.blend`
- `room-structural.glb`
- `room-spec.md`
- `structural-validation.json`
- `style-reference.jpg`

IMPORTANT:
The structural scene is now the LOCKED BASELINE.
Use Blender only as a background 3D generation/rendering engine.
Do NOT open or depend on the Blender GUI.
The user will review all visual changes through the local browser viewer.

Use `style-reference.jpg` only for visual language:
- material palette
- furniture character
- lighting mood
- textile style
- decorative language

The style reference is NOT structural authority.

Do NOT change:
- room dimensions
- wall positions
- door positions
- window positions
- structural openings
- validated architectural geometry

If the style reference conflicts with the floor plan, preserve the floor plan and adapt the visual design.

## Before editing

Capture and save the locked structural baseline:
- object transforms
- dimensions
- relevant mesh/geometry identifiers

The final validation must prove that this baseline remains unchanged.

## Visual priorities

Work in this order:
1. major furniture
2. believable real-world furniture scale
3. floor and wall materials
4. cabinets / built-ins where supported
5. curtains and textiles
6. lighting
7. plants / decoration
8. small details only after the major forms are correct

Prefer procedural or locally generated assets.
Do not download paid assets.
Do not use copyrighted commercial 3D assets without permission.
No people.

## Outputs

Create:
- `room-final.blend`
- `room-final.glb`
- `room-final.png`
- `visual-validation.json`

Again, the `.blend` file is a source artifact.
The normal review experience must be through the browser.

## Update the Web Viewer

Update the existing `web-viewer/` so the browser can display the final model.

Add controls for:
- Final
- Structural / Before
- orbit
- zoom
- pan
- center
- fit model

If practical, allow switching between:
`room-structural.glb` and `room-final.glb`
so the user can compare:
STRUCTURE vs FINAL
without opening Blender.

Keep the same local viewer URL/launcher if possible.

## Validation

After the visual pass verify:
- locked structural geometry unchanged
- room dimensions unchanged
- wall positions unchanged
- openings unchanged
- final GLB exports successfully
- final GLB loads successfully in the browser
- Structural / Final switching works if implemented

Save the result to:
`visual-validation.json`

When complete, give me the local browser URL or launcher.
Do NOT ask me to open Blender.
```

Compare Structural / Before and Final in the browser. Check the validation report as well as the visible result; a successful export alone does not demonstrate that the structural baseline was preserved.

สลับดู Structural / Before กับ Final ในเบราว์เซอร์ และตรวจรายงาน Validation ควบคู่กับภาพจริง การ Export สำเร็จอย่างเดียวไม่ได้ยืนยันว่าโครงยังเหมือนเดิม
