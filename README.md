# PSD Template Compositor

A browser-based tool for compositing images into Photoshop (PSD) templates. Upload your PSD templates, drop in images, add text overlays, and export finished compositions as PNG — all client-side with zero server dependencies.

## **[Launch the Live App](https://scuffedepoch.com/psd-templating/)**

---

## Features

- **PSD Template Parsing** — Upload `.psd` files with named layers. The system automatically detects subject slots, text regions, and background layers using the `cf_` naming convention.
- **Image Gallery** — Upload JPEG, PNG, WebP, or GIF images. Tag, filter, and multi-select images for batch composition.
- **Smart Scaling** — Source images are never cropped or distorted. The template automatically upscales to accommodate larger images, maintaining 100px of visible background framing on every edge.
- **Text Overlays** — Templates can include replaceable title and caption text layers. Enter custom text at export time and it renders directly onto the composition.
- **Export to PNG** — Compose and download finished images. Save exports to a local history for later re-download.
- **Fully Client-Side** — Everything runs in your browser. No uploads to any server. Images and templates are stored in IndexedDB.
- **Dark Theme** — Bronze dark UI with teal accents. Colorblind-safe palette throughout.

---

## Creating PSD Templates

The app includes a built-in **Guide** page with detailed, step-by-step instructions for creating both single-image and multi-image PSD templates. Access it from the Guide tab in the app navigation.

### Layer Naming Convention

The system recognises layers with the `cf_` prefix:

| Layer Name | Purpose |
|---|---|
| `cf_background` | Base background layer — rendered behind everything |
| `cf_subject_1` | First image slot (required) |
| `cf_subject_2`, `cf_subject_3`, ... | Additional image slots for multi-image templates |
| `cf_text_title` | Replaceable title text region (optional) |
| `cf_text_caption` | Replaceable caption text region (optional) |

### Quick Start

1. **Create a new PSD** at your chosen aspect ratio (e.g. 954×1272 for 3:4 portrait)
2. **Add a `cf_background` layer** with your background design (gradient, pattern, artwork)
3. **Create an empty layer** named `cf_subject_1` — position it above the background in the layer stack
4. **(Optional)** Add `cf_text_title` and `cf_text_caption` text layers with placeholder text
5. **(Optional)** For multi-image layouts, add `cf_subject_2`, `cf_subject_3`, etc.
6. **Save as `.psd`** with layers intact (do not flatten)
7. **Upload to the app** via the Templates tab and test with sample images

### Example Layer Stack (bottom to top)

```
cf_background          ← your background design
Gradient Fill 1        ← any decorative layers (name freely)
cf_subject_1           ← empty placeholder for user image
Border overlay         ← decorative elements on top
cf_text_title          ← replaceable title text
cf_text_caption        ← replaceable caption text
```

### How Scaling Works

1. Source images are decoded at **full native resolution** — never cropped or distorted
2. The template canvas is **uniformly upscaled** so the source image fits inside with 100px of padding on every edge
3. All template layers scale proportionally to fill the larger output canvas
4. The source image is **contain-fitted** and centred within the padded region

### Design Tips

- **Bold backgrounds** work best — gradients, textures, and high-contrast designs remain striking even as a thin border frame
- **Place text layers near edges** — these areas are guaranteed visible as part of the frame padding
- **Use high-contrast text colours** — white on dark or black on light for readability
- **Design at 1000-2000px** on the longest side — the output upscales automatically for larger source images
- **Rasterize effects before saving** — layer styles, adjustment layers, and smart objects should be flattened. The compositor reads raw pixel data, not live effects

---

## Example Templates

This repository includes reference PSD templates for testing:

- `3-4-template.psd` — 3:4 portrait aspect ratio (954×1272)
- `4-3-template.psd` — 4:3 landscape aspect ratio (1696×1272)

These use the `cf_` layer naming convention and include background layers, a subject slot, and text overlays.

---

## Running Locally

```bash
cd psd-template-demo
npm install
npm run dev        # Development server at http://localhost:5173
npm run build      # Production build to dist/
```

### Tech Stack

- **Vite** + **React** + **TypeScript**
- **ag-psd** for PSD file parsing and layer data extraction
- **IndexedDB** for client-side storage of images, templates, and export history
- **OffscreenCanvas** for GPU-accelerated image composition

---

## 📚 Citation

### Academic Citation

If you use this codebase in your research or project, please cite:

```bibtex
@software{psd_template_compositor,
  title = {PSD Template Compositor: Browser-based PSD template composition tool},
  author = {Drift Johnson},
  year = {2025},
  url = {https://github.com/MushroomFleet/psd-templating},
  version = {1.0.0}
}
```

### Donate:

[![Ko-Fi](https://cdn.ko-fi.com/cdn/kofi3.png?v=3)](https://ko-fi.com/driftjohnson)
