[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript 语音活动检测

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

> 只需几行代码，即可在用户说话的音频片段上执行回调。

该软件包旨在提供一个准确、友好的浏览器端语音活动检测（VAD）实现。通过本软件包，你可以申请麦克风权限、开始录音、将包含语音的音频片段发送到你的服务端处理，或在用户正在说话时显示动画或指示器。注意：我已决定[停止 node 支持](#important-update-about-node-support---oct-2024-)以便把精力集中在浏览器场景。

| 🧭 快速概览 | 详情 |
| --- | --- |
| 📦 核心包 | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 主要运行环境 | 浏览器（`WebAudio` + `getUserMedia`） |
| 📚 文档 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 在线演示 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

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

| Resource | Link |
| --- | --- |
| 在线演示 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 文档 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [加入社区](https://discord.gg/4WPeGEaSpF) |
| 调研 | [分享你的使用场景](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 贡献指南 | [开发者开发指南](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 文档源码位于 `./docs`。
- 贡献者入门从这里开始：[developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/)。如有问题，可在 Issue 或 Discord 提出。

在底层，这些包通过 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web)（带有历史上对 ONNX Runtime Node.js 的引用，来自此前的 Node 支持）运行 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)。感谢这些开源项目，使这一切成为可能。

关于 i18n 的说明：`i18n/` 包含本文件顶部已列出的语言对应 README 翻译。

## Overview 🧭

该仓库是一个 monorepo，包含两个主要发布包：

| Package | 用途 |
| --- | --- |
| `@ricky0123/vad-web` | 浏览器 API，包含 `MicVAD`、`AudioNodeVAD` 和 `NonRealTimeVAD` |
| `@ricky0123/vad-react` | `vad-web` 的 React Hook 封装器（`useMicVAD`） |

项目采用浏览器优先策略，包含：

- 实时麦克风分段回调（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` 等）
- 可配置的算法阈值和时间参数
- 支持 legacy 与 v5 Silero 模型
- 仓库内提供示例应用和文档站源码

## Features ✨

- 由 Silero ONNX 模型驱动的浏览器优先 VAD 流程
- 支持脚本标签、打包器和 React
- 合理的麦克风流默认约束
- 可覆盖的流生命周期（`getStream`、`pauseStream`、`resumeStream`）
- 通过 `NonRealTimeVAD` 支持预录音频的非实时语音分段
- 可通过 `baseAssetPath` 与 `onnxWASMBasePath` 配置模型与运行时资源加载
- 通过内置包装器同时支持 legacy 与 v5 模型状态
- 提供 script tag、webpack 打包器、React 打包器与 Next.js 示例

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

更详细的路径：

- `packages/web/src/real-time-vad.ts`：实时麦克风/audio-node VAD 的编排实现
- `packages/web/src/non-real-time-vad.ts`：预录音频的异步分段
- `packages/web/src/frame-processor.ts`：阈值判断与语音片段边界逻辑
- `packages/react/src/index.ts`：`useMicVAD` React hook 生命周期与状态封装

## Compatibility Matrix 🧩

| 组件 | 支持环境 |
| --- | --- |
| `@ricky0123/vad-web` | 现代浏览器（支持 `WebAudio` + `MediaDevices.getUserMedia`） |
| `@ricky0123/vad-react` | React 应用（`react` / `react-dom` >= 16.8.0） |
| 文档工具链 | Python 3.10 + Poetry（按 CI 工作流） |
| CI Node 运行时 | Node 18（按仓库工作流） |

仓库快照中的包版本（`packages/*/package.json`）：

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerequisites ✅

- 浏览器使用：现代浏览器，支持 `MediaDevices.getUserMedia`
- 本地开发：Node.js + npm workspaces
- 文档开发：Python + Poetry（用于 MkDocs 构建）

基于 CI 配置的建议本地基线：

- Node.js 18.x
- Python 3.10.x

## Installation 📦

安装浏览器端包：

```bash
npm i @ricky0123/vad-web
```

安装 React 包装器：

```bash
npm i @ricky0123/vad-react
```

安装 monorepo 依赖（供贡献者使用）：

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

在浏览器里通过 script 标签使用 VAD，请引入以下脚本：

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

常见参数如下：

- `positiveSpeechThreshold`（实时 API 默认约为 `0.3`）
- `negativeSpeechThreshold`（实时 API 默认约为 `0.25`）
- `redemptionMs`（实时 API 默认约为 `1400`）
- `preSpeechPadMs`（实时 API 默认约为 `800`）
- `minSpeechMs`（实时 API 默认约为 `400`）

实时 API（`MicVAD`、`useMicVAD`）还支持：

- `getStream`、`pauseStream`、`resumeStream`
- `onFrameProcessed`、`onSpeechStart`、`onSpeechRealStart`、`onSpeechEnd`、`onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` 或 `"v5"`）
- `baseAssetPath` 和 `onnxWASMBasePath`
- `workletOptions`

完整 API 表见文档：[API reference](https://docs.vad.ricky0123.com/user-guide/api/) 与 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### Configuration recipe: self-hosting model and runtime assets

若不使用 CDN 默认值，请确保你的应用能提供以下资源：

- `silero_vad_legacy.onnx` 和/或 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 运行时文件（`.wasm`，以及较新运行时的 `.mjs`）

然后按如下配置：

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

仓库示例：

- `examples/script-tags`：基础 script tag 示例
- `examples/bundler`：`webpack` + `@ricky0123/vad-web`
- `examples/react-bundler`：`webpack` + `@ricky0123/vad-react`
- `examples/nextjs`：Next.js 集成示例

`examples/bundler` 示例命令：

```bash
npm run build && npm run start
```

在浏览器中打包 VAD，或在 Node/React 项目中使用，详见 [vad.ricky0123.com](https://www.vad.ricky0123.com)。

## Development Notes 🛠️

仓库根目录脚本：

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

它们的作用：

- `npm run build`：构建所有 workspace
- `npm run test`：运行 workspace 测试
- `npm run test:coverage`：`packages/web` 覆盖率
- `npm run typecheck`：检查 `packages`、`test-site` 和测试的 TypeScript
- `npm run format-check`：检查 `packages`、`examples`、`test-site` 下 TS/TSX 的格式
- `npm run dev`：监听 package 与 test-site 源码、重建并服务 `test-site/dist`

文档构建（MkDocs + Poetry）：

```bash
poetry install
poetry run mkdocs serve
```

补充说明：

- `./test-site/build.sh` 会将所需 VAD/ONNX Runtime 资源复制到 `test-site/dist` 和 `test-site/dist/subpath`
- `./scripts/dev.sh` 使用 `nodemon` + `live-server` 在本地循环重建并监听 `8080` 端口
- `./check_vad_up_to_date.sh` 为历史遗留脚本，仍引用 `silero_vad.onnx`（而仓库实际提供 `silero_vad_legacy.onnx` 与 `silero_vad_v5.onnx`）

## CI & Quality Gates 🧱

`.github/workflows/` 下的 GitHub 工作流包括：

- 测试（`test.yml`）
- 类型检查（`typecheck.yml`）
- 格式检查（`format-check.yml`）
- 文档构建/部署（`docs.yml`）
- 发布流程（`publish.yml`）

这些工作流是当前可执行环境版本与发布校验的实际准则。

## Troubleshooting 🩺

| 症状 | 检查与修复 |
| --- | --- |
| 麦克风权限被拒绝 | 确保浏览器已允许你的站点访问麦克风权限 |
| 资源加载失败（`.onnx`、`.wasm`、`.mjs`、worklet） | 正确设置 `baseAssetPath` / `onnxWASMBasePath`，并确认文件已正确提供 |
| 新版 `onnxruntime-web` 运行时问题 | 需要同时提供 `.mjs` 文件，不只是 `.wasm` |
| 本地开发使用不安全源（非 HTTPS） | 浏览器麦克风 API 通常要求安全上下文（`https` 或 `localhost`） |
| 打包构建阶段问题 | 按[浏览器文档](https://docs.vad.ricky0123.com/user-guide/browser/)提供的打包指引处理 |
| Next.js 集成问题 | 按 [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) 中的配置模式，并核对静态资源托管路径 |

## Sponsorship ❤️

若你的产品是商业用途，欢迎对项目进行经济支持：[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Important update about node support - Oct 2024 📢

我将逐步停用 `ricky0123/vad-node`（用于服务端 Node 场景的语音活动检测包）。从现在开始，我不再计划继续发布 node 包更新。我做出该决定的原因如下：

- 这个项目最初的目标是客户端语音活动检测。最初我因为有人提出需求才加上了 node 支持，也希望能帮到更多人，但我的投入时间有限，停用 `ricky0123/vad-node` 能让我把更多时间用于 `ricky0123/vad-web`。
- 相比学习 onnxruntime-web、audio worklet 等前端技术并自己实现一个客户端方案，很多开发者更容易自行构建服务端语音活动检测方案。因此我认为 `ricky0123/vad-web` 对社区更有价值。
- 浏览器包和 node 包之间在模型运行与调用方式上有环境差异，代码共享并不顺畅。
- 根据[调研问卷](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)，大多数用户在使用 `ricky0123/vad-web`（可能搭配 `ricky0123/vad-react`）。

## Roadmap 🛣️

当前方向（基于仓库现状和维护者说明）：

- 继续聚焦浏览器优先 API（`@ricky0123/vad-web`、`@ricky0123/vad-react`）
- 维护并完善面向打包器和框架的文档与示例
- 提升贡献者/开发者文档与 test-site 工作流
- 补充并维护 `i18n/` 下的多语言 README

## Contributing 🤝

- 阅读开发指南：[docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 在仓库提交 Issue 或 PR：[github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 想快速理解项目上下文，请查看 [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD 仓库：[github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

- 项目许可：ISC（见 [LICENSE](LICENSE)）
