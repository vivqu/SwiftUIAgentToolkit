---
name: placeholder-ui
description: Guide for populating SwiftUI prototype screens with bundled placeholder images and SF Symbol icons. Use when building any screen that needs realistic-looking placeholder content — avatars, product cards, hero images, etc.
---

# Placeholder UI Assets

Use this skill whenever you're building a prototype screen that needs images. Prefer bundled assets over network calls — they work offline, load instantly, and are semantically appropriate.

## Decision guide

| Need | Approach |
| --- | --- |
| Person / avatar | Bundled avatar — ask user which style (see Step 1) |
| Product card | Bundled product image (`product-1` to `product-10`) |
| Hero / banner | Bundled hero image (nature or architecture subcategory) |
| Background / decorative | Bundled abstract image (`abstract-1` to `abstract-6`) |
| Category or action indicator | SF Symbol (see reference below) |
| Loading / skeleton state | `.redacted(reason: .placeholder)` |

## Step 1 — Discover available images

Read `assets/placeholder-images/README.md` — it lists every available image by category with filenames and descriptions.

If a category has no images yet, use the picsum fallback (see Step 3).

### When multiple styles exist for a category, ask the user

After reading the README, if the category has more than one style (e.g. avatars have both **illustrated** and **photo** variants), pause and ask the user which style they prefer before proceeding. For example:

> There are two avatar styles available:
>
> - **Illustrated** (`avatar-illustrated-1` to `avatar-illustrated-6`) — cartoon personas
> - **Photo** (`avatar-1` to `avatar-6`) — realistic portraits
>
> Which style would you like to use?

Do not pick a style silently — the choice affects the visual tone of the whole screen.

## Step 2 — Import into Assets.xcassets

For each image you want to use:

1. Glob for `*.xcassets` in the project directory to find the asset catalog
2. Create an `.imageset` folder named after the image (without extension):

   ```none
   YourApp/Assets.xcassets/placeholder-avatar-illustrated-1.imageset/
   ```

3. Copy the source image into that folder:

   ```bash
   cp assets/placeholder-images/avatars/avatar-illustrated-1.png \
      YourApp/Assets.xcassets/avatar-illustrated-1.imageset/
   ```

4. Write `Contents.json` in the imageset folder using the template at `references/imageset-contents.json`, substituting the actual filename

Repeat for each image needed. The project uses `PBXFileSystemSynchronizedRootGroup` so no changes to `project.pbxproj` are required — Xcode picks up new `.imageset` folders automatically.

## Step 3 — SwiftUI usage

```swift
// Bundled image
Image("avatar-illustrated-1")
    .resizable()
    .aspectRatio(contentMode: .fill)

// Bundled avatar in a circle
Image("avatar-illustrated-1")
    .resizable()
    .aspectRatio(contentMode: .fill)
    .frame(width: 80, height: 80)
    .clipShape(Circle())

// Fallback: picsum (network — use when no bundled image fits the category)
AsyncImage(url: URL(string: "https://picsum.photos/seed/UNIQUE_SEED/300/300")!) { image in
    image.resizable().aspectRatio(contentMode: .fill)
} placeholder: {
    Color(.systemGray5)
}

// Skeleton / loading state
RoundedRectangle(cornerRadius: 12)
    .fill(Color(.systemGray5))
    .redacted(reason: .placeholder)
```

## SF Symbols reference

Common needs in prototype UI:

| Use case         | Symbol name        |
|------------------|--------------------|
| User / avatar    | `person.circle.fill` |
| Location         | `location.fill`    |
| Photo            | `photo`            |
| Clothing         | `tshirt`           |
| Electronics      | `laptopcomputer`   |
| Books            | `book`             |
| Food             | `fork.knife`       |
| Sports           | `figure.run`       |
| Home             | `house`            |
| Beauty           | `sparkles`         |
| Toys / games     | `gamecontroller`   |
| Settings         | `gearshape`        |
| Notifications    | `bell`             |
| Search           | `magnifyingglass`  |
| Favorites        | `heart`            |
| Shopping         | `bag`              |
| Star / rating    | `star.fill`        |
| Calendar         | `calendar`         |
| Map              | `map`              |
| Camera           | `camera`           |
