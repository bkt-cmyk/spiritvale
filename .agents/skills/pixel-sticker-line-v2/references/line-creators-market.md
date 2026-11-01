# LINE Creators Market Requirements

Use this reference whenever creating, exporting, or reviewing a LINE sticker set. These requirements were checked against the official English LINE Creators Market pages on 2026-10-17. The official pages may change; re-check the selected product's current guide before final submission when internet access is available.

## Choose the Product First

This reference contains requirements for:

- Static stickers
- Animated stickers
- Review-readiness shared by sticker products

Do not apply these dimensions or animation limits to Custom, Message, Big, Pop-up, Effect, emoji, or theme products. Consult the current official guide for that exact product.

## Static Stickers

### Required images

| Asset | Quantity | Canvas limit | Format and size |
|---|---:|---:|---|
| Main image | 1 | Exactly 240 x 240 px | PNG, 1 MB or less |
| Sticker images | 8, 16, 24, 32, or 40 | Maximum 370 x 320 px each | PNG, 1 MB or less each |
| Chat thumbnail icon | 1 | Exactly 96 x 74 px | PNG, 1 MB or less |

### Technical rules

- Use PNG for every image.
- Use RGB color mode and a resolution of at least 72 dpi.
- Use a transparent background.
- Sticker image width and height must both be even numbers because LINE resizes them automatically.
- Keep the complete ZIP at 60 MB or less when uploading as one archive.
- Leave about 10 px between the trimmed image bounds and the visible content, while maintaining balanced composition.

For pixel art, start from a smaller logical grid only when the final artwork can be enlarged with nearest-neighbor at a whole-number scale. Validate the actual exported pixel dimensions, not just the source grid.

## Animated Stickers

### Required images

| Asset | Quantity | Canvas limit | Format and size |
|---|---:|---:|---|
| Main image | 1 | Exactly 240 x 240 px | APNG with `.png` extension, 1 MB or less |
| Animated sticker images | 8, 16, or 24 | Maximum 320 x 270 px each | APNG with `.png` extension, 1 MB or less each |
| Chat thumbnail icon | 1 | Exactly 96 x 74 px | PNG, 1 MB or less |

### Dimensions and files

- Each animated sticker must fit within 320 x 270 px.
- Either its width or its height must be at least 270 px. If width is below 270 px, height must be at least 270 px; if height is below 270 px, width must be at least 270 px.
- Use RGB color mode and a transparent background.
- Keep the complete ZIP at 60 MB or less when uploading as one archive.
- Do not draw a play symbol on the chat thumbnail; LINE adds it automatically.
- Trim non-animated empty areas rather than carrying a needlessly large transparent canvas.

### Frames, time, and loops

- Use 5 to 20 PNG frames per APNG.
- Choose an individual playback duration of exactly 1, 2, 3, or 4 seconds.
- Use 1 to 4 loops.
- Playback duration multiplied by loop count must not exceed 4 seconds total.
- Do not submit an APNG whose frames all contain identical data; it will not animate correctly and can fail upload.
- Beware that APNG tools may combine repeated identical frames, reducing the effective frame count.

### Still-image behavior

The first APNG frame is used as the static representation in the Sticker Shop, LINE STORE, unsupported contexts, and whenever animation is not playing. Make frame 1 clearly communicate the sticker's main emotion or idea, even if that requires duplicating a later key pose as the first frame.

For pixel animation, prefer flat colors, a restricted palette, localized motion, and recycled frames where appropriate. These choices preserve pixel clarity and reduce APNG size.

## Text Metadata

These limits apply to both static and animated stickers:

| Field | Maximum |
|---|---:|
| Sticker title | 40 characters |
| Creator name | 50 characters |
| Sticker description | 160 characters |
| Copyright | 50 characters |

Asian-language characters and some symbols count as two characters. Validate within LINE Creators Market rather than relying only on ordinary string length.

Review all metadata for spelling, consistency with the images, and prohibited promotional content. Do not put URLs or device-dependent emoji in title or description fields.

## Design and Review Readiness

### Strong candidates

- Easy to use in ordinary conversation.
- Clear expressions, messages, and illustrations.
- Readable at chat size, with sufficient contrast and a compact silhouette.
- A varied set of intents, poses, expressions, and compositions.
- Main image and chat thumbnail accurately represent the submitted sticker set.

### Common rejection risks

- Wrong format, dimensions, quantity, color mode, transparency, file size, frame count, duration, or loop count.
- Poor visibility, overly tall or narrow compositions, or a full-body character that becomes too small to read.
- A set with little variety, including near-duplicates, only pale designs, or number strings.
- Images made only from a logo, or only from text and phrases.
- Spelling mistakes or metadata that conflicts with the images.
- Main or thumbnail images that differ materially from the stickers being sold.
- Duplicates of stickers already on sale or under review.
- Advertising, promotions, release announcements, corporate-logo-only content, URLs, or attempts to collect personal information or IDs.
- References to other messenger apps or similar services and their characters.
- Unlicensed characters, fan art with unclear rights, unauthorized photos or likenesses, or other trademark, copyright, patent, privacy, or publicity-right violations.
- Sexual, graphically violent, hateful, discriminatory, criminal, gambling, substance-abuse, political, religious-solicitation, bullying, self-harm-promoting, phishing, or otherwise antisocial content described by the review guidelines.

Review approval remains discretionary and can vary by content and sales region. Phrase the result as a preflight assessment, not a guarantee.

## Preflight Checklist

### Every set

- [ ] Product type selected before applying specifications.
- [ ] Allowed sticker count used.
- [ ] All required main, sticker, and thumbnail assets present.
- [ ] Every exported file uses the required PNG/APNG format, RGB color mode, and transparency.
- [ ] Every file and the optional ZIP stay within size limits.
- [ ] Character silhouettes, faces, gestures, and text remain readable at 1x.
- [ ] Artwork is checked on light and dark chat-like backgrounds for halos and lost contrast.
- [ ] Set has useful conversational variety and no accidental near-duplicates.
- [ ] Spelling and metadata are checked, and metadata matches the art.
- [ ] Rights to characters, text, logos, photos, fonts, and other incorporated material are documented.
- [ ] Content and business-purpose review risks have been checked.

### Static-only

- [ ] Sticker width and height are even numbers.
- [ ] About 10 px of balanced margin remains around visible content.

### Animated-only

- [ ] Every APNG satisfies the 320 x 270 maximum and the one-side-at-least-270 rule.
- [ ] Every APNG has 5 to 20 effective frames after assembly.
- [ ] Duration is 1, 2, 3, or 4 seconds; loops are 1 to 4; duration multiplied by loops is at most 4 seconds.
- [ ] Frame 1 works as a standalone still image.
- [ ] Empty non-animated margins have been trimmed.
- [ ] Chat thumbnail does not contain a manually drawn play icon.

## Official Sources

- Static stickers: https://creator.line.me/en/guideline/sticker/
- Animated stickers: https://creator.line.me/en/guideline/animationsticker/
- Animated sticker details: https://creator.line.me/en/guideline/animationsticker/detail/
- Sticker review guidelines: https://creator.line.me/en/review_guideline/
- Product guide index: https://creator.line.me/en/guideline/
