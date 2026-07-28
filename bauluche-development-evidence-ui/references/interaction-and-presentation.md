# Interaction and presentation

## Desktop

- One `tablist`, one active `tab`, and one labelled `tabpanel`.
- Set `aria-selected`, `aria-controls`, `id`, and `aria-labelledby` consistently.
- Give only the active tab `tabIndex=0`; use `-1` for the others.
- Arrow Left/Up selects the previous item with wrapping.
- Arrow Right/Down selects the next item with wrapping.
- Home selects the first; End selects the last.
- Move focus with selection and preserve an obvious focus indicator.
- Use immediate manual input only; no timer, autoplay, or cycling.

## Mobile

At 900 px and below, show every project as a semantic article in DOM order. Each article contains its image, number, title, qualified status, metrics, summary, and official sources. Links need comfortable touch targets and must not rely on hover.

Keep both layouts rendered only if CSS and accessible visibility are unambiguous. Never leave duplicate interactive controls exposed to assistive technology.

## Premium visual language

Use proportion, serif/sans hierarchy, quiet indexes, fine dividers, dark layered surfaces, generous spacing, and restrained gold accents. Keep proof close to the claim. Avoid glowing badges, oversized card chrome, dense borders, parallax, or salesy callouts.

Restrict image motion to a subtle transition such as at most 600 ms and `scale(1.02)`. Avoid animating factual text or layout. Under `prefers-reduced-motion: reduce`, remove the transition instead of shortening it. Prevent horizontal overflow at every viewport.
