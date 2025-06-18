# 🧩 Custom VS Code Build with Wingman AI - README

This repository provides a portable and reproducible way to build Visual Studio Code with the **Wingman AI** extension embedded as a **core feature** (non-removable).

---

## 📦 Project Structure

```
/vscode                         # Fork of Microsoft VS Code
└── /extensions
        └── /wingman-ai        # Wingman AI source embedded here
```

---

## ✅ Tech-stack version used

* Node.js (matching `.nvmrc`, e.g. `v22.15.1`)
* Python 3.13
* C/C++ Build Tools (Windows: install via VS Build Tools or `choco install`)
* WSL2 (preferred for setup) Ubuntu

---

## 🔧 Build Instructions

### 1. Clone and Setup

```bash
git clone https://github.com/Arinjain111/fenrir-sec.git
cd vscode
npm i
npm run compile
npm run watch
```

### 2. Embeded Wingman AI Extension

Clone Wingman AI into the builtin extensions folder:

```bash
cd extensions/wingman-ai
git remote set-url origin https://github.com/RussellCanfield/wingman-ai.git
git submodule update --remote --init --recursive
```

### 4. Build Executable (Windows Example)

```bash
npm run gulp vscode-win32-x64
```

### 5. Run Dev Build

for windows build
```bash
./scripts/code.bat
```

for WSL2 build
```bash
./scripts/code.sh --no-sandbox
```

---

## 🔄 Upgrade Guide (VS Code / Wingman AI)

### A. Upgrade VS Code Base

```bash
git remote add upstream https://github.com/microsoft/vscode.git
git fetch upstream

# Rebase or merge latest
git checkout main
git rebase upstream/main   # or git merge upstream/main
```

Resolve conflicts especially in:

* `product.json`
* `gulpfile` or bootstrap files

### B. Upgrade Wingman AI Extension

If manually cloned:

```bash
cd extensions/builtin/wingman-ai
git pull origin main
```

If using submodule:

```bash
git submodule update --remote extensions/builtin/wingman-ai
```

### C. Re-Apply Custom Changes

* `gulpfile`: Ensure Wingman is bundled

---

## 🧪 Troubleshooting

### Hygiene Failures

```bash
yarn hygiene
```

Fix missing headers, lint errors, and license notices.

### Node-gyp or Wine Errors

* Ensure `windows-build-tools` installed for Windows
* On Linux, avoid using `wine` unless cross-compiling

### Swap and Heap memory issues

refer to this article
```bash
https://learn.microsoft.com/en-us/answers/questions/1296124/how-to-increase-memory-and-cpu-limits-for-wsl2-win
```

Add to `/etc/fstab`:

```
/swapfile none swap sw 0 0
```

---

## 🚀 Notes

* Extensions won't show in `dev` builds by default; use `--enable-proposed-api` to test
* Marketplace is disabled by default in portable `.exe` builds
* Customizations should be reapplied each time you rebase

---


## 📌 Final Output

* Windows: `/VSCode-win32-x64/Code.exe`
* Portable: No online dependencies, Wingman AI built-in

---

## 🧭 License

MIT for modifications. Respect the licenses of Microsoft VS Code and Wingman AI.
