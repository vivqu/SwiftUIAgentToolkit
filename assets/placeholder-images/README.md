# Placeholder Images

Curated images for use in Swift prototypes. Drop images into the appropriate category folder and follow the naming convention below.

## Naming convention

| Category | Names | Count | Use for |
| -------- | ----- | ----- | ------- |
| Avatar / portrait (illustrated) | `placeholder-avatar-illustrated-1.png` … `placeholder-avatar-illustrated-6.png` | 6 | Profile photos, user avatars, social UI |
| Avatar / portrait (photo) | `placeholder-avatar-1.jpg` … `placeholder-avatar-3.jpg` | 3 | Realistic profile photos, social UI |
| Product | `placeholder-product-1.jpg` … | 0 | Product cards, shop listings — use picsum fallback until populated |
| Hero / banner | `placeholder-hero-1.jpg` … | 0 | Full-width headers, feature banners — use picsum fallback until populated |
| Abstract / background | `placeholder-abstract-1.jpg` … | 0 | Decorative backgrounds, cards — use picsum fallback until populated |

## Rules

- **Format:** JPEG or PNG, square or landscape crops preferred
- **Resolution:** At least 600×600px so they look sharp on 3× displays

## Sources

- **Avatars:** Illustrated personas from [Personas by Draftbit](https://personas.draftbit.com/)

## Optimization

Images have been minified using [TinyPNG](https://tinypng.com/).

## Folders

```none
assets/placeholder-images/
├── avatars/      ← illustrated + photo portrait images
├── products/     ← product card images (empty — use picsum fallback)
├── heroes/       ← full-width banner images (empty — use picsum fallback)
└── abstracts/    ← decorative background images (empty — use picsum fallback)
```
