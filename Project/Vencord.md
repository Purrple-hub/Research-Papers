# Vencord

> The cutest Discord client mod 🎀

**Vencord** is a lightweight, feature-rich Discord client modification that enhances your Discord experience with over 100 built-in plugins, custom CSS and theme support, and a strong commitment to privacy. Whether you're using the desktop app or your favorite browser, Vencord makes Discord more customizable, functional, and fun.

---

## 📋 Project Description

Vencord is a Discord client mod designed to be **easy to install**, **user‑friendly**, and **actively maintained**. It comes with all plugins preinstalled—just enable what you like and you're done. The project prioritizes privacy by blocking Discord's analytics and crash reporting out of the box, with zero telemetry of its own.

With a flexible and robust plugin system, Vencord empowers both users and developers to customize their Discord experience to their heart's content.

---

## ✨ Features

- **🚀 Super Easy Installation** — Download the graphical installer, open it, click the install button, and you're done.
- **🧩 100+ Built‑in Plugins** — A vast library of plugins comes preinstalled; just toggle the ones you want.
- **⚡ Lightweight** — Surprisingly lightweight despite the many built‑in plugins.
- **🌐 Excellent Browser Support** — Works just as well inside your favorite browser as it does on desktop.
- **💻 Works on Any Discord Branch** — Compatible with Stable, PTB, Canary, and more.
- **🎨 Custom CSS & Themes** — Built-in CSS editor with support for importing any CSS files, including BetterDiscord themes.
- **🔒 Privacy Friendly** — Blocks Discord analytics and crash reporting out of the box. No telemetry, ever.
- **🛠️ Developer Friendly** — Flexible plugin system with extensive APIs, making it easy to build and share your own plugins.
- **🔧 Actively Maintained** — Bugs are typically fixed within a day; no more broken plugins.

---

## 🚀 Quick Start

1. **Close Discord** completely (including from the system tray).
2. Download the installer from [https://vencord.dev/download](https://vencord.dev/download).
3. Run the installer and select your Discord client (usually **Stable**).
4. Click **Install** and wait for the process to complete.
5. Launch Discord — you'll now see a **Vencord Settings** tab in your Discord settings menu.

> 💡 **Tip:** For the web version, Vencord works seamlessly inside your browser without additional setup.

---

## 📦 Installation

### Windows

Download the official installer from the [releases page](https://github.com/Vendicated/Vencord/releases) or use the direct link:

```
https://github.com/Vencord/Installer/releases/latest/download/VencordInstaller.exe
```

Run the `.exe` file, select your Discord installation, and click **Install**.

### macOS / Linux

For macOS and Linux, you can build from source or use community-supported installation methods. Refer to the [official documentation](https://vencord.dev) for the latest instructions.

### Building from Source

If you prefer to build from source, you'll need **Node.js** (LTS recommended) and **pnpm**:

```bash
git clone https://github.com/Vendicated/Vencord.git
cd Vencord
pnpm install
pnpm build
```

Then run Vencord's official installer to inject the built files.

---

## ⚙️ Configuration

Once installed, open Discord and navigate to **User Settings** → **Vencord Settings**. From there, you can:

- **Enable/Disable Plugins** — Browse the full list of built‑in plugins and toggle them on or off.
- **Configure Plugin Options** — Many plugins offer additional settings; adjust them to your liking.
- **Custom CSS** — Use the built‑in CSS editor to apply your own styles or import BetterDiscord themes.
- **Manage Themes** — Import and switch between CSS themes effortlessly.

### Example: Enabling a Plugin

1. Open **Discord Settings** → **Vencord Settings**.
2. Navigate to the **Plugins** tab.
3. Find the plugin you want (e.g., `SpotifyControls`, `MessageLogger`, `Translate`, `NoTrack`).
4. Toggle the switch to enable it.
5. The plugin is now active — no restart required!

---

## 💻 Usage Examples

### Custom CSS

Vencord includes a full-featured CSS editor. To apply a custom theme:

1. Go to **Vencord Settings** → **CSS**.
2. Paste your CSS code or import a `.css` file.
3. Changes apply instantly.

### Plugin Highlights

| Plugin | Description |
|--------|-------------|
| **SpotifyControls** | Enhanced Spotify integration and controls. |
| **MessageLogger** | Log deleted and edited messages. |
| **Experiments** | Access Discord's experimental features. |
| **Translate** | In‑chat message translation. |
| **NoTrack** | Blocks Discord analytics and tracking. |
| **QuickReply** | Quick reply shortcuts. |
| **Free Emotes/Stickers** | Use emotes and stickers without Nitro. |
| **ShowHiddenChannels** | Reveals hidden channels. |
| **PronounDB** | Display pronouns from PronounDB. |

---

## 🧪 Running Tests

For developers who want to run the test suite:

```bash
# Install dependencies
pnpm install

# Run tests
pnpm test
```

Make sure you have the latest Node.js LTS version installed before running tests.

---

## 📝 Contributing

Contributions are welcome and encouraged! Here's how you can get involved:

### Reporting Issues

- Check the [existing issues](https://github.com/Vendicated/Vencord/issues) to avoid duplicates.
- Provide as much detail as possible: steps to reproduce, expected vs. actual behavior, and your environment.

### Developing Plugins

Vencord's plugin system is flexible and well-documented. To create your own plugin:

1. Fork the repository.
2. Add your plugin to the `src/plugins/` directory.
3. Follow the existing plugin patterns and use the provided APIs.
4. Submit a pull request with your plugin.

### Pull Request Guidelines

- Keep code clean and well‑commented.
- Ensure your changes don't break existing functionality.
- Update the README if you add significant new features.
- Be responsive to feedback during the review process.

### Community

Join the [Vencord Support/Community Server](https://vencord.dev) for help, discussion, and updates.

---

## 📄 License

Vencord is open‑source software. Please refer to the [LICENSE](https://github.com/Vendicated/Vencord/blob/main/LICENSE) file in the repository for the full licensing terms.

---

<div align="center">
  <sub>Built with ❤️ by the Vencord community</sub>
</div>
