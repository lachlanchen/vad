[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Javascript 的語音活動偵測

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 只需幾行程式碼，就能在包含使用者語音的音訊片段上執行回呼。

本套件旨在提供一個可於瀏覽器執行、精準且易用的語音活動偵測器（VAD）。透過此套件，你可以向使用者請求麥克風權限、開始錄音、將含有語音的音訊片段送到伺服器處理，或在使用者說話時顯示特定動畫或指示器。請注意，我已決定[停止支援 node](#important-update-about-node-support---oct-2024-)以專注於瀏覽器使用情境。

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
- [License 📄](#license-)

## Quick Links 🔗

| Resource | Link |
| --- | --- |
| Live demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Join the community](https://discord.gg/4WPeGEaSpF) |
| Survey | [Share your use case](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Contributing guide | [Developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 瀏覽說明文件（原始碼位於 `./docs` 目錄）。
- 如果你想參與貢獻，我已開始撰寫如何開始開發這些套件的文件，請見[此處](https://docs.vad.ricky0123.com/developer-guide/hacking/)。若有任何問題，你可以在此提交 issue，或到 Discord 留言。

在底層，這些套件透過 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node) 執行 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)。非常感謝這些專案的貢獻者讓這一切成為可能。

i18n 狀態說明：`i18n/` 已存在，且包含多個已翻譯的 README 檔案。上方語言選擇器也包含計畫中或占位用的翻譯連結（`README.de.md`、`README.ru.md`），它們在此儲存庫快照中可能尚未存在。

## Overview 🧭

此儲存庫是一個 monorepo，主要發布兩個套件：

| Package | Purpose |
| --- | --- |
| `@ricky0123/vad-web` | 瀏覽器 API，包含 `MicVAD`、`AudioNodeVAD`、`NonRealTimeVAD` |
| `@ricky0123/vad-react` | `vad-web` 的 React hook 包裝器（`useMicVAD`） |

本專案以瀏覽器為優先，並包含：

- 即時麥克風分段回呼（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` 等）
- 可設定的演算法閾值與時間控制
- 支援 Legacy 與 v5 的 Silero 模型
- 本儲存庫內含 demo/test 應用與文件網站來源

## Features ✨

- 由 Silero ONNX 模型驅動、以瀏覽器為優先的 VAD 流程
- 可搭配 script tag、bundler 與 React 使用
- 提供合理預設的麥克風 stream 約束
- 可覆寫的 stream 生命週期（`getStream`、`pauseStream`、`resumeStream`）
- 透過 `NonRealTimeVAD` 對預錄音訊進行非即時語音分段
- 透過 `baseAssetPath` 與 `onnxWASMBasePath` 設定模型/資產載入
- 內建包裝器支援 legacy 與 v5 模型狀態處理
- 含 script tag、webpack bundler、React bundler 與 Next.js 的範例

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

更詳細的路徑：

- `packages/web/src/real-time-vad.ts`：即時麥克風/audio-node VAD 協調邏輯
- `packages/web/src/non-real-time-vad.ts`：預錄音訊的非同步分段
- `packages/web/src/frame-processor.ts`：閾值判斷與語音片段邊界邏輯
- `packages/react/src/index.ts`：`useMicVAD` React hook 生命週期與狀態包裝

## Compatibility Matrix 🧩

| Component | Environment |
| --- | --- |
| `@ricky0123/vad-web` | 支援 WebAudio + `MediaDevices.getUserMedia` 的現代瀏覽器 |
| `@ricky0123/vad-react` | React 應用（`react` / `react-dom` >= 16.8.0） |
| Docs toolchain | Python 3.10 + Poetry（依 CI workflow） |
| CI Node runtime | Node 18（依儲存庫 workflows） |

假設說明：範例與文件與此儲存庫快照中的目前套件版本一致（`@ricky0123/vad-web@0.0.27`、`@ricky0123/vad-react@0.0.33`）。

## Prerequisites ✅

- 瀏覽器使用：支援 `MediaDevices.getUserMedia` 的現代瀏覽器
- 本機開發：Node.js + npm workspaces
- 文件開發：Python + Poetry（用於 MkDocs 建置）

依據 CI 設定建議的本機基準版本：

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

安裝 monorepo 相依套件（貢獻者）：

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

若要在瀏覽器中透過 script tag 使用 VAD，請加入以下 script tags：

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

各 API 常見選項包含：

- `positiveSpeechThreshold`（即時 API 預設約為 `0.3`）
- `negativeSpeechThreshold`（即時 API 預設約為 `0.25`）
- `redemptionMs`（即時 API 預設約為 `1400`）
- `preSpeechPadMs`（即時 API 預設約為 `800`）
- `minSpeechMs`（即時 API 預設約為 `400`）

即時 API（`MicVAD`、`useMicVAD`）另外支援：

- `getStream`、`pauseStream`、`resumeStream`
- `onFrameProcessed`、`onSpeechStart`、`onSpeechRealStart`、`onSpeechEnd`、`onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` 或 `"v5"`）
- `baseAssetPath` 與 `onnxWASMBasePath`
- `workletOptions`

完整 API 表格請見文件：[API reference](https://docs.vad.ricky0123.com/user-guide/api/) 與 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### Configuration recipe: self-hosting model and runtime assets

不使用 CDN 預設值時，請確認你的應用有提供：

- `silero_vad_legacy.onnx` 與/或 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 執行階段檔案（`.wasm`；以及較新執行階段建置所需的 `.mjs`）

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

儲存庫範例：

- `examples/script-tags`：基本 script-tag 設定
- `examples/bundler`：webpack + `@ricky0123/vad-web`
- `examples/react-bundler`：webpack + `@ricky0123/vad-react`
- `examples/nextjs`：Next.js 整合範例

`examples/bundler` 的示例指令：

```bash
npm run build && npm run start
```

關於如何在瀏覽器打包語音活動偵測器，或在 node 與 React 專案中使用的文件，請見 [vad.ricky0123.com](https://www.vad.ricky0123.com)。

## Development Notes 🛠️

根工作區腳本：

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

用途說明：

- `npm run build`：建置所有 workspaces
- `npm run test`：執行 workspace 測試
- `npm run test:coverage`：`packages/web` 的 coverage
- `npm run typecheck`：檢查 packages、test-site 與 tests 的 TypeScript
- `npm run format-check`：檢查 `packages`、`examples`、`test-site` 下 TS/TSX 的格式
- `npm run dev`：監看 package 與 test-site 原始碼、重新建置並提供 `test-site/dist`

文件建置（MkDocs + Poetry）：

```bash
poetry install
poetry run mkdocs serve
```

補充說明：

- `./test-site/build.sh` 會將必要的 VAD/ONNX Runtime 資產複製到 `test-site/dist` 與 `test-site/dist/subpath`
- `./scripts/dev.sh` 使用 `nodemon` + `live-server`，在 `8080` 埠進行本機重建與服務循環
- `./check_vad_up_to_date.sh` 為歷史腳本，且引用 `silero_vad.onnx`（而本儲存庫提供的是 `silero_vad_legacy.onnx` 與 `silero_vad_v5.onnx`）

## CI & Quality Gates 🧱

位於 `.github/workflows/` 的 GitHub workflows 包含：

- Test（`test.yml`）
- Typecheck（`typecheck.yml`）
- Formatting（`format-check.yml`）
- Docs build/deploy（`docs.yml`）
- Publish flow（`publish.yml`）

這些 workflows 是預期執行環境/工具版本與發佈檢查的實用事實依據。

## Troubleshooting 🩺

| Symptom | Check / Fix |
| --- | --- |
| Mic permission denied | 確認瀏覽器已為你的來源授予麥克風權限。 |
| Assets fail to load (`.onnx`, `.wasm`, `.mjs`, worklet) | 正確設定 `baseAssetPath` / `onnxWASMBasePath`，並確認檔案確實有被提供。 |
| Newer `onnxruntime-web` runtime issues | 除了 `.wasm` 之外，也需提供 `.mjs` 檔案。 |
| Local dev over insecure origin | 瀏覽器麥克風 API 通常要求安全內容（`https` 或 `localhost`）。 |
| Build-time bundler issues | 使用[browser docs](https://docs.vad.ricky0123.com/user-guide/browser/)中的打包指引。 |
| Next.js integration issues | 依照 [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) 的設定模式，並確認靜態資產託管路徑。 |

## Sponsorship ❤️

請以財務方式支持本專案，尤其是當你的商業產品依賴此套件時。[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Important update about node support - Oct 2024 📢

我將逐步停止支援 `ricky0123/vad-node`，也就是用於伺服器端 node 環境的語音活動偵測套件。從現在開始，我不打算再發佈 node 套件更新。做出這個決定有以下原因：

- 我最初的使用情境是客戶端語音活動偵測。後來因應他人請求加入了 node 支援，想盡量幫忙。然而我能投入此專案的時間有限，停用 `ricky0123/vad-node` 可讓我把更多時間放在 `ricky0123/vad-web`。
- 相較之下，開發者要自行打造伺服器端語音活動偵測方案，通常比學會 onnxruntime-web、audio worklets 等技術並做出客戶端方案更容易。因此我認為 `ricky0123/vad-web` 對社群能提供更高價值。
- 由於執行與使用語音活動偵測模型所需的環境差異，瀏覽器與 node 套件之間共享程式碼相當尷尬。
- 根據[問卷](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)，多數使用者都在使用 `ricky0123/vad-web`（可能也包含 `ricky0123/vad-react`）。

## Roadmap 🛣️

目前方向（依儲存庫現況與上方維護者說明）：

- 持續聚焦於瀏覽器優先 API（`@ricky0123/vad-web`、`@ricky0123/vad-react`）
- 維護並改進 bundler 與 framework 的文件/範例
- 改善貢獻者/開發者文件與 test-site 工作流程
- 在 `i18n/` 下新增並維護多語 README

## Contributing 🤝

- 閱讀開發指南：[docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 在此儲存庫提出 issue 或 PR：[github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 快速掌握專案脈絡可參考 [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## License 📄

- 專案授權：ISC（見 [LICENSE](LICENSE)）
