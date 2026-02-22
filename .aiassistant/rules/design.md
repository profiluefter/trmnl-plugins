---
apply: always
---

## Skill: Designing TRMNL Plugins with the TRMNL Framework (Design System)

### What you’re building
TRMNL plugins are essentially **templates** (commonly HTML + Liquid) that get rendered to a **device-constrained e‑ink UI**. The TRMNL Framework gives you a **design system + utility class toolkit** so your layouts stay consistent across:

- **screen sizes** (`sm`, `md`, `lg`)
- **orientation** (`portrait`, etc.)
- **bit-depth / grayscale capability** (`1bit`, `2bit`, `4bit`)

### Where to find the official docs (Context7)
This TRMNL Framework design system documentation is available in Context7 under the library ID:

- **`/websites/trmnl_framework`**

(That’s the ID you’d reference when retrieving up-to-date docs/snippets.)

---

## Core mental model (how to design correctly)

### 1) Compose UI from “components” + “utilities”
You’ll typically structure a screen using:
- **Layout primitives**: `grid`, `flex`, `table`
- **Text primitives**: `label`, `description`, `content` (rich text)
- **Spacing utilities**: padding/margins + gaps (consistent rhythm)

The goal is **predictable, tokenized styling** rather than custom CSS per plugin.

---

## Common TRMNL Framework classes you’ll use all the time

### Layout + display utilities
Use these to control structure and flow:

- Display/visibility: `hidden`, `visible`, `block`, `inline`, `inline-block`, `flex`, `grid`, `table`
- Responsive display changes (mobile-first overrides):  
  - `hidden md:block`
  - `block md:flex`
  - `hidden lg:grid`

### Grid + Flex patterns
- Grid columns: `grid grid--cols-2`, `grid grid--cols-3`, etc.
- Flex direction: `flex flex--col`, `flex flex--row`

### Gap (inter-item spacing) system
TRMNL provides **predefined gap tokens** (super important for e‑ink readability and consistent density):

- `gap--none`, `gap--xsmall`, `gap--small`, `gap` (default), `gap--medium`, `gap--large`, `gap--xlarge`, `gap--xxlarge`
- Responsive gaps: `md:gap--large`, `lg:gap--xlarge`, `portrait:gap--medium`

Example (from the framework’s docs style):
```html
<div class="grid grid--cols-3 gap--small md:gap--large lg:gap--xlarge portrait:gap--medium">
  <div>...</div>
  <div>...</div>
  <div>...</div>
</div>
```


### Spacing utilities (padding)
Spacing uses a consistent `{property}--{size}` pattern:

- `p--{size}`, `pt--{size}`, `pr--{size}`, `pb--{size}`, `pl--{size}`
- `px--{size}`, `py--{size}`
- Works with responsive/orientation prefixes: `sm:px--{size}`, `portrait:pb--{size}`, `md:portrait:pt--{size}`

### Text alignment utilities
For quick alignment changes without custom CSS:

- `text--left`, `text--center`, `text--right`, `text--justify`

---

## “Device-aware” design: the TRMNL superpower

### Responsive prefixes can stack
You can combine constraints like:
- breakpoint (`md`)
- orientation (`portrait`)
- bit-depth (`1bit` / `2bit` / `4bit`)

Example pattern:
```html
<div class="flex flex--row md:portrait:4bit:flex--col">
  ...
</div>
```


### Bit-depth targeting (e‑ink capability)
To optimize for simpler rendering on lower bit-depth displays:

- `1bit:hidden`, `2bit:flex`, `4bit:grid`, etc.

Example:
```html
<div class="1bit:hidden">Hidden on monochrome displays</div>
<div class="2bit:flex">Flex on 4-shade grayscale displays</div>
<div class="4bit:grid">Grid on 16-shade grayscale displays</div>
```


This lets you do **progressive enhancement**:
- 1‑bit: simpler layout, fewer fine details
- 4‑bit: richer layout (more grid, more nuance)

---

## Common “components” (design-system building blocks)

### Label / Description (typography primitives)
These provide consistent hierarchy and spacing:

- Labels: `label`, plus size variants: `label--large`, `label--xlarge`, `label--xxlarge`
- Descriptions: `description`, plus `description--large`, `description--xlarge`, `description--xxlarge`

### Rich Text
Wrap formatted content in:
- `richtext` container
- `content` element with size variants:
  - `content--small`, `content` (default), `content--base`, `content--large`, `content--xlarge`, `content--xxlarge`, `content--xxxlarge`

Responsive example:
```html
<div class="richtext gap--large">
  <div class="content content--base lg:content--xxlarge">
    <p>Readable by default, bigger on large screens</p>
  </div>
</div>
```


### Screen component (device variants)
The framework includes a **Screen component** that supports **device-specific variants** to account for dimensions/scaling/bit-depth differences across TRMNL device generations. Practically: you design with variants in mind so the same plugin can render correctly on multiple devices.

---

## Recommended workflow (practical steps)

1. **Start with structure**: decide whether the screen is mostly `grid`, `flex`, or `table`.
2. **Apply rhythm**: use `gap--*` and padding utilities (`p--{size}`, `px--{size}`) instead of ad-hoc spacing.
3. **Set hierarchy**: use `label`, `description`, and `richtext/content` sizes to control information density.
4. **Add device-awareness**:
   - breakpoints: `md:…`, `lg:…`
   - orientation: `portrait:…`
   - bit-depth: `1bit:…`, `2bit:…`, `4bit:…`
5. **Progressively enhance**:
   - Keep the 1‑bit layout “boring but clear”
   - Upgrade layout complexity for 4‑bit

---

## Mini reference: “common class families” to remember
- **Visibility/Display**: `hidden`, `visible`, `block`, `inline`, `flex`, `grid`, `table` (+ `md:` / `lg:` / `1bit:` etc.)
- **Layout**: `grid--cols-*`, `flex--col`, `flex--row`
- **Spacing**: `gap--*`, `p*--{size}`, `px--{size}`, `py--{size}`
- **Text**: `text--left|center|right|justify`, `label--*`, `description--*`, `content--*`
- **Variants**: stacked prefixes like `md:portrait:4bit:...`
