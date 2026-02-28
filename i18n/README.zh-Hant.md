[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript 的語音活動偵測

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)
[![CI](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/test.yml?branch=main&style=flat-square&label=CI)](https://github.com/ricky0123/vad/actions/workflows/test.yml)
[![Typecheck](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/typecheck.yml?branch=main&style=flat-square&label=Typecheck)](https://github.com/ricky0123/vad/actions/workflows/typecheck.yml)
[![Docs](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/docs.yml?branch=main&style=flat-square&label=Docs)](https://github.com/ricky0123/vad/actions/workflows/docs.yml)
[![GitHub stars](https://img.shields.io/github/stars/ricky0123/vad?style=flat-square&logo=github)](https://github.com/ricky0123/vad)
[![Node.js 18+](https://img.shields.io/badge/Node-18%2B-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)

> 只要幾行程式碼，就能在使用者說話時的音訊片段上執行回呼。

這個套件目標是提供一個準確且使用者友善的、可在瀏覽器執行的語音活動偵測（VAD）工具。透過它，你可以請求使用者麥克風權限、開始錄音、將含有語音的音訊片段傳送到後端處理，或是在使用者正在說話時顯示動畫或指示器。請注意，我已決定[停止 node 支援](#important-update-about-node-support---oct-2024-)以便將重心放在瀏覽器使用案例上。

| 🧭 簡要總覽 | 詳情 |
| --- | --- |
| 📦 核心套件 | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 主要執行環境 | 瀏覽器（`WebAudio` + `getUserMedia`） |
| 📚 文件 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 線上示範 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Table of Contents

- [Quick Links 🔗](#quick-links-)
- [Overview 🧭](#overview-)
- [Features ✨](#features-)
- [Project Structure 🗂️](#project-structure-)
- [Compatibility Matrix 🧩](#compatibility-matrix-)
- [Prerequisites ✅](#prerequisites-)
- [Installation 📦](#installation-)
- [Usage 🚀](#usage-)
- [Configuration ⚙️](#configuration-)
- [Examples 🧪](#examples-)
- [Development Notes 🛠️](#development-notes-)
- [CI & Quality Gates 🧱](#ci--quality-gates-)
- [Troubleshooting 🩺](#troubleshooting-)
- [Sponsorship ❤️](#sponsorship-)
- [Important update about node support - Oct 2024 📢](#important-update-about-node-support---oct-2024-)
- [Roadmap 🛣️](#roadmap-)
- [Contributing 🤝](#contributing-)
- [References 📚](#references-)
- [❤️ Support](#-support)
- [License 📄](#license-)

## Quick Links 🔗

| 資源 | 連結 |
| --- | --- |
| 線上示範 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 文件 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [加入社群](https://discord.gg/4WPeGEaSpF) |
| 問卷 | [分享你的使用案例](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 貢獻指南 | [開發者指南](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 文件原始碼位於 `./docs`。
- 貢獻者可從這裡開始：[developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/)。如果有問題，歡迎透過 Issue 或 Discord 詢問。

在底層，這些套件透過 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web)（含歷史上針對 ONNX Runtime Node.js 的參考，來自先前 node 支援時代）運行 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)。感謝這些專案的貢獻者，讓這些功能變成現實。

關於 i18n：`i18n/` 包含本頁上方語言清單對應的 README 翻譯檔。

## Overview 🧭

這個專案是個 monorepo，主要發布兩個套件：

| 套件 | 用途 |
| --- | --- |
| `@ricky0123/vad-web` | 瀏覽器 API，包含 `MicVAD`、`AudioNodeVAD` 與 `NonRealTimeVAD` |
| `@ricky0123/vad-react` | `vad-web` 的 React Hook 包裝器（`useMicVAD`） |

專案採用瀏覽器優先模式，並提供：

- 即時麥克風分段回呼（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` 等）
- 可調整的演算法閾值與時間參數
- 支援 legacy 與 v5 的 Silero 模型
- 倉庫內含範例應用與文件網站原始碼

## Features ✨

- 以 Silero ONNX 模型驅動的瀏覽器優先 VAD 流程
- 支援 `<script>` 標籤、打包工具與 React
- 合理的預設麥克風串流限制
- 可覆寫串流生命週期（`getStream`、`pauseStream`、`resumeStream`）
- 透過 `NonRealTimeVAD` 支援預先錄製音訊的非即時語音分段
- 可透過 `baseAssetPath` 與 `onnxWASMBasePath` 設定模型與 runtime 資源載入
- 透過內建包裝器同時支援 legacy 與 v5 模型狀態
- 提供 script tag、Webpack 打包、React 打包器與 Next.js 的範例

## Project Structure 🗂️

```text
.
├── README.md
├── docs/                     # MkDocs source for docs.vad.ricky0123.com
├── examples/                 # script-tag, bundler, react-bundler, nextjs examples
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # dev helpers
├── test-site/                # local interactive playground
├── i18n/                     # translated README files
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

更詳細路徑：

- `packages/web/src/real-time-vad.ts`：即時麥克風 / audio-node VAD 的協調流程
- `packages/web/src/non-real-time-vad.ts`：預先錄製音訊的非同步分段
- `packages/web/src/frame-processor.ts`：閾值判定與語音片段邊界邏輯
- `packages/react/src/index.ts`：`useMicVAD` React hook 的生命週期與狀態封裝

## Compatibility Matrix 🧩

| 元件 | 支援環境 |
| --- | --- |
| `@ricky0123/vad-web` | 現代瀏覽器（支援 `WebAudio` + `MediaDevices.getUserMedia`） |
| `@ricky0123/vad-react` | React 應用（`react` / `react-dom` >= 16.8.0） |
| 文件工具鏈 | Python 3.10 + Poetry（依 CI 工作流程） |
| CI Node runtime | Node 18（依倉庫工作流程） |

倉庫快照中的套件版本（`packages/*/package.json`）：

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerequisites ✅

- 瀏覽器使用：支援 `MediaDevices.getUserMedia` 的現代瀏覽器
- 本機開發：Node.js + npm workspaces
- 文件開發：Python + Poetry（用於 MkDocs 建置）

依 CI 設定的建議本機基線：

- Node.js 18.x
- Python 3.10.x

## Installation 📦

安裝瀏覽器套件：

```bash
npm i @ricky0123/vad-web
```

安裝 React 包裝器：

```bash
npm i @ricky0123/vad-react
```

安裝 monorepo 依賴（供貢獻者使用）：

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

在瀏覽器透過 script tag 使用 VAD，請加入下列腳本：

```html
<script src="https://cdn.jsdelivr.net/npm/onnxruntime-web@1.22.0/dist/ort.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@ricky0123/vad-web@0.0.27/dist/bundle.min.js"></script>
<script>
  async function main() {
    const myvad = await vad.MicVAD.new({
      onSpeechStart: () => {
        console.log("Speech start detected")
      },
      onSpeechEnd: (audio) => {
        // do something with `audio` (Float32Array of audio samples at sample rate 16000)...
      },
      onnxWASMBasePath: "https://cdn.jsdelivr.net/npm/onnxruntime-web@1.22.0/dist/",
      baseAssetPath: "https://cdn.jsdelivr.net/npm/@ricky0123/vad-web@0.0.27/dist/",
    })
    myvad.start()
  }
  main()
</script>
```

### Browser package usage (module import)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React usage

```tsx
import { useMicVAD } from "@ricky0123/vad-react"

export function MyComponent() {
  const vad = useMicVAD({
    onSpeechEnd: (audio) => {
      console.log("User stopped talking", audio.length)
    },
  })

  return <div>{vad.userSpeaking ? "User is speaking" : "Idle"}</div>
}
```

### Non-real-time usage (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuration ⚙️

各 API 共用的常見選項包括：

- `positiveSpeechThreshold`（即時 API 預設約為 `0.3`）
- `negativeSpeechThreshold`（即時 API 預設約為 `0.25`）
- `redemptionMs`（即時 API 預設約為 `1400`）
- `preSpeechPadMs`（即時 API 預設約為 `800`）
- `minSpeechMs`（即時 API 預設約為 `400`）

即時 API（`MicVAD`、`useMicVAD`）也支援：

- `getStream`、`pauseStream`、`resumeStream`
- `onFrameProcessed`、`onSpeechStart`、`onSpeechRealStart`、`onSpeechEnd`、`onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` 或 `"v5"`）
- `baseAssetPath` 與 `onnxWASMBasePath`
- `workletOptions`

完整 API 表可參見文件：[API reference](https://docs.vad.ricky0123.com/user-guide/api/) 與 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### Configuration recipe: self-hosting model and runtime assets

若未使用 CDN 預設資源，請確認你的應用程式能提供：

- `silero_vad_legacy.onnx` 和/或 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` runtime 檔案（`.wasm`，以及新版本 runtime 的 `.mjs`）

接著這樣設定：

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Examples 🧪

倉庫示例：

- `examples/script-tags`：基礎 script-tag 範例
- `examples/bundler`：webpack + `@ricky0123/vad-web`
- `examples/react-bundler`：webpack + `@ricky0123/vad-react`
- `examples/nextjs`：Next.js 串接範例

`examples/bundler` 的範例指令：

```bash
npm run build && npm run start
```

在瀏覽器中打包語音活動偵測器，或在 node／React 專案中使用，請參閱 [vad.ricky0123.com](https://www.vad.ricky0123.com)。

## Development Notes 🛠️

根目錄 workspace 指令：

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

各指令用途：

- `npm run build`：建置所有工作區
- `npm run test`：執行 workspace 測試
- `npm run test:coverage`：`packages/web` 的覆蓋率
- `npm run typecheck`：檢查 `packages`、`test-site` 與 tests 的 TypeScript
- `npm run format-check`：檢查 `packages`、`examples`、`test-site` 下 TS/TSX 的格式
- `npm run dev`：監看 package 與 test-site 原始碼，重建並服務 `test-site/dist`

文件建置（MkDocs + Poetry）：

```bash
poetry install
poetry run mkdocs serve
```

補充：

- `./test-site/build.sh` 會將所需的 VAD/ONNX Runtime 資源複製到 `test-site/dist` 與 `test-site/dist/subpath`
- `./scripts/dev.sh` 會使用 `nodemon` + `live-server` 於本機 8080 進行重建與服務迴圈
- `./check_vad_up_to_date.sh` 是歷史遺留腳本，仍引用 `silero_vad.onnx`（本倉庫實際提供 `silero_vad_legacy.onnx` 與 `silero_vad_v5.onnx`）

## CI & Quality Gates 🧱

`.github/workflows/` 中的 GitHub 工作流程包含：

- 測試（`test.yml`）
- 型別檢查（`typecheck.yml`）
- 格式檢查（`format-check.yml`）
- 文件建置與部署（`docs.yml`）
- 發佈流程（`publish.yml`）

這些工作流程也是實際可作為執行時與工具版本、版本發布檢查依據的主要來源。

## Troubleshooting 🩺

| 症狀 | 檢查 / 修正 |
| --- | --- |
| 麥克風權限被拒 | 確認瀏覽器已允許你的網域使用麥克風 |
| 資源載入失敗（`.onnx`、`.wasm`、`.mjs`、worklet） | 正確設定 `baseAssetPath` / `onnxWASMBasePath`，並確認檔案確實被提供 |
| `onnxruntime-web` 最新 runtime 問題 | 除 `.wasm` 外，務必一併提供 `.mjs` 檔案 |
| 本機開發走不安全來源（非 HTTPS） | 瀏覽器麥克風 API 通常需要安全內容（`https` 或 `localhost`） |
| 打包建置期問題 | 依 [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/) 的打包建議處理 |
| Next.js 整合問題 | 依照 [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) 的設定模式，並確認靜態資源託管路徑 |

## Sponsorship ❤️

如果你的產品有商業用途，歡迎對專案提供經濟支持。[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Important update about node support - Oct 2024 📢

我將逐步終止 `ricky0123/vad-node` 的支援。`ricky0123/vad-node` 是用於伺服器端 node 環境的語音活動偵測套件。從現在起我不再繼續發布該 node 套件的更新。這樣做的原因如下：

- 這個專案一開始主要是用在客戶端語音活動偵測。我是因為有需求才加上 node 支援，初衷是幫助更多人；但目前可投入時間有限，停用 `ricky0123/vad-node` 能讓我把更多時間放在 `ricky0123/vad-web` 上。
- 相較於學習 `onnxruntime-web`、`audio worklet` 等技術並自行打造客戶端方案，個別開發者通常更容易自行建立伺服器端的語音活動偵測方案。因此我認為 `ricky0123/vad-web` 對社群更有價值。
- 瀏覽器與 Node 環境在執行與使用語音活動偵測模型的關鍵面向差異很大，讓這兩個套件之間共享程式碼變得不順暢。
- 根據[問卷](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)結果，大多數使用者正在使用 `ricky0123/vad-web`（通常搭配 `ricky0123/vad-react`）。

## Roadmap 🛣️

目前方向（依倉庫現況與維護者說明）：

- 持續聚焦瀏覽器優先 API（`@ricky0123/vad-web`、`@ricky0123/vad-react`）
- 維護並改善打包器與框架文件／範例
- 改善貢獻者與開發者文件，以及 `test-site` 工作流程
- 在 `i18n/` 下新增並維護更多語言版本 README

## Contributing 🤝

- 閱讀開發者指南：[docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 在本倉庫提交 Issue 或 PR：[github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 想快速掌握專案脈絡，請參閱 [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD 倉庫：[github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

- 專案授權：ISC（請參閱 [LICENSE](LICENSE)）
