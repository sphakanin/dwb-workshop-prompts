# Prompt สร้างเว็บไซต์ — ตัวอย่างทริปญี่ปุ่น

เปิดโฟลเดอร์โปรเจกต์ที่มี `frames/` ใน Coding Agent แล้วคัดลอกเฉพาะข้อความในกรอบด้านล่างไปใช้ หรือให้ Agent อ่านไฟล์นี้เป็นโจทย์สร้างเว็บ

ตัวอย่างนี้ใช้เรื่องอาหารจากทริปญี่ปุ่น หากจะใช้กับสินค้าอื่น ให้แก้หัวข้อ ลำดับภาพ โทนภาพ และเนื้อเรื่องที่เกี่ยวข้องก่อนส่ง ใช้เฟรมที่เตรียมไว้จริง โดยคงข้อกำหนดด้านการโหลดภาพ การเลื่อน การรองรับมือถือ และการตรวจงานไว้

## คัดลอกพรอมป์ต์นี้

```text
Build a polished, production-quality storytelling website about my Japan trip using the frame sequence I have already prepared.

The extracted image frames are located in the `frames` folder. Inspect the existing files first and use those frames as the primary visual sequence. Do not regenerate, replace, or modify the supplied frame images. If files are missing or unusable, report the issue and ask for the correct inputs.

## Core Experience

Create a cinematic scroll-driven Hero section where the frame sequence transitions visually from:

**a simple bowl of rice → rice topped with egg → unagi rice bowl**, only to the extent that these states exist in the supplied frames. Follow the actual sequence; do not invent or generate missing intermediate states.

The animation must be controlled by the user's **native page scroll position**.

Requirements:

- Scrolling down advances the frame sequence.
- Scrolling back up reverses the sequence naturally.
- Do not autoplay it like a video.
- Do not hijack scrolling.
- Do not create artificial scroll inertia or a heavy custom smooth-scroll system.
- The page must remain responsive and pleasant to scroll with a mouse, trackpad, or touchscreen.
- The Hero should feel cinematic but still behave like a real website.

Map scroll progress to the available frames intelligently based on the actual number of images in the `frames` folder. The expected naming convention is frame-0000.webp, frame-0001.webp, and so on. Inspect and sort the actual filenames numerically; do not assume there are 120 or 150 images. Clamp the selected frame index to the available range. Report missing or unreadable frames and keep a valid poster or nearby loaded frame visible.

## Frame Loading and Performance

Do **not** load the entire frame sequence at once.

Implement an efficient frame-loading strategy:

- Load the poster / initial frame immediately.
- Preload only a small window of frames around the current scroll position.
- Prioritize the frame the user is about to see.
- Load nearby forward and backward frames progressively.
- Avoid unnecessary memory usage, especially on mobile.
- Bound both the preload concurrency and the decoded-image cache; loading progressively must not grow memory without limit.
- Keep the last valid frame visible while the requested frame loads, and prevent stale asynchronous loads from replacing the current frame.
- Prevent visible flashes, blank frames, or frame-loading jumps where possible.
- Keep scrolling smooth even on average mobile hardware.

Choose an implementation appropriate for the existing project instead of adding unnecessary dependencies.

## Hero Composition

The Hero should feel like a premium Japanese travel / food editorial experience.

Think in terms of:

- Japanese editorial design
- quiet luxury
- food photography
- travel journals
- printed magazines
- restrained typography
- generous negative space
- subtle hierarchy
- natural warmth
- elegant motion
- storytelling rather than marketing

The frame sequence should remain the visual focus.

Text must be real **HTML text layered over or around the experience**.

Do NOT bake titles, captions, typography, gradients containing text, or UI elements into the images.

Use text sparingly.

Possible narrative direction:

A simple meal becoming a memory.

The experience should gradually reveal the story as the food transforms.

## Visual Direction

Make the final website **stunning**, but avoid anything that looks like generic AI-generated web design.

Absolutely avoid typical "AI slop" aesthetics such as:

- excessive gradients
- random glowing blobs
- neon lighting
- glassmorphism everywhere
- floating translucent cards
- oversized rounded rectangles
- fake SaaS-style dashboard components
- excessive pill-shaped UI
- arbitrary decorative particles
- meaningless animations
- excessive parallax
- overly dramatic copywriting
- generic "Discover Japan" tourism-template styling
- dozens of sections added simply to make the page look larger

Do not over-design it.

Instead, make deliberate editorial choices in:

- typography
- composition
- spacing
- image cropping
- rhythm
- transitions
- subtle texture
- color
- hierarchy

A simpler composition executed extremely well is better than a visually noisy one.

The visual identity should feel handcrafted and intentional.

## Color and Typography

Use a warm Japanese editorial palette inspired by materials and food rather than technology.

For example:

- warm rice / ivory
- soft paper white
- charcoal ink
- muted brown
- subtle unagi / soy tones
- restrained warm accent colors

Do not mechanically use these exact colors if the existing imagery suggests a better palette. Derive the final visual system from the photographs.

Typography should feel editorial and sophisticated.

Use Japanese-compatible fonts where appropriate, but prioritize readability, loading performance, and visual quality.

## Responsive Behavior

The experience must work properly on:

- desktop
- laptop
- tablet
- mobile portrait
- mobile landscape where practical

Do not simply shrink the desktop layout.

On mobile:

- maintain the visual impact of the food
- adjust cropping intentionally
- keep text readable
- avoid covering the main subject with text
- reduce unnecessary decorative elements
- ensure scrolling remains responsive
- avoid allocating excessive memory to frame images

## Poster and Fallbacks

Provide a proper static poster state.

If the animation is unavailable or inappropriate, the page should still look finished.

Implement support for:

`prefers-reduced-motion: reduce`

For users who prefer reduced motion:

- avoid scrubbing through hundreds of frames
- present an elegant static or lightly transitioned Hero instead
- preserve the narrative and visual hierarchy
- make it feel like an intentional design rather than a broken animation

Also provide a reasonable fallback if JavaScript or frame loading fails.

## Content After the Hero

After the cinematic Hero, continue with a short editorial story about:

- food
- travelling in Japan
- how an ordinary meal can become part of a travel memory
- the emotional connection between photographs, taste, and remembering a trip

Keep this section concise.

This is a personal travel storytelling piece, not a restaurant review website.

Do NOT invent:

- restaurant names
- addresses
- prices
- chefs
- ratings
- awards
- historical claims
- specific locations that are not present in the project
- fake testimonials
- fake quotes
- fake travel facts
- fake reviews

If specific trip information is not available, write in a personal but intentionally non-specific way.

Do not fabricate details merely to fill the page.

## Storytelling Style

Avoid generic travel-copy phrases such as:

"Embark on an unforgettable culinary journey."

"Experience the authentic taste of Japan."

"Where tradition meets innovation."

Instead, use restrained editorial writing.

The story should feel observational and human — like looking back through photographs from a trip.

Short sentences and small moments are preferable to exaggerated marketing copy.

## Interaction Details

Polish the experience with subtle interactions where they genuinely improve it.

For example:

- gentle text reveals
- subtle section transitions
- restrained image movement
- small editorial details
- carefully designed progress cues if they are actually useful

Animation should support the story, not become the story.

Do not add interactions simply because they are technically impressive.

## Accessibility

Make the experience usable and accessible.

Include:

- semantic HTML
- proper heading hierarchy
- useful alt text where appropriate
- sufficient text contrast
- keyboard-safe interaction
- no critical information that only exists inside animation
- reduced-motion support

## Implementation Quality

Inspect the existing project structure before making changes.

Reuse the project's current stack where reasonable.

Do not rewrite the project unnecessarily.

Keep the implementation:

- maintainable
- performant
- responsive
- clean
- understandable
- free from unnecessary dependencies

If frame dimensions or aspect ratios vary, handle them deliberately rather than allowing layout shifts.

The scroll sequence must not cause cumulative layout shift.

## Final Verification

Do not stop after writing the code.

Run the actual website and inspect it in a real browser.

Verify at minimum:

### Desktop
- Hero composition
- scroll forward
- scroll backward
- frame continuity
- text layering
- image cropping
- performance
- transitions
- content after the Hero

### Mobile
- portrait layout
- Hero crop
- touch scrolling
- text readability
- frame performance
- memory behavior
- spacing
- reduced viewport height cases

Also verify the reduced-motion version.

Fix visible problems you discover before considering the task complete. Report what you actually tested, the command used to run the website, and any remaining limitations. If you cannot run the app or access a browser, state that clearly; do not claim that browser verification passed.

The final result should feel like a carefully art-directed **Japanese travel editorial transformed into an interactive web experience**, not a technology demo and not an AI-generated landing-page template.

The cinematic frame sequence is the centerpiece.

Everything else should exist to support the food, the photograph, and the memory.
```

