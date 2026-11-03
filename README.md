# Vocab Drill · 背单词

A tiny, offline-first vocabulary trainer for **SAT / GRE** — spaced repetition, four quiz modes, no accounts, no tracking, no backend.

[![Live demo](https://img.shields.io/badge/live-demo-5eead4?style=flat-square)](https://yli629.github.io/vocab/)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![PWA](https://img.shields.io/badge/PWA-installable-5eead4?style=flat-square)](manifest.webmanifest)

![screenshot](docs/screenshot.png)

## Features

- **Spaced repetition** — each word is scheduled at 1 / 2 / 4 / 7 / 12 / 20 days; wrong answers come back the same session.
- **Four quiz modes** — `EN→ZH`, `ZH→EN`, `Spell` (type the word), `Swipe` (right = know, left = don't).
- **Decks** — SAT (433), SAT 910 (554 unique), GRE (452), plus **your own custom deck** pasted in settings.
- **Wrong-word drill** — one tap filters to the words you've missed; a word graduates after reaching level 3.
- **Confusable hints** — after answering, pairs like *venal / venial* or *complaisant / complacent* are shown side by side.
- **Pace prediction** — estimates how many days the remaining deck will take at your recent speed.
- **Offline / installable** — service worker + web manifest; add to home screen and use it on the subway.
- **Bilingual UI** — 中文 / English.
- **Private by default** — progress lives in `localStorage`; export/import as JSON to move devices.

## Quick start

### Use it as-is

Open **https://yli629.github.io/vocab/** on your phone, then *Share → Add to Home Screen*.

### Deploy your own copy

1. Click **Use this template** (or fork this repo).
2. In your repo: **Settings → Pages → Deploy from a branch → `main` / `/ (root)`**.
3. Open `https://<your-user>.github.io/<repo>/` — done. No build step, no dependencies.

### Run locally

```bash
git clone https://github.com/Yli629/vocab.git
cd vocab
python3 -m http.server 8000
# open http://localhost:8000
```

> `?fresh=1` on the URL opens the start screen with an empty progress store — handy for screenshots.

## Custom deck

Settings → **Custom deck**, one word per line:

```
ephemeral, 短暂的
ubiquitous | adj. | 无处不在的
```

Then tap **Save and switch to my deck**. It is stored locally and can be exported with the rest of your progress.

## Data format

Everything is one JSON object in `localStorage` under `vocab_srs_v4`:

```json
{
  "settings": { "newPerDay": 40, "deck": "all", "mode": "en2zh", "examDate": "2026-12-03", "lang": "zh" },
  "words": { "abate": { "lv": 2, "due": "2026-11-08", "seen": 3, "lapses": 1 } },
  "history": { "2026-11-02": { "new": 40, "seen": 62 } },
  "custom": [{ "w": "ephemeral", "p": "", "z": "短暂的" }]
}
```

## Tech

Vanilla HTML/CSS/JS, no build, no dependencies, no analytics. ~1,500 lines total. Word lists live in `words.js`; lookalike pairs are precomputed into `confusions.js`.

## 中文说明

- **间隔重复**：答对后 1/2/4/7/12/20 天再出现；答错当场重排。
- **四种模式**：英→中、中→英、拼写、快刷（左右滑）。
- **自定义词库**：设置里粘贴，按「word, 意思」或「word | 词性 | 意思」每行一条。
- **进度**：存在手机本地，可导出 JSON 换设备。
- **离线可用**：添加到主屏幕后断网也能背。

## License

MIT — see [LICENSE](LICENSE). Word lists are included for study purposes; check them against your own sources before relying on them.
