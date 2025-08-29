# Termux Ollama Setup Guide

A complete step-by-step guide to install and run **Ollama (LLM runtime)** on Android using **Termux**.  
This document is structured so you can copy-paste commands in one click.

---

## 🔗 Useful Links
- **Download Termux (F-Droid):**  
  https://f-droid.org/packages/com.termux/

- **Ollama GitHub Repository:**  
  https://github.com/ollama/ollama

- **Ollama Official Website (Model Library):**  
  https://ollama.com/library

- **Ollama Android Client (Community UI):**  
  https://github.com/JHubi1/ollama-app

---

## 🛠️ Installation

### 1) Update Termux
```bash
pkg update && pkg upgrade -y
```

### 2) Install Required Dependencies
```bash
pkg install git cmake golang -y
```

### 3) Clone Ollama Repository
```bash
git clone --depth 1 https://github.com/ollama/ollama
```

### 4) Enter the Repository
```bash
ls
cd ollama
```

### 5) Generate and Build Ollama
```bash
go generate ./...
go build .
```

### 6) Start Ollama Server
```bash
./ollama serve &
```

### 7) Run a Model
```bash
./ollama run gemma3:1b
```

---

## 🔄 Restarting the Server
```bash
cd ~/ollama
./ollama serve &
./ollama run gemma3:1b
```

---

## 🤖 Running Other Models
```bash
ollama run phi3:mini
```
👉 Full list of available models: https://ollama.com/library

---

## 📱 Using a Client App (Optional)
- Install this Android client:  
  https://github.com/JHubi1/ollama-app  
- Connect it to your local Ollama server for a better UI experience.

---

## ⚡ Quick Setup (One Command)
```bash
pkg update && pkg upgrade -y && pkg install git cmake golang -y && git clone --depth 1 https://github.com/ollama/ollama && cd ollama && go generate ./... && go build . && ./ollama serve & && ./ollama run gemma3:1b
```

---

## ✅ Notes
- First time running a model downloads it from the internet.
- After download, models run offline.
- Restart the server anytime with:  
  ```bash
  ./ollama serve &
  ```
- For better UI experience, use the [Ollama App](https://github.com/JHubi1/ollama-app).

---

## 📚 References
- Ollama Docs: https://github.com/ollama/ollama  
- Termux Wiki: https://wiki.termux.com/
