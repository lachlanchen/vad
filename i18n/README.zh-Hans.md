[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Javascript 语音活动检测

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 仅需几行代码，即可在检测到用户语音的音频片段上触发回调。

这个包旨在提供一个准确、易用、可在浏览器中运行的语音活动检测器（VAD）。使用该包，你可以向用户请求麦克风权限、开始录音、将包含语音的音频片段发送到服务器进行处理，或在用户说话时显示特定动画或指示器。请注意，我已决定[停止 Node 支持](#important-update-about-node-support---oct-2024-)以便专注于浏览器场景。

## 目录

- [快速链接 🔗](#quick-links-)
- [概览 🧭](#overview-)
- [特性 ✨](#features-)
- [项目结构 🗂️](#project-structure-)
- [兼容性矩阵 🧩](#compatibility-matrix-)
- [前置要求 ✅](#prerequisites-)
- [安装 📦](#installation-)
- [用法 🚀](#usage-)
- [配置 ⚙️](#configuration-)
- [示例 🧪](#examples-)
- [开发说明 🛠️](#development-notes-)
- [CI 与质量门禁 🧱](#ci--quality-gates-)
- [故障排查 🩺](#troubleshooting-)
- [赞助 ❤️](#sponsorship-)
- [关于 Node 支持的重要更新 - 2024 年 10 月 📢](#important-update-about-node-support---oct-2024-)
- [路线图 🛣️](#roadmap-)
- [贡献 🤝](#contributing-)
- [参考资料 📚](#references-)
- [许可证 📄](#license-)

<a id="quick-links-"></a>

## 快速链接 🔗

| 资源 | 链接 |
| --- | --- |
| 在线演示 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 文档 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [加入社区](https://discord.gg/4WPeGEaSpF) |
| 调研问卷 | [分享你的使用场景](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 贡献指南 | [开发者 hacking 指南](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 浏览文档，其源码位于 `./docs` 目录。
- 如果你想贡献，我已开始编写如何参与这些包开发的文档，见[这里](https://docs.vad.ricky0123.com/developer-guide/hacking/)。如有疑问，你可以在这里提 issue，或在 Discord 留言。

在底层，这些包通过 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node) 运行 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)。非常感谢这些项目的贡献者让这件事成为可能。

i18n 状态说明：`i18n/` 目录已存在，并包含多个已翻译的 README 文件。上方语言选择器也包含了计划中/占位用翻译链接（`README.de.md`、`README.ru.md`），这些文件在当前仓库快照中可能尚不存在。

<a id="overview-"></a>

## 概览 🧭

这个仓库是一个 monorepo，主要发布两个包：

| 包名 | 用途 |
| --- | --- |
| `@ricky0123/vad-web` | 浏览器 API，包括 `MicVAD`、`AudioNodeVAD` 和 `NonRealTimeVAD` |
| `@ricky0123/vad-react` | `vad-web` 的 React Hook 封装（`useMicVAD`） |

该项目以浏览器优先，并包含：

- 实时麦克风分段回调（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` 等）
- 可配置的算法阈值与时序控制
- 支持 Silero legacy 与 v5 模型
- 本仓库内的 demo/测试应用及文档站点源码

<a id="features-"></a>

## 特性 ✨

- 由 Silero ONNX 模型驱动、浏览器优先的 VAD 流水线
- 支持 script tags、bundler 与 React
- 提供合理的默认麦克风流约束
- 可覆盖的流生命周期（`getStream`、`pauseStream`、`resumeStream`）
- 通过 `NonRealTimeVAD` 对预录音频进行非实时语音分段
- 通过 `baseAssetPath` 与 `onnxWASMBasePath` 配置模型/资源加载
- 通过内置封装同时支持 legacy 与 v5 模型状态处理
- 提供 script tags、webpack bundler、React bundler 与 Next.js 示例

<a id="project-structure-"></a>

## 项目结构 🗂️

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

- `packages/web/src/real-time-vad.ts`：实时麦克风/AudioNode VAD 编排
- `packages/web/src/non-real-time-vad.ts`：用于预录音频的异步分段
- `packages/web/src/frame-processor.ts`：阈值与语音片段边界逻辑
- `packages/react/src/index.ts`：`useMicVAD` React Hook 的生命周期与状态封装

<a id="compatibility-matrix-"></a>

## 兼容性矩阵 🧩

| 组件 | 环境 |
| --- | --- |
| `@ricky0123/vad-web` | 支持 WebAudio + `MediaDevices.getUserMedia` 的现代浏览器 |
| `@ricky0123/vad-react` | React 应用（`react` / `react-dom` >= 16.8.0） |
| 文档工具链 | Python 3.10 + Poetry（按 CI workflow） |
| CI Node 运行时 | Node 18（按仓库 workflows） |

假设说明：示例和文档与该仓库快照中的当前包版本一致（`@ricky0123/vad-web@0.0.27`、`@ricky0123/vad-react@0.0.33`）。

<a id="prerequisites-"></a>

## 前置要求 ✅

- 浏览器使用：支持 `MediaDevices.getUserMedia` 的现代浏览器
- 本地开发：Node.js + npm workspaces
- 文档开发：Python + Poetry（用于 MkDocs 构建）

基于 CI 配置，推荐本地基线版本：

- Node.js 18.x
- Python 3.10.x

<a id="installation-"></a>

## 安装 📦

安装浏览器包：

```bash
npm i @ricky0123/vad-web
```

安装 React 封装：

```bash
npm i @ricky0123/vad-react
```

安装 monorepo 依赖（贡献者）：

```bash
npm install
```

<a id="usage-"></a>

## 用法 🚀

### 快速开始（script tags）

要在浏览器中通过 script tag 使用 VAD，请包含以下 script tags：

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

### 浏览器包用法（模块导入）

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React 用法

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

### 非实时用法（批处理音频）

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

<a id="configuration-"></a>

## 配置 ⚙️

这些 API 的常见选项包括：

- `positiveSpeechThreshold`（实时 API 中默认约为 `0.3`）
- `negativeSpeechThreshold`（实时 API 中默认约为 `0.25`）
- `redemptionMs`（实时 API 中默认约为 `1400`）
- `preSpeechPadMs`（实时 API 中默认约为 `800`）
- `minSpeechMs`（实时 API 中默认约为 `400`）

实时 API（`MicVAD`、`useMicVAD`）还支持：

- `getStream`、`pauseStream`、`resumeStream`
- `onFrameProcessed`、`onSpeechStart`、`onSpeechRealStart`、`onSpeechEnd`、`onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` 或 `"v5"`）
- `baseAssetPath` 与 `onnxWASMBasePath`
- `workletOptions`

完整 API 表请查看文档：[API reference](https://docs.vad.ricky0123.com/user-guide/api/) 与 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### 配置示例：自托管模型与运行时资源

当不使用 CDN 默认值时，请确保你的应用提供：

- `silero_vad_legacy.onnx` 和/或 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 运行时文件（`.wasm`；较新运行时构建还需要 `.mjs`）

然后这样配置：

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

<a id="examples-"></a>

## 示例 🧪

仓库中的示例：

- `examples/script-tags`：基础 script-tag 配置
- `examples/bundler`：webpack + `@ricky0123/vad-web`
- `examples/react-bundler`：webpack + `@ricky0123/vad-react`
- `examples/nextjs`：Next.js 集成示例

来自 `examples/bundler` 的示例命令：

```bash
npm run build && npm run start
```

关于在浏览器中打包语音活动检测器或在 Node/React 项目中使用它的文档，可在 [vad.ricky0123.com](https://www.vad.ricky0123.com) 查看。

<a id="development-notes-"></a>

## 开发说明 🛠️

根工作区脚本：

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

作用说明：

- `npm run build`：构建所有 workspaces
- `npm run test`：运行 workspace 测试
- `npm run test:coverage`：为 `packages/web` 生成覆盖率
- `npm run typecheck`：检查 packages、test-site 和 tests 中的 TypeScript
- `npm run format-check`：检查 `packages`、`examples`、`test-site` 下 TS/TSX 的格式
- `npm run dev`：监听 package 与 test-site 源码，重建并提供 `test-site/dist`

文档构建（MkDocs + Poetry）：

```bash
poetry install
poetry run mkdocs serve
```

补充说明：

- `./test-site/build.sh` 会把所需的 VAD/ONNX Runtime 资源复制到 `test-site/dist` 和 `test-site/dist/subpath`
- `./scripts/dev.sh` 使用 `nodemon` + `live-server` 在 `8080` 端口进行本地重建与服务循环
- `./check_vad_up_to_date.sh` 为历史脚本，仍引用 `silero_vad.onnx`（而此仓库实际提供 `silero_vad_legacy.onnx` 与 `silero_vad_v5.onnx`）

<a id="ci--quality-gates-"></a>

## CI 与质量门禁 🧱

`.github/workflows/` 中的 GitHub workflows 覆盖：

- 测试（`test.yml`）
- 类型检查（`typecheck.yml`）
- 格式检查（`format-check.yml`）
- 文档构建/部署（`docs.yml`）
- 发布流程（`publish.yml`）

这些 workflows 是预期运行时/工具版本和发布检查项的实用事实来源。

<a id="troubleshooting-"></a>

## 故障排查 🩺

| 症状 | 检查 / 修复 |
| --- | --- |
| 麦克风权限被拒绝 | 确认浏览器已为你的来源授予麦克风权限。 |
| 资源加载失败（`.onnx`、`.wasm`、`.mjs`、worklet） | 正确设置 `baseAssetPath` / `onnxWASMBasePath`，并确认文件确实已被服务。 |
| 较新 `onnxruntime-web` 运行时问题 | 除了 `.wasm` 外，还要提供 `.mjs` 文件。 |
| 非安全来源下的本地开发 | 浏览器麦克风 API 通常要求安全上下文（`https` 或 `localhost`）。 |
| 构建阶段的 bundler 问题 | 参考 [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/) 中的打包指引。 |
| Next.js 集成问题 | 参考 [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) 中的配置模式，并校验静态资源托管路径。 |

<a id="sponsorship-"></a>

## 赞助 ❤️

请为项目提供资金支持，尤其是在你的商业产品依赖此包的情况下。[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

<a id="important-update-about-node-support---oct-2024-"></a>

## 关于 Node 支持的重要更新 - 2024 年 10 月 📢

我将逐步停止对 `ricky0123/vad-node`（面向服务端 Node 环境的语音活动检测包）的支持。后续我不计划再发布该 Node 包的更新。我做出这个决定的原因如下：

- 这个项目最初的使用场景是客户端语音活动检测。我后来添加 Node 支持，是因为有人提出需求，我也想提供帮助。然而我能投入在这个项目上的时间有限，弃用 `ricky0123/vad-node` 能让我把更多精力投入到 `ricky0123/vad-web`。
- 与其让开发者学习 onnxruntime-web、audio worklets 等技术来构建客户端方案，个人开发者通常更容易按需实现定制的服务端语音活动检测方案。因此我认为 `ricky0123/vad-web` 能为社区提供更高价值。
- 由于浏览器与 Node 环境在运行和使用语音活动检测模型时存在关键差异，在两个包之间共享代码相当别扭。
- 根据[问卷](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)结果，大多数用户都在使用 `ricky0123/vad-web`（可能同时使用 `ricky0123/vad-react`）。

<a id="roadmap-"></a>

## 路线图 🛣️

当前方向（基于仓库状态和上方维护者说明）：

- 继续聚焦浏览器优先 API（`@ricky0123/vad-web`、`@ricky0123/vad-react`）
- 持续维护并改进面向 bundler 与框架的文档/示例
- 改进贡献者/开发者文档与 test-site 工作流
- 在 `i18n/` 下新增并维护翻译版 README

<a id="contributing-"></a>

## 贡献 🤝

- 阅读 hacking 指南：[docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 在本仓库提交 issue 或 PR：[github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 如需快速了解项目上下文，请查看 [`HACKING.md`](HACKING.md)

<a id="references-"></a>

## 参考资料 📚

1. Silero VAD 仓库：[github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

<a id="license-"></a>

## 许可证 📄

- 项目许可证：ISC（见 [LICENSE](LICENSE)）
