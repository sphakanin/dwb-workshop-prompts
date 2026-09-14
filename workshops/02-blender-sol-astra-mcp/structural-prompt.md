# Prompt 1 — Structural model with Sol + MCP

[Workshop guide / วิธีใช้](README.md) · [Prompt 2 — Visual polish](visual-polish-prompt.md)

Prepare `plan.jpg` in your project workspace, then give the English block below to an agent that can read the image, run Blender in the background, and create a local web viewer. The video uses GPT-5.6 Sol + MCP for this stage.

เตรียม `plan.jpg` ไว้ใน Workspace ที่ Agent เข้าถึงได้ แล้วคัดลอกข้อความในกรอบด้านล่างไปใช้ ขั้นตอนนี้ใช้ขึ้นโครงและตรวจสัดส่วนก่อน ยังไม่ตกแต่งตามภาพสไตล์

Use `plan.jpg` consistently. The supplied draft also referred to `plan.png`; those references have been corrected to match the input filename. If you use another filename, update every reference in the prompt.

## Copy this prompt / คัดลอกพรอมป์ต์นี้

```text
Read `plan.jpg` first.

Goal: Build an accurate structural 3D model of this single room/apartment using Blender as a background 3D engine, then create a local browser-based viewer for reviewing the result.

IMPORTANT WORKFLOW RULE:
Do NOT open or depend on the Blender GUI.
The user will NOT review the model inside Blender.
Blender must be used through scripts / command line / background or headless execution where practical.
The primary review interface must be a local web viewer opened in a normal web browser.

Target workflow:
plan.jpg → GPT-5.6 Sol → MCP → Blender Python / background build → GLB → Local Web Viewer → Browser review

Treat `plan.jpg` as the geometry source of truth.
Do NOT use `style-reference.jpg` yet.

## Structural rules

1. Extract every readable dimension from the plan.
2. Identify:
   - exterior walls
   - interior walls
   - doors and door openings
   - windows
   - fixed architectural elements
   - major furniture shown in the plan
3. Work in real-world metric units.
4. Preserve the proportions and positions shown in the plan.
5. Do not invent hidden rooms, walls, openings, or architectural features.
6. If something cannot be determined from the drawing, mark it explicitly as an assumption.
7. Use simple geometry for this pass. Do not spend time on:
   - detailed furniture
   - textures
   - decoration
   - photorealistic rendering
8. Build the structural scene through a reproducible Blender Python script.
9. Run Blender through command line / background mode. Do not require manual interaction with the Blender application.
10. Keep the original source plan unchanged.

## Before building

Create:
`room-spec.md`

Document:
- dimensions extracted directly from the plan
- room boundaries
- wall thickness assumptions
- doors
- windows
- fixed elements
- furniture/blockout items
- every assumption made

## Blender outputs

Create:
- `build_room.py`
- `room-structural.blend`
- `room-structural.glb`
- `room-spec.md`
- `structural-validation.json`

The `.blend` file is a source artifact only.
Do NOT expect the user to open it for review.

## Browser Viewer

Create a simple local web viewer inside:
`web-viewer/`

The viewer must load:
`room-structural.glb`

Provide at minimum:
- orbit
- zoom
- pan
- reset / center view
- fit model to screen
- dollhouse / isometric starting camera
- clear loading/error state

The viewer must work locally through a simple localhost web server.
Do not require a cloud service.
Prefer locally available dependencies or a minimal self-contained implementation.

Create a launcher if useful, for example:
`OPEN-VIEWER.cmd`
or an equivalent script that:
1. starts a localhost web server
2. opens the viewer in the default browser

The user should be able to inspect the entire structural model without opening Blender.

## Validation

`structural-validation.json` must include:
- final room dimensions
- number/list of walls
- door/window openings
- structural object list
- assumptions
- exported GLB path
- validation status

Verify that the GLB successfully loads in the browser viewer.
If browser/headless browser testing is available through the existing workspace tools, test the viewer before reporting completion.

## Final response

When finished, tell me:
1. what was read directly from the plan
2. what required assumptions
3. what files were generated
4. the local URL or launcher used to review the model

Do NOT perform the visual-polish pass yet.
Do NOT open Blender GUI.
```

Review the model and assumptions in the browser. Request structural corrections until you are satisfied, then use [Prompt 2](visual-polish-prompt.md).

เปิดตรวจโมเดลและสมมุติฐานในเบราว์เซอร์ แก้โครงให้พอใจก่อน แล้วจึงไปต่อที่ [Prompt 2](visual-polish-prompt.md)
