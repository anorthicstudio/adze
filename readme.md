# Adze IDE

> The IDE for the world that never owned a PC.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Platform](https://img.shields.io/badge/Platform-Android-3ddc84.svg)]()
[![Status](https://img.shields.io/badge/Status-In%20Development-orange.svg)]()
[![Built by](https://img.shields.io/badge/Built%20by-Anorthic%20Studio-cb272c.svg)](https://anorthicstudio.com)

---

## The Problem

Billions of people in Bangladesh, Nigeria, Pakistan, Indonesia, and across the developing world watch others build careers through code — and feel locked out. Not for lack of talent. For lack of a machine.

A laptop costs $500–$1,000. Out of reach.

An Android phone? Almost universal. A tablet? Under $130.

These devices run reels. They could run careers.

Every mobile code editor today is either abandoned, crippled, or a developer's emergency backup for when they lose their real computer. Nobody has built a true IDE — full LSP, debugger, Git UI, AI panel, extensions — for the person whose only computer fits in their pocket.

**Adze is that IDE.**

Bing and Yahoo existed. Google won because it was genuinely better. Adze isn't another mobile text editor with a terminal bolted on. It is VS Code — rebuilt from the ground up for Android.

---

## What Makes Adze Different

Every other Android editor stops at syntax highlighting and a terminal. Adze closes every gap:

| Capability | Other Android editors | Adze |
|---|---|---|
| Editor engine | Ace / basic WebView | Monaco (VS Code's exact engine) |
| IntelliSense / LSP | ❌ | ✅ Full LSP via language servers |
| Debugger | ❌ | ✅ DAP-based (breakpoints, watch, call stack) |
| Git UI | Push/pull only | ✅ Stage hunks, diff view, merge conflicts, blame |
| Extensions | 30–250 plugins | ✅ Open marketplace (thousands) |
| AI panel | CLI only | ✅ IDE-native panel — inline diffs, file context |
| Problems panel | ❌ | ✅ Cross-file errors, clickable navigation |
| Multi-root workspace | ❌ | ✅ |
| Tasks / build system | ❌ | ✅ tasks.json support |
| Peek definition | ❌ | ✅ Inline peek without leaving file |
| Local history | ❌ | ✅ File timeline |
| Dedicated keyboard | ❌ | ✅ Adze Keys companion IME |

---

## Architecture

Adze is built on proven, production-grade components — not reinvented wheels.

| Layer | Technology | Reason |
|---|---|---|
| App shell | Kotlin + Jetpack Compose | Native Android performance, adaptive layout, direct pty/JNI access |
| Editor engine | Monaco Editor (WebView) | VS Code's exact engine — IntelliSense, minimap, multi-cursor, virtual rendering |
| Terminal emulator | Termux terminal-emulator (extracted) | Battle-tested VT100/xterm, GPL-3.0 compatible, ARM64 + ARMv7 |
| Linux environment | PRoot + Alpine Linux | Full package manager, no root required, runs Node.js / Python / Git / Claude Code |
| LSP | Language servers in Alpine (tsserver, pyright, clangd) | Zero IDE RAM overhead — LSP runs as Alpine process, bridges to Monaco via WebSocket |
| Debugger | DAP servers in Alpine | Debug Adapter Protocol — same standard VS Code uses |
| Git | JGit + custom visual UI | Pure Java, full Git operations, visual diff/merge panel |
| AI agents (CLI) | Claude Code + Gemini CLI via Alpine | Full agentic coding in real terminal |
| AI panel (IDE-native) | Anthropic API + Gemini API | File-context aware chat, inline diffs, no terminal required |
| Extensions | Custom plugin system + open marketplace | Community-extensible from day one |
| Keyboard | Adze Keys (custom Kotlin IME) | Dedicated coding keyboard — symbol row always visible |

### Why Native Android, Not Flutter

Flutter adds an abstraction layer between the app and the Android OS. For a code editor this costs nothing. For a terminal emulator with pty via JNI, real-time WebView bridging, and background language server processes, that cost is unacceptable. Adze needs direct access. Termux proved native Kotlin is the right foundation.

### Why Monaco, Not CodeMirror

Adze's mission is VS Code on Android — not "a decent mobile editor." Monaco is VS Code's exact engine. It handles 100,000+ line files via viewport-aware tokenization. It is heavier (5–10MB) but cached after first load. The UX parity is worth it.

### Why PRoot + Alpine, Not Custom pty

PRoot runs a full Linux environment without root. Alpine Linux's `apk` package manager installs Node.js, Python, Git, Claude Code, Gemini CLI, and any language server in seconds. This gives Adze a full developer environment on any Android device — not a toy shell.

---

## Features

### Editor (Monaco)
- Syntax highlighting for 100+ languages
- Full IntelliSense — autocomplete, parameter hints, import suggestions
- Go to definition, find references, rename symbol
- Hover documentation
- Multi-cursor editing
- Code folding, breadcrumbs, minimap
- Bracket pair colorization
- Peek definition / peek references inline
- Local file history / timeline

### Terminal
- Real pty — not a fake terminal, not cloud-dependent
- Full VT100/xterm compatibility, 24-bit color, Unicode
- Multiple terminal sessions (tabs)
- Alpine Linux environment — full `apk` package manager
- Run Node.js, Python, Go, Rust, Git, and more on-device

### Language Intelligence (LSP)
- TypeScript / JavaScript — `typescript-language-server`
- Python — `pyright`
- C / C++ — `clangd`
- Rust — `rust-analyzer`
- Go — `gopls`
- Any LSP-compatible language server installable via Alpine

### Debugger (DAP)
- Breakpoints, conditional breakpoints
- Watch variables, call stack, step through
- JavaScript / Node.js — `js-debug`
- Python — `debugpy`
- Extensible to any DAP-compatible debugger

### Git (Visual UI)
- Stage / unstage individual hunks
- Inline diff view
- Merge conflict resolution UI
- Blame annotations
- Branch management
- Commit history, file timeline
- Push / pull / fetch

### AI
- **Claude Code** — full agentic coding via Alpine terminal (plan, execute, verify)
- **Gemini CLI** — Google's AI agent via Alpine terminal
- **Adze AI Panel** — IDE-native chat with file context, inline diffs, code actions (Anthropic API + Gemini API)

### Adaptive Layout
- **Phone** — single pane, bottom terminal drawer, touch-optimized tap targets
- **Tablet** — full VS Code layout: icon strip + sidebar + editor + secondary panel + terminal split
- Same app. Same codebase. Responsive.

### Extensions
- Plugin API from day one
- Open community marketplace
- Installable from within the IDE

### Adze Keys *(companion keyboard app)*
- Dedicated Android IME for coding
- Always-visible row: `{ } [ ] ( ) < > / \ ; : " '`
- Number row, arrow keys, Tab, Esc, Ctrl combos
- Swipe-up on keys for alternate characters
- Themes sync with Adze IDE

---

## Who This Is For

- A student in Dhaka with a ৳15,000 tablet and no laptop
- A freelancer in Lagos who can afford Android but not macOS
- A developer in Karachi who is ready to ship but has no PC
- Anyone building a career in software from a device that fits in their pocket

The barrier to becoming a developer should be skill — not hardware.

---

## Roadmap

**Phase 1 — Foundation**
- [ ] Project architecture and repository structure
- [ ] Jetpack Compose shell (adaptive layout — phone + tablet)
- [ ] Monaco Editor in Android WebView with touch optimization
- [ ] File system layer (Android scoped storage + SAF)

**Phase 2 — Terminal and Linux**
- [ ] Terminal emulator (Termux terminal-emulator, extracted)
- [ ] PRoot + Alpine Linux environment bootstrap
- [ ] Multi-session terminal tabs

**Phase 3 — IDE Intelligence**
- [ ] JGit integration + visual Git UI (diff, stage, merge)
- [ ] LSP bridge (Monaco ↔ Alpine language servers via WebSocket)
- [ ] DAP debugger (Monaco ↔ Alpine debug servers)
- [ ] Problems panel, outline view, peek definition

**Phase 4 — AI**
- [ ] Claude Code + Gemini CLI (terminal, via Alpine)
- [ ] Adze AI Panel (Anthropic API + Gemini API, IDE-native)

**Phase 5 — Ecosystem**
- [ ] Plugin / extensions system + marketplace
- [ ] Tasks / build system (tasks.json)
- [ ] Multi-root workspace
- [ ] Local file history / timeline

**Phase 6 — Keyboard**
- [ ] Adze Keys — custom Android IME companion app

**Phase 7 — Polish and Launch**
- [ ] Performance optimization (low-end device testing, 2GB RAM target)
- [ ] Onboarding flow for first-time developers
- [ ] Alpha release (Google Play + F-Droid + direct APK)

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE) for details.

Open source. Always. Because the people this is built for deserve to own their tools.

---

## Contributing

Adze is in early development. Contributions, ideas, and feedback are welcome.

If you come from a country where a phone is your only computer — this is your project too.

---

*Built by [Anorthic Studio](https://github.com/anorthicstudio)*
