# Gemini Watermark Remover

> A lightweight, client-side tool for removing visible Google Gemini AI sparkle watermarks from images and videos — with pixel-perfect precision, zero quality loss, and zero server uploads.

---

## 📋 Project Description

**Gemini Watermark Remover** is an open‑source utility that reverses the alpha‑blending process used by Google Gemini (and Nano Banana) to apply its visible ✦ sparkle watermark. Instead of relying on inpainting or generative fill, the tool solves the exact alpha‑compositing equation, recovering the original pixel values that were hidden beneath the mark.

The project is designed to run **100% locally** — in your browser or on your command line — so your generated content never leaves your machine. It supports both **static images** and **Veo video** watermarks, making it a one‑stop solution for cleaning up AI‑generated visuals before sharing, printing, or further editing.

> ⚠️ **Important**: This tool removes the *visible* watermark (sparkle + vendor text) only. It does **not** remove SynthID‑style invisible watermarks, C2PA provenance metadata, or EXIF tags.

---

## ✨ Features

- 🔍 **Mathematically accurate** – reverse alpha blending restores the exact pixels under the watermark, not an approximation.
- 🌐 **100 % client‑side** – no image data is ever uploaded to a server; everything runs in your browser or locally via CLI.
- 🖼️ **Multi‑format support** – works with PNG, JPEG, WebP, and other common image formats; also handles Veo video watermarks.
- ⚡ **Fast & lightweight** – optimized for large images and batch processing.
- 🧪 **Pixel‑perfect reproducibility** – deterministic algorithm ensures consistent results across runs.
- 🛠️ **Dual interface** – use the intuitive web UI or the command‑line tool for scripting and automation.
- 📦 **Zero dependencies** (web version) – pure JavaScript / HTML, no external libraries required.
- 🧩 **Extensible** – easily plug into existing workflows as a library or CLI tool.

---

## 🚀 Quick Start

### Web Version (Online)

1. Visit **[gradually.ai/en/gemini-watermark-remover](https://www.gradually.ai/en/gemini-watermark-remover/)**.
2. Drag & drop your Gemini‑generated image or video onto the drop zone.
3. Click **“Remove Watermark”**.
4. Download the cleaned result instantly — no sign‑up, no installation.

### CLI Version (Local)

```bash
# Install via pip (Python)
pip install gemini-watermark-remover

# Remove watermark from an image
gemini-remove watermark input.png -o output.png
```

---

## 📦 Installation

### Web / Browser
No installation required — the tool runs entirely in your modern browser (Chrome, Firefox, Edge, Safari).

### Python Package (CLI / Library)

```bash
pip install gemini-watermark-remover
```

For the latest development version:

```bash
git clone https://github.com/gradually-ai/gemini-watermark-remover.git
cd gemini-watermark-remover
pip install -e .
```

### Node.js / npm (JavaScript library)

```bash
npm install @gradually-ai/gemini-watermark-remover
```

### Docker (optional)

```bash
docker pull gradually/gemini-watermark-remover
docker run -p 8080:80 gradually/gemini-watermark-remover
```

---

## ⚙️ Configuration

The tool works out‑of‑the‑box with sensible defaults, but you can tweak the following options (CLI / library):

| Option | Description | Default |
|--------|-------------|---------|
| `--alpha-threshold` | Alpha channel threshold for watermark detection | `0.01` |
| `--blend-mode` | Alpha blending mode (`normal`, `multiply`, `screen`) | `normal` |
| `--output-format` | Output image format (`png`, `jpg`, `webp`) | `png` |
| `--quality` | JPEG/WebP compression quality (1–100) | `95` |
| `--preserve-metadata` | Keep EXIF / XMP metadata | `false` |
| `--batch-size` | Number of images to process in parallel (CLI only) | `4` |

### Environment Variables

```bash
# Set default output directory
export GEMINI_OUTPUT_DIR=~/cleaned_images

# Increase memory limit for large videos
export GEMINI_MEMORY_LIMIT=4096
```

---

## 💻 Usage Examples

### Command Line (Python)

```bash
# Single image
gemini-remove watermark photo.jpg -o clean_photo.png

# Batch process all PNGs in a folder
gemini-remove watermark ./images/*.png --output-dir ./cleaned/

# Process a Veo video
gemini-remove watermark video.mp4 -o clean_video.mp4 --video

# With custom alpha threshold
gemini-remove watermark input.png -o output.png --alpha-threshold 0.02
```

### JavaScript / Node.js

```javascript
import { removeWatermark } from '@gradually-ai/gemini-watermark-remover';

const result = await removeWatermark({
  input: 'image.png',
  output: 'cleaned.png',
  alphaThreshold: 0.01,
  blendMode: 'normal'
});

console.log('Watermark removed successfully!');
```

### Python Library

```python
from gemini_watermark_remover import WatermarkRemover

remover = WatermarkRemover()
cleaned_image = remover.remove('input.png')
cleaned_image.save('output.png')
```

### Browser (JavaScript)

```html
<script src="https://cdn.gradually.ai/gemini-watermark-remover/latest/index.js"></script>
<script>
  const fileInput = document.getElementById('imageInput');
  fileInput.addEventListener('change', async (e) => {
    const file = e.target.files[0];
    const result = await GeminiWatermarkRemover.remove(file);
    const link = document.createElement('a');
    link.href = URL.createObjectURL(result);
    link.download = 'cleaned.png';
    link.click();
  });
</script>
```

---

## 🧪 Running Tests

The project includes a comprehensive test suite covering alpha‑blending math, edge cases, and file I/O.

### Python

```bash
# Install test dependencies
pip install -e .[test]

# Run all tests
pytest tests/

# With coverage report
pytest --cov=gemini_watermark_remover tests/
```

### JavaScript / Node.js

```bash
npm install
npm test
```

### Browser Tests

Open `tests/browser/index.html` in your browser to run the QUnit test suite.

---

## 📝 Contributing

We welcome contributions of all kinds — bug reports, feature requests, documentation improvements, and code patches.

### How to Contribute

1. **Fork** the repository on GitHub.
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/your-username/gemini-watermark-remover.git
   ```
3. **Create a branch** for your feature or fix:
   ```bash
   git checkout -b feature/amazing-idea
   ```
4. **Make your changes** — and add tests if applicable.
5. **Run the tests** to ensure nothing breaks.
6. **Commit** with a clear, descriptive message.
7. **Push** to your fork and open a **Pull Request**.

### Development Setup

```bash
# Python
pip install -e .[dev]
pre-commit install

# JavaScript
npm install
npm run build
```

### Coding Standards

- Python: PEP 8, black, isort, flake8
- JavaScript: ESLint + Prettier
- Commit messages: Conventional Commits format

### Reporting Issues

Please use the [GitHub Issues](https://github.com/gradually-ai/gemini-watermark-remover/issues) tracker and include:
- A clear description of the problem
- Steps to reproduce
- Your environment (OS, browser/Node version, etc.)
- Screenshots or sample files if applicable

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2026 Gradually AI

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
...
```

---

## 🙏 Acknowledgements

- Inspired by the reverse‑engineering work of [journey‑ad/gemini‑watermark‑remover](https://github.com/journey-ad/gemini-watermark-remover)
- Built with ❤️ by the Gradually AI team and open‑source contributors

---

## 📬 Contact & Community

- **Website**: [gradually.ai](https://gradually.ai)
- **GitHub**: [github.com/gradually-ai/gemini-watermark-remover](https://github.com/gradually-ai/gemini-watermark-remover)
- **Discord**: [Join our community](https://discord.gg/gradually-ai)
- **Twitter/X**: [@GraduallyAI](https://twitter.com/GraduallyAI)

---

*Made for creators, by creators — because your AI‑generated art should look the way you intended.*
