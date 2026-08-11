# MCStacker

> **The ultimate command generator for Minecraft: Java Edition**

MCStacker is a powerful web-based tool that helps you generate complex Minecraft commands without memorizing NBT syntax, JSON structures, or command formats. Since 2014, it has been the go‑to resource for map makers, server administrators, and command-block enthusiasts who want to create custom items, entities, and blocks with ease.

---

## 📋 Project Description

MCStacker is a command generation tool for **Minecraft: Java Edition** that abstracts away the complexity of raw command syntax. Instead of wrestling with nested NBT tags and component structures, you simply fill out intuitive forms — and MCStacker outputs the exact command you need.

Whether you're summoning a custom mob with full inventory, creating a give command for a perfectly enchanted weapon, or building complex data-driven mechanics, MCStacker handles the heavy lifting. The tool stays current with the latest Minecraft versions, with ongoing development driven by community support.

---

## ✨ Features

### Core Capabilities

- **Command Generation** – Create `/give`, `/summon`, `/setblock`, `/data`, and many other commands through an intuitive form interface
- **NBT & Component Support** – Full support for item components (1.20.5+) and legacy NBT tags, covering even edge‑case combinations
- **Multi‑Version Compatibility** – Supports Minecraft **1.12 and up**, with version‑specific options for each release
- **Saved Commands** – Store and share your command creations directly on the website
- **Theme & Language Options** – Customize the interface with multiple themes and language choices

### Editions

| Feature | Online Edition | Offline Edition | Deluxe Edition |
|---------|---------------|----------------|----------------|
| **Minecraft Versions** | 1.12 and up | 1.13 and up | 1.20 and up |
| **Works Offline** | ❌ No | ✅ Yes | ✅ Yes |
| **Cost** | Free | Patreon ($1+/mo) | One‑time ($10+) |
| **Advertising** | Yes (ad‑free for supporters) | No | No |
| **Command History** | ❌ | ❌ | ✅ |
| **Command List Import/Export** | ❌ | ❌ | ✅ |
| **Import/Output Diff Checker** | ❌ | ❌ | ✅ |
| **Lifetime Updates** | ✅ | ✅ | ✅ |
| **Installable Application** | ❌ | ❌ | ✅ (Win/Mac/Linux) |

*Source: MCStacker official comparison table*

### Deluxe Edition Exclusive Features

- **Command History** – Never lose a command you worked on
- **Command List Import/Export** – Work with `.mcfunction`, `.txt`, or any text format
- **Import/Output Diff Checker** – Identify errors when importing commands
- **Lifetime Updates** – Always stay current

---

## 🚀 Quick Start

The fastest way to start using MCStacker:

1. **Open your browser** and navigate to **[mcstacker.net](https://mcstacker.net/)**
2. **Choose a command type** from the sidebar (e.g., `/give`, `/summon`, `/setblock`)
3. **Fill in the form** with your desired options — items, enchantments, attributes, etc.
4. **Copy the generated command** from the output box
5. **Paste it into Minecraft** (command block, chat, or function file)

That's it — no installation, no setup, no configuration required to get started.

---

## 📦 Installation

### Online Edition (Free)
No installation needed. Simply visit **[mcstacker.net](https://mcstacker.net/)** in any modern browser.

### Offline Edition (Patreon)
1. Become a patron at **[patreon.com/mcstacker](https://www.patreon.com/mcstacker)** ($1+/month)
2. Download the ZIP file containing all HTML documents and assets
3. Extract and open `index.html` in your browser — works without an internet connection

### Deluxe Edition (One‑time Purchase)
1. Purchase at **[Ko‑fi](https://ko-fi.com/s/27510c833f)** ($10+ one‑time)
2. Download the installable package for **Windows, Mac, or Linux**
3. Run the installer and launch MCStacker as a desktop application
4. Enjoy all exclusive features including command history, import/export, and diff checking

---

## ⚙️ Configuration

MCStacker offers several settings to customize your experience:

| Setting | Description |
|---------|-------------|
| **Command Prefix** | Set a custom prefix for generated commands |
| **Update Prefix on Import** | Automatically update prefixes when importing commands |
| **Namespace** | Configure the namespace for command outputs |
| **Update Namespace on Import** | Auto‑update namespace on import |
| **Remove Command Slash** | Toggle whether to include the leading `/` in output |
| **Load Item User Interface** | Choose how items are displayed in the UI |
| **Warn on Close/Reload** | Enable/disable close/reload confirmation dialogs |
| **Website Theme** | Select from multiple visual themes |
| **Item/Block List Language** | Choose display language for item/block names |
| **Item/Block List Sort** | Customize sorting order of lists |

*Source: MCStacker settings panel*

---

## 💻 Usage Examples

### Example 1: Summon a Custom Zombie

1. Select **`/summon`** from the command types
2. Choose **Zombie** as the entity
3. Set custom name: `"Boss Zombie"`
4. Add armor: diamond helmet, chestplate, leggings, boots
5. Set health: `100` (50 hearts)
6. Copy the generated command:
   ```mcfunction
   /summon minecraft:zombie ~ ~ ~ {CustomName:'{"text":"Boss Zombie"}',Health:100f,ArmorItems:[{id:"minecraft:diamond_boots",Count:1},{id:"minecraft:diamond_leggings",Count:1},{id:"minecraft:diamond_chestplate",Count:1},{id:"minecraft:diamond_helmet",Count:1}]}
   ```

### Example 2: Create an Enchanted Weapon

1. Select **`/give`**
2. Choose **Netherite Sword**
3. Add enchantments: Sharpness V, Fire Aspect II, Unbreaking III
4. Set custom name: `"Blade of the Inferno"`
5. Add lore: `"Forged in the depths of the Nether"`
6. Copy the generated command:
   ```mcfunction
   /give @p minecraft:netherite_sword{display:{Name:'{"text":"Blade of the Inferno"}',Lore:['{"text":"Forged in the depths of the Nether"}']},Enchantments:[{id:"minecraft:sharpness",lvl:5},{id:"minecraft:fire_aspect",lvl:2},{id:"minecraft:unbreaking",lvl:3}]}
   ```

### Example 3: Set a Custom Block

1. Select **`/setblock`**
2. Choose **Chest** as the block
3. Add custom loot table or items inside
4. Set block state properties (facing, type, etc.)
5. Copy the generated command

*For more examples and advanced usage, explore the [MCStacker Discord community](https://discord.gg/WCb6GNf)*

---

## 🧪 Running Tests

MCStacker is a web‑based tool, not a software library, so traditional test suites do not apply. However, you can validate your generated commands by:

1. **Testing in Minecraft** – Paste the command into a command block or chat to verify it works as expected
2. **Using the Import/Output Diff Checker** (Deluxe Edition) – Compare imported commands against expected outputs to catch errors
3. **Cross‑referencing with Minecraft version notes** – MCStacker keeps detailed change logs for each version update

If you encounter issues, visit the **[Help page](https://mcstacker.net/help.php)** or reach out to the community on Discord.

---

## 📝 Contributing

MCStacker is a closed‑source project developed and maintained by **Matt / PyroStunts**. While the source code is not publicly available, there are several ways you can contribute:

### Support the Project
- **Become a Patreon supporter** – [patreon.com/mcstacker](https://www.patreon.com/mcstacker)
- **Make a one‑time donation** – [ko-fi.com/mcstacker](https://ko-fi.com/mcstacker)
- **Purchase the Deluxe Edition** – [Ko‑fi shop](https://ko-fi.com/s/27510c833f)

### Provide Feedback
- **Report bugs & request features** – Email [bimbimma@gmail.com](mailto:bimbimma@gmail.com)
- **Join the Discord community** – [discord.gg/WCb6GNf](https://discord.gg/WCb6GNf)
- **Share your command creations** – Use the "Saved Commands" feature on the website

---

## 📄 License

MCStacker is a proprietary project. The online version is **free to use** for all players, while the Offline and Deluxe editions require a Patreon subscription or one‑time purchase, respectively.

- **Online Edition** – Free for personal and commercial use (with advertising)
- **Offline Edition** – Available to Patreon supporters ($1+/month)
- **Deluxe Edition** – One‑time purchase ($10+), includes lifetime updates and exclusive features

All rights reserved. MCStacker is not affiliated with Mojang Studios or Microsoft.

---

## 🔗 Links

| Resource | Link |
|----------|------|
| **Website** | [mcstacker.net](https://mcstacker.net/) |
| **Patreon** | [patreon.com/mcstacker](https://www.patreon.com/mcstacker) |
| **Ko‑fi** | [ko-fi.com/mcstacker](https://ko-fi.com/mcstacker) |
| **Deluxe Edition** | [Ko‑fi shop](https://ko-fi.com/s/27510c833f) |
| **Discord** | [discord.gg/WCb6GNf](https://discord.gg/WCb6GNf) |
| **Email** | [bimbimma@gmail.com](mailto:bimbimma@gmail.com) |

---

*MCStacker – Making Minecraft commands accessible since 2014.* 
