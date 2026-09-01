# Output Format

Return Markdown. Output only the platforms requested, in the requested order. If the user gives no order, use Instagram, Facebook, Threads, then Telegram.

Omit optional sections that add no value. Do not print empty headings, internal analysis, the Source Brief, or the pre-flight checklist unless requested.

## Instagram

````markdown
## Instagram

### Caption

...

### CTA

...

### Hashtags

...

### Optional Carousel Outline

...

### Image Direction

...

### Nano Banana 2 Prompt

```text
...
```

### ChatGPT Images 2.0 Prompt

```text
...
```
````

Keep `Hashtags` and `Optional Carousel Outline` optional.
Keep all three image fields together. Include them by default unless the user opts out.

## Facebook

```markdown
## Facebook

### Post

...

### CTA

...
```

## Threads

For a single post:

```markdown
## Threads

### Post

...
```

For a thread, replace `Post` with `Thread` and separate each numbered entry.

When an image materially supports the Threads angle, append all three image fields after the post or thread:

````markdown
### Image Direction

...

### Nano Banana 2 Prompt

```text
...
```

### ChatGPT Images 2.0 Prompt

```text
...
```
````

Omit all three fields when the image has no clear job. Never print an explanation or empty image heading.

## Telegram

```markdown
## Telegram

### Message

...

### Link Placement Recommendation

...
```

## Source-safe formatting

- Include a URL only when the user supplied it or the readable source exposed it.
- Keep links exactly as supplied unless the user requests tracking parameters.
- Do not imply that a profile, bio, comment, or channel contains a link unless the user confirms it.
- Put a CTA in its platform field when the format defines one; do not repeat it word for word in the post.
- Put copy-ready image prompts in `text` code fences. Do not add commentary inside the fences.
- Keep the provider prompts standalone and complete; never use placeholders or refer to the other prompt.
