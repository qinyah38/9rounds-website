# How It Works carousel refinement

_Started 2026-06-27 21:30 UTC_

---

## User

How It Works" Mobile Carousel — Refined
Card height:

Increase card height from 420px to 520px so cards feel more immersive and image-forward

Initial peek & position:

First card does NOT start flush with the left edge
Cards container starts with padding-left: 24px but the first card is offset so roughly 85% of card 1 is visible and ~15% of card 2 peeks in from the right
This immediately signals to the user that the content is swipeable — no need for arrows or labels

Active card scaling:

The card currently centered/snapped is full size: width: calc(100vw - 48px), height: 520px
Non-active cards (left and right neighbors) scale down slightly: transform: scale(0.92), opacity: 0.7
As the user swipes and a new card snaps into center, it scales up smoothly to full size while the previous one shrinks
Transition: transform 0.35s ease, opacity 0.35s ease

Scroll snap:

scroll-snap-type: x mandatory on the container
scroll-snap-align: center on each card
scroll-behavior: smooth

Spacing:

Gap between cards: 16px
Right padding on container: 24px so the last card doesn't get clipped awkwardly

Text stays bottom-left on all card sizes — no repositioning during scale

## Assistant

_[tool: grep]_

_[tool: read_file]_

_[tool: grep]_

_[tool: read_file]_

Now I'll refine the mobile carousel. Editing the template and logic:

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Done. The mobile carousel now uses 520px cards with center snapping, the active card at full size and neighbors scaled to 0.92/0.7 opacity, 16px gaps, 24px padding, smooth scroll, and 0.35s transitions. Text stays bottom-left.

## User

"How It Works" Mobile Carousel — Card Height & Peek Fix
Card height:

Increase to 580px — tall enough to feel immersive without overflowing the viewport on small phones

Second card peek from the right:

The goal is exactly like the reference image — active card takes most of the screen, next card peeks visibly from the right edge
First card width: calc(100vw - 72px) — leaves a deliberate ~60px window on the right
That 60px window shows the left edge of card 2, hinting strongly that there's more to swipe
Cards should never be centered — align the active card to the left with padding-left: 24px on the container, so the peek always appears on the right side naturally

Snap behavior:

scroll-snap-type: x mandatory
scroll-snap-align: start (not center) — this keeps the active card left-aligned and the peek consistently on the right, matching the reference image pattern

Scale effect:

Active card: full size, opacity: 1
Peeking card: scale(0.96), opacity: 0.75 — slightly smaller and dimmer so the active card feels dominant
Transition: 0.3s ease

Gap between cards: 12px

## Assistant

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Updated: 580px cards, `calc(100vw - 72px)` width with start alignment so the next card peeks ~60px on the right, scale 0.96 / opacity 0.75 on non-active cards, 12px gap, 0.3s transitions.

## User

Here's the prompt:

Scrolling Image Strip — 9ROUND Logo
Add a full-width horizontally scrolling image strip directly above the "How It Works" section title.
Implementation:

One div with background-image: url('9round-background.webp')
background-repeat: repeat-x — tiles the image horizontally end to end seamlessly
background-size: auto 100% — height is fixed, width tiles naturally with no gaps
Scroll animation via CSS only: @keyframes marquee { from { background-position-x: 0 } to { background-position-x: -500px } } — adjust the pixel value to match the natural width of one image tile
animation: marquee 20s linear infinite

Strip dimensions:

width: 100%
height: 80px
overflow: hidden

Placement:

Sits directly above the "How It Works" heading
margin-bottom: 32px between the strip and the section title
No horizontal padding — bleeds edge to edge intentionally

No JS, no extra markup — single div, pure CSS handles the tiling and motion

## Assistant

_[tool: image_metadata]_

_[tool: read_file]_

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Added a full-bleed 80px strip above the "How it works" heading. The 9ROUND logo tiles seamlessly with `background-repeat: repeat-x` and scrolls left via a pure-CSS `marquee9` keyframe (offset 414px to match one tile at 80px height), with 32px below it before the title.

## User

Add Spacing Between Tiled Logo Instances
Since background-repeat: repeat-x doesn't support gaps natively, switch to the inline image approach instead:
Implementation:

Create a flex container div with overflow: hidden, width: 100%, height: 80px
Inside it, a scrolling inner div with display: flex, align-items: center, width: max-content
Repeat the <img src="9round-background.webp"> tag 10–12 times inside the inner div — enough to fill double the viewport width for seamless looping
Each image: height: 60px, width: auto
Gap between each image: 64px using gap: 64px on the flex container

Animation:

@keyframes marquee { from { transform: translateX(0) } to { transform: translateX(-50%) } }
animation: marquee 25s linear infinite on the inner scrolling div
The -50% works because the images fill exactly double the viewport — first half scrolls out, second half seamlessly takes over

## Assistant

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Switched to 12 inline logo images in a flex strip with 64px gaps, each 60px tall, scrolling via `translateX(-50%)` over 25s for a seamless loop.

## User

Update the footer styling:
Background:

background-color: #C91D22 — 9Round brand red

Text:

All text inside the footer: color: #FFFFFF
This includes nav links, copyright line, address, phone numbers, and any helper text

Links:

color: #FFFFFF
Remove default underline: text-decoration: none
Hover state: opacity: 0.75 — subtle dimming instead of a color change, keeps it clean on red

Icons & dividers:

Any SVG icons inside the footer: fill: #FFFFFF or stroke: #FFFFFF
Divider lines: border-color: rgba(255,255,255,0.25) — soft white, not harsh

Logo in footer:

If the footer contains the 9Round logo, switch to the white version if available — or apply filter: brightness(0) invert(1) to force it white

## Assistant

_[tool: read_file]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Footer is now 9Round red (#C91D22) with white text and links, opacity-0.75 hover, soft white dividers, and the logo forced white via invert. I left the App Store / Google Play badges as black since those are standard brand badges that read fine on red — let me know if you'd like those inverted too.

## User

replace the hero section image with this image

## Assistant

_[tool: grep]_

_[tool: copy_files]_

_[tool: ready_for_verification]_

Replaced the hero image with the new boxer photo.

## User

replace the hero section image with this image

## Assistant

_[tool: copy_files]_

_[tool: ready_for_verification]_

Replaced the hero image with the new photo.

## User

Marquee Strip — Desktop Alignment Fix
The scrolling image strip is not reaching the right edge of the page on desktop. Fix it without touching the mobile layout.
The fix:

The strip container must be width: 100vw not width: 100% on desktop — 100% is constrained by the parent container's max-width, which is why it stops short of the right edge
Use a negative margin trick to break out of the parent container:

css  @media (min-width: 768px) {
    .marquee-strip {
      width: 100vw;
      position: relative;
      left: 50%;
      transform: translateX(-50%);
    }
  }

This pulls the strip full viewport width regardless of what max-width the parent section has, without affecting any other element's layout

Mobile: no changes — keep exactly as is since it already works correctly

## Assistant

_[tool: read_file]_

_[tool: str_replace_edit]_

_[tool: str_replace_edit]_

_[tool: ready_for_verification]_

Fixed. The strip now uses a `.marquee-strip` class — mobile keeps the existing `100vw` margin trick, and desktop (≥768px) uses the `left:50%` + `translateX(-50%)` breakout so it spans the full viewport width regardless of the parent's max-width.

