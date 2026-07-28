# Plan asset contract

## Never crop a plan

For every `unit.*` media slot:

- set `defaultFit: "contain"`;
- set `allowedFits: ["contain"]`;
- center the image;
- preserve the decoded aspect ratio;
- render the complete drawing inside a neutral, high-contrast canvas;
- keep useful padding without sacrificing labels at narrow widths.

Do not use `cover`, negative offsets, mask/clip paths, or a transform that pushes drawing content outside the canvas. `overflow: hidden` is acceptable only when the contained image and animation remain entirely inside.

## Inspect before changing

Read actual image metadata; do not trust a filename or remembered size. Compare the decoded size with `DEFAULT_MEDIA_DIMENSIONS` and the component's width/height props. Check whether apparent “cropping” is:

- CSS object fitting;
- a parent with constrained height;
- transform animation at an edge;
- internal whitespace in the source;
- content already cut off inside the uploaded bitmap;
- an administrator-selected asset with an unexpected aspect ratio.

CSS cannot restore pixels missing from the source.

## Accessible content

Use concise factual alt text such as “장성 바울루체 84A 타입 평면도”. Keep the active plan associated with its visible unit heading and facts. Do not repeat marketing copy in alt text or hide an informative plan from assistive technology.

Under reduced motion, remove the plan entrance transform. Ensure 200% zoom and narrow mobile preserve the full drawing and readable surrounding facts without horizontal page overflow.
