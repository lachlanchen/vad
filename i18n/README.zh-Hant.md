[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript 語音活動偵測

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 只要幾行程式碼，就能對含有人聲的音訊片段執行回呼。

本套件目標是提供可在瀏覽器中執行、精準且友善好用的語音活動偵測（VAD）工具。使用此套件後，你可以請求使用者授予麥克風權限、開始錄音、把含語音的音訊片段傳送到你的伺服器處理，或在使用者正在說話時顯示動畫與指示器。請注意，我已決定[停止支援 node](#important-update-about-node-support---oct-2024-)以便將重心放在瀏覽器使用情境上。

| 快速總覽 | 詳細 |
| --- | --- |
| 核心套件 | `@ricky0123/vad-web`、`@ricky0123/vad-react` |
| 主要執行環境 | 瀏覽器（`WebAudio` + `getUserMedia`） |
| 文件 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 線上示範 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

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
- [❤️ Support](#-support)
- [Important update about node support - Oct 2024 📢](#important-update-about-node-support---oct-2024-)
- [Roadmap 🛣️](#roadmap-)
- [Contributing 🤝](#contributing-)
- [References 📚](#references-)
- [License 📄](#license-)

## Quick Links 🔗

| Resource | Link |
| --- | --- |
| 線上示範 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 文件 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [加入社群](https://discord.gg/4WPeGEaSpF) |
| 問卷 | [分享你的使用情境](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 貢獻指南 | [開發者入門指南](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 文件原始檔位於 `./docs`。
- 貢獻者導向可由這裡開始：[developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/)。問題可透過 issue 或 Discord 提出。

底層而言，本套件透過 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web)（並有早期 Node 支援的歷史參考 ONNX Runtime Node.js）執行 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)。感謝這些專案讓這一切能成為可能。

關於 i18n 狀態說明：`i18n/` 包含本頁頂部語言選項對應的 README 翻譯檔案。

## Overview 🧭

這個 repo 是 monorepo，主要有兩個已發佈套件：

| 套件 | 用途 |
| --- | --- |
| `@ricky0123/vad-web` | 瀏覽器 API，包含 `MicVAD`、`AudioNodeVAD` 與 `NonRealTimeVAD` |
| `@ricky0123/vad-react` | `vad-web` 的 React hook 包裝器（`useMicVAD`） |

專案以瀏覽器優先設計，包含：

- 即時麥克風分段回呼（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` 等）
- 可調整的演算法閾值與時間控制
- 支援 legacy 與 v5 的 Silero 模型
- repo 內含 demo/test app 與文件網站的原始碼

## Features ✨

- 由 Silero ONNX 模型驅動、以瀏覽器為先的 VAD 流程
- 支援 script tag、bundler 與 React
- 合理預設的麥克風 stream constraints
- 可覆寫的串流生命週期（`getStream`、`pauseStream`、`resumeStream`）
- 使用 `NonRealTimeVAD` 對預錄音訊進行非即時語音分段
- 可透過 `baseAssetPath` 與 `onnxWASMBasePath` 設定模型/資產載入
- 透過內建包裝器同時支援 legacy 與 v5 模型狀態
- 提供 script tag、webpack-based bundlers、React bundlers、Next.js 的實作範例

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

- `packages/web/src/real-time-vad.ts`：即時麥克風與 audio-node VAD 的協調邏輯
- `packages/web/src/non-real-time-vad.ts`：預錄音訊的非同步分段
- `packages/web/src/frame-processor.ts`：閾值判斷與語音片段邊界邏輯
- `packages/react/src/index.ts`：`useMicVAD` React hook 的生命週期與狀態包裝

## Compatibility Matrix 🧩

| Component | Environment |
| --- | --- |
| `@ricky0123/vad-web` | 支援 WebAudio + `MediaDevices.getUserMedia` 的現代瀏覽器 |
| `@ricky0123/vad-react` | React 應用（`react` / `react-dom` >= 16.8.0） |
| Docs toolchain | Python 3.10 + Poetry（依 CI workflow） |
| CI Node runtime | Node 18（依 repository workflows） |

Repository snapshot 套件版本（`packages/*/package.json`）：

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerequisites ✅

- 瀏覽器使用：現代瀏覽器且支援 `MediaDevices.getUserMedia`
- 本機開發：Node.js + npm workspaces
- 文件開發：Python + Poetry（用於 MkDocs 建置）

依 CI 設定建議的本機基線版本：

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

安裝 monorepo 相依套件（給貢獻者）：

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

要在瀏覽器中透過 script tag 使用 VAD，請加入以下標籤：

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

各 API 的常見選項包含：

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

完整 API 表可參考文件： [API 參考](https://docs.vad.ricky0123.com/user-guide/api/) 與 [演算法說明](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### Configuration recipe: self-hosting model and runtime assets

未使用 CDN 預設值時，請確認你的應用有提供：

- `silero_vad_legacy.onnx` 與/或 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` runtime 檔案（`.wasm`；新式 runtime 建置可用 `.mjs`）

接著設定：

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

本 repo 的範例：

- `examples/script-tags`：基本 script-tag 設定
- `examples/bundler`：webpack + `@ricky0123/vad-web`
- `examples/react-bundler`：webpack + `@ricky0123/vad-react`
- `examples/nextjs`：Next.js 整合範例

`examples/bundler` 的指令範例：

```bash
npm run build && npm run start
```

關於在瀏覽器打包語音活動偵測器，或在 node 或 React 專案使用，請參見 [vad.ricky0123.com](https://www.vad.ricky0123.com)。

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

對應用途如下：

- `npm run build`：建置所有 workspace
- `npm run test`：執行 workspace 測試
- `npm run test:coverage`：針對 `packages/web` 的 coverage
- `npm run typecheck`：檢查 `packages`、`test-site` 與 `tests` 的 TypeScript
- `npm run format-check`：檢查 `packages`、`examples`、`test-site` 下 TS/TSX 格式
- `npm run dev`：即時監看 package 與 test-site 原始檔、重建並提供 `test-site/dist`

文件建置（MkDocs + Poetry）：

```bash
poetry install
poetry run mkdocs serve
```

補充說明：

- `./test-site/build.sh` 會將必要的 VAD/ONNX Runtime 資產複製到 `test-site/dist` 與 `test-site/dist/subpath`
- `./scripts/dev.sh` 使用 `nodemon` + `live-server`，在本機的 `8080` 進行重建與即時伺服
- `./check_vad_up_to_date.sh` 是歷史腳本，仍參考 `silero_vad.onnx`（而本 repo 提供 `silero_vad_legacy.onnx` 與 `silero_vad_v5.onnx`）

## CI & Quality Gates 🧱

`.github/workflows/` 下的 GitHub workflows 包含：

- 測試（`test.yml`）
- Typecheck（`typecheck.yml`）
- 格式檢查（`format-check.yml`）
- 文件建置與部署（`docs.yml`）
- 發佈流程（`publish.yml`）

這些 workflow 是實務上可信賴的版本與工具版本、發佈檢核來源。

## Troubleshooting 🩺

| 症狀 | 檢查 / 修正 |
| --- | --- |
| 麥克風權限被拒 | 請確認該網域已取得麥克風權限 |
| 資產無法載入（`.onnx`、`.wasm`、`.mjs`、worklet） | 正確設定 `baseAssetPath` / `onnxWASMBasePath`，並確認檔案確實被提供 |
| `onnxruntime-web` 新版 runtime 問題 | 除了 `.wasm` 外，亦需提供 `.mjs` |
| 本機開發在不安全來源 | 瀏覽器麥克風 API 通常要求安全來源（`https` 或 `localhost`） |
| 打包時期問題 | 請參考 [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/) 中的打包建議 |
| Next.js 整合問題 | 依照 [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) 的設定模式並確認靜態資源託管路徑 |

## Sponsorship ❤️

若你的商業產品依賴本套件，請以經濟方式支持本專案。[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Important update about node support - Oct 2024 📢

我將逐步停止支援 `ricky0123/vad-node`（伺服器端 Node 環境的語音活動偵測套件）。自此以後，我不打算再發布 node 套件更新。做出這個決定的原因如下：

- 這個專案的原始目標是用於用戶端語音活動偵測。我是因為有人需求才加入 node 支援，並希望幫助更多人。不過我可用於維護此專案的時間有限，停止 `ricky0123/vad-node` 可讓我更專注在 `ricky0123/vad-web` 上。
- 對每位開發者來說，要自行打造伺服器端語音活動偵測解法，比學會如何使用 onnxruntime-web、audio worklets 等技術並做出用戶端解法，要容易得多。因此我認為 `ricky0123/vad-web` 對社群有更高價值。
- 由於執行與使用語音活動偵測模型的環境差異，瀏覽器套件與 node 套件之間共享程式碼相當不順。
- 根據[問卷結果](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)，大多數使用者都在使用 `ricky0123/vad-web`（可能也有搭配 `ricky0123/vad-react`）。

## Roadmap 🛣️

目前方向（依 repo 現況與維護者上述備註）：

- 持續聚焦於瀏覽器優先 API（`@ricky0123/vad-web`、`@ricky0123/vad-react`）
- 維護並改善 bundlers 與 frameworks 的文件與範例
- 改善貢獻者/開發者文件與 test-site 流程
- 在 `i18n/` 下新增並維護更多語系 README

## Contributing 🤝

- 閱讀 hacking guide：[docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 在此庫提出 issue 或 PR：[github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 想快速掌握專案脈絡，請參考 [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD 專案：[github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## License 📄

- 專案授權：ISC（參見 [LICENSE](LICENSE)）
