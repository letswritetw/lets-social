# Image Prompts

Use this reference only when producing image direction and copy-ready prompts for Instagram or Threads.

## Goal

Give the user a source-grounded visual concept they can paste into Nano Banana 2 or ChatGPT Images 2.0. The skill writes prompts; it does not call either service or create an image.

If the user names other image models, provide one standalone prompt per named model. Keep the two defaults above when the user does not name a model.

## Build one Image Brief per platform

Keep the brief internal. Define:

- The image's job in that platform post
- The chosen style direction and one line on why the source calls for it
- Main subject and supporting elements grounded in the source
- Composition and platform format
- Visual style, palette, lighting, and mood
- Exact on-image text, or `none`
- Elements and claims to exclude

The Instagram and Threads briefs may differ because each post can use a different angle. Within one platform, both provider prompts must follow the same brief.

## Source and visual integrity

- Start from visible objects, processes, comparisons, or relationships stated in the source.
- For an abstract topic, use an editorial illustration or visual metaphor that readers will not mistake for documentary evidence.
- Treat style, palette, lighting, and composition as creative direction. Do not turn them into factual claims.
- Do not invent charts, measurements, quotations, citations, product screens, logos, awards, people, or outcomes.
- Do not imitate a named living artist. Describe the visual qualities instead.
- On-image text is required by default and must be quoted exactly in the prompt. Every word must be supported by the source. Request that the model render only those exact strings and no other lettering.

## Choose a visual style that fits the source

Do not reuse one house style for every article. Pick the style direction from what the source actually is, name it in the Image Brief with one line on why it fits, and apply it consistently across both provider prompts and every image in a series.

If the user names a style, that wins. Otherwise choose from directions like these, or describe a better one the source suggests:

- **Handwritten-digital knowledge card** — checklists, evaluation criteria, how-to steps. Clean background, precise heavy sans headline, handwritten English accents, highlighter and marker markup.
- **Editorial diagram** — architecture, data flow, request lifecycles, before-and-after comparisons. Hand-inked nodes and directional connectors, each node drawn as its own object rather than a repeated box, arrows with wobble and weight.
- **Bold typographic poster** — one strong opinion or a single counterintuitive claim. Oversized type as the subject, one dominant color field, minimal illustration.
- **Retro terminal or blueprint** — low-level engineering, tooling, protocols, debugging. Monospaced accents, grid or scanline texture, restrained palette with one bright signal color.
- **Soft illustrated scene** — team process, career, workflow, decision-making. Rounded figures and objects, warm palette, light narrative staging.

Selection cues: a process or comparison wants a diagram; a list of criteria wants a card; a single provocative claim wants a poster; a hands-on engineering piece wants the terminal or blueprint look; a people-and-process piece wants a scene.

### What holds in every style

Whatever direction is chosen, every prompt must still specify:

- A palette of at least four colors used with intent, unless the user asked for a deliberately monochrome look. Say which color does what.
- The source-grounded key points written on the image, per the next section.
- Hierarchy: which element reads first, second, and last.
- Enough texture, markup, or structural detail that the image does not read as a bare stock illustration.

### Keep the image alive

The default failure mode is a sterile corporate infographic. The style label is not what causes it; specific phrases in the prompt are. Unless the user asks for a restrained, minimal, or formal look:

**Never write these into a prompt:** `flat vector`, `consistent stroke weight`, `generous whitespace`, `clean and minimal`, `calm professional mood`, `simple geometric shapes`, `subtle drop shadow`. Each one instructs the model to strip out personality.

**Write these instead.** Every prompt must name at least four:

- **Line with character.** Hand-drawn ink with uneven weight, visible wobble, corners that overshoot — or another line quality with a stated personality. Never a uniform vector stroke.
- **A broken grid.** Elements tilted a few degrees, sizes deliberately unequal, at least two elements overlapping. Never a centered symmetric grid.
- **Print or media texture.** Paper grain, halftone dots, risograph misregistration where color fills sit a few pixels off their outlines, marker bleed. Say which one.
- **Motion marks.** Speed lines, sparkles, hand-circled emphasis, underline swipes, and arrows drawn to spec. Every arrow is short, runs straight or on a single gentle arc, has a thick shaft, and ends in a solid filled triangular head clearly wider than the shaft. Never ask for wobbly, squiggly, serpentine, curling, or multi-curve arrows, and never thin trailing lines: they render as strands of hair. Hand feel comes from uneven pressure along the shaft and a few degrees of tilt, never from bending the path.
- **One concrete subject per image.** A real object, scene, hand, or small character. A slide holding one empty rounded rectangle and one line of text reads as dead space no matter how it is styled.
- **Type that moves.** Sharp size contrast between headline and support, a marker swipe behind one word, one element crossing a text baseline. The clean-sans CJK rule below still holds; legibility is not what makes an image stiff.

**No human hands, faces, or figures.** Image models render them into uncanny-valley territory — extra fingers, melted knuckles, dead eyes — and one bad hand sinks an otherwise good image. This holds in every style, exactly like the CJK typography rule below. When a hand would have carried the action (pointing, pushing, holding, blocking, tapping), use something else that does the same job: a wobbly arrow with speed lines, a hovering object mid-motion, a stamp, a cursor, a dashed outline, or a fully abstract mascot with no human anatomy. If the source genuinely requires a person, keep them small, back-turned, or reduced to a flat silhouette with no fingers or facial features, and say so explicitly in the prompt.

**Repeated shapes must differ.** When the source has several parallel items — four platforms, three steps, five criteria — give each its own icon, tilt, and accent color. Drawing them as identical boxes contradicts a source whose whole point is that the items are not the same.

### Typography rule that keeps text legible

Image models garble handwritten CJK. This rule survives every style:

- Every Chinese, Japanese, or Korean string must be requested as clean, precise sans-serif type, bold enough to read at phone size. Never ask for handwritten, brush, calligraphic, or distressed CJK.
- Decorative or handwritten treatment applies only to short English phrases, two to four words each, and only when the chosen style calls for them.
- State this split explicitly in both provider prompts. Do not leave the font style implied.

## On-image key points

Extract the key points from the source and write them into the prompt as exact strings:

- One headline, up to twelve characters in Chinese or six words in English.
- On the cover only — the single image, or image 1 of a series — one line that identifies what is being promoted, set smaller than the headline and placed above it. Use the source's title when it is short enough to render; otherwise use the named subject the article is about (the tool, product, or skill name) or a shortened title that keeps the original meaning, capped at sixteen Chinese characters or eight English words. A Latin name renders far more reliably than a long CJK title. Never repeat this line on the other images in a series — once is identification, every image is a watermark, and each extra string is another chance for the model to garble text.
- Three to five key-point lines, each up to sixteen characters in Chinese or eight words in English, each mapped to one block or region of the layout.
- One optional closing takeaway line.
- One to three short English atmosphere phrases, two to four words each, when the chosen style uses them. They are decoration, so they must stay generic and must not carry a claim.
- List every string explicitly in the prompt, state where each one goes, and instruct the model to render no other text, no lorem, and no decorative fake lettering.
- Keep the strings short and few. Image models garble long text, and CJK characters degrade fastest, so fewer and shorter strings produce cleaner output.
- The strings are claims. They must restate the source, never add numbers, results, or guarantees the source does not state.

## Platform decisions

### Instagram

Create one 4:5 portrait feed visual by default, in the style chosen for this source. It should stop the scroll and let a reader grasp the caption's key points from the image alone. Colorful and information-rich is the target; keep every string legible at phone size.

When the output includes an optional carousel outline, the default prompts create the carousel cover. The ChatGPT Images 2.0 prompt renders the cover and the slides as one numbered series, so a carousel outline maps directly onto its images.

### Threads

Create an image only when it clarifies or strengthens the selected observation. A decorative image is not enough. Do not reuse the Instagram concept unless the user asks for one cross-platform asset.

Use a format suited to the selected visual. State the aspect ratio in both prompts. Threads visuals use the same style chosen for the source but carry fewer key-point lines, usually two or three.

## Copy-ready prompt contract

Write each prompt in the post's language unless the user requests another language. Preserve technical terms when translating them would reduce accuracy.

Each prompt must stand alone and include:

1. The image to create and its communication goal
2. Aspect ratio, composition, and focal hierarchy
3. Subject, setting, and source-grounded supporting details
4. The chosen style, palette, and mood, including the named colors and the font split between clean sans CJK and any decorative English
5. Every exact on-image string with its placement, plus exclusions

Replace every variable with actual content. Do not use brackets, placeholders, "same as above," or instructions that depend on the article being visible to the image model.

The Nano Banana 2 and ChatGPT Images 2.0 prompts may phrase instructions differently, but they must not change the subject, claim, on-image text, or composition.

### ChatGPT Images 2.0 renders a series

ChatGPT Images 2.0 returns up to ten images from one prompt, and each image can carry different content. Its prompt therefore describes a numbered series that walks through the article, not repeated takes on one card.

- Image 1 is the cover: the headline, the hook, and the strongest visual element.
- Each following image covers one key point, with its own on-image strings, its own supporting visual, and its own accent color from the shared palette.
- An optional final image carries the takeaway or the call to read the article.
- Default to the cover plus three to five key points, so four to six images. Follow the carousel outline instead when the Instagram output includes one. Never request more than ten.
- Lock the chosen style across the series: same background, same palette, same font rule, same visual vocabulary, so the images read as one set. Only the content changes.
- List every image by number, and under each number list its exact on-image strings. Every string is still bound by the source-integrity rules, so a series must not stretch the article into points it does not make.
- Nano Banana 2 keeps its single-image prompt and matches image 1.

If the user asks for a single ChatGPT image, request image 1 alone and drop the rest of the series.

## Pre-flight

- The user can paste either prompt without adding context.
- Both prompts would create recognizably equivalent images. For a series, the comparison is the ChatGPT cover image.
- The visual supports its platform post instead of summarizing the whole article.
- No prompt asks the model to fabricate proof, interface details, or unreadable decorative text.
- The prompt names the chosen style, at least four colors, its structural or textural detail, the CJK font rule, and every on-image string verbatim.
- Every on-image string is short enough to render cleanly and is supported by the source.
