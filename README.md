# ClearCut

ClearCut is a small, client-side web app that removes image backgrounds in the browser. You upload a photo (JPEG, PNG, or WebP), and the app produces a transparent PNG with the subject cut out—without sending your image to a server.

## How it works

1. On first visit, the app downloads a compact segmentation model and caches it in the browser.
2. After the model is ready, you can pick or drag-and-drop an image (up to **10 MB**).
3. Inference runs locally with **[Transformers.js](https://github.com/xenova/transformers.js)** (v2), using the **`briaai/RMBG-1.4`** model from the Hugging Face hub.
4. The result is drawn to a canvas with an alpha channel; you can download it as PNG.

Because processing stays on your device, ClearCut is suitable when you want to avoid uploading personal or sensitive images to third-party APIs.

## Requirements

- A modern browser with JavaScript modules and support for the features Transformers.js relies on (WebAssembly; see the library docs for details).
- A network connection for the **first** load (model and script are fetched from CDNs). Later visits can reuse cached assets when the browser allows it.

## Running locally

There is no build step. You can:

- Open `index.html` directly in the browser (some environments restrict module loading from `file://`; if something fails, use a local server instead), or  
- Serve the project folder with any static file server, for example:

```bash
npx --yes serve .
```

Then open the URL shown in the terminal.

## Project layout

| File        | Role |
|------------|------|
| `index.html` | Single page: layout, styles, and in-page script that loads the model and runs removal. |
| `ikon.ico`   | Favicon for the tab. |

## UI language

The interface text is in Turkish; this README is in English for broader reuse and documentation.

## Credits

- Background removal model: [briaai/RMBG-1.4](https://huggingface.co/briaai/RMBG-1.4) (check the model card for license and terms).
- Runtime: [@xenova/transformers](https://www.npmjs.com/package/@xenova/transformers) via jsDelivr.
