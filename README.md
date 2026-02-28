[English](README.md) · [العربية](i18n/README.ar.md) · [Español](i18n/README.es.md) · [Français](i18n/README.fr.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [Tiếng Việt](i18n/README.vi.md) · [中文 (简体)](i18n/README.zh-Hans.md) · [中文（繁體）](i18n/README.zh-Hant.md) · [Deutsch](i18n/README.de.md) · [Русский](i18n/README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Voice Activity Detection for JavaScript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Run callbacks on segments of audio with user speech in a few lines of code.

This package aims to provide an accurate, user-friendly voice activity detector (VAD) that runs in the browser. By using this package, you can prompt the user for microphone permissions, start recording audio, send segments of audio with speech to your server for processing, or show a certain animation or indicator when the user is speaking. Note that I have decided [to discontinue node support](#important-update-about-node-support---oct-2024-) in order to focus on the browser use case.

| At a glance | Details |
| --- | --- |
| Core packages | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Primary runtime | Browser (`WebAudio` + `getUserMedia`) |
| Docs | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Live demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

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
| Live demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Join the community](https://discord.gg/4WPeGEaSpF) |
| Survey | [Share your use case](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Contributing guide | [Developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Documentation source lives in `./docs`.
- Contributor onboarding starts here: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Questions are welcome via issues or Discord.

Under the hood, these packages run [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references) using [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (with historical references to ONNX Runtime Node.js from earlier Node support). Thanks a lot to those folks for making this possible.

Note on i18n status: `i18n/` includes translated README files for the language options linked at the top of this file.

## Overview 🧭

This repository is a monorepo with two primary published packages:

| Package | Purpose |
| --- | --- |
| `@ricky0123/vad-web` | Browser APIs including `MicVAD`, `AudioNodeVAD`, and `NonRealTimeVAD` |
| `@ricky0123/vad-react` | React hook wrapper (`useMicVAD`) for `vad-web` |

The project is browser-first and includes:

- Real-time microphone segmentation callbacks (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Configurable algorithm thresholds and timing controls
- Legacy and v5 Silero model support
- Demo/test apps and docs site sources in this repository

## Features ✨

- Browser-first VAD pipeline powered by Silero ONNX models
- Works with script tags, bundlers, and React
- Sensible default microphone stream constraints
- Override-able stream lifecycle (`getStream`, `pauseStream`, `resumeStream`)
- Non-real-time speech segmentation for pre-recorded audio via `NonRealTimeVAD`
- Configurable model/asset loading via `baseAssetPath` and `onnxWASMBasePath`
- Supports both legacy and v5 model state handling via built-in wrappers
- Includes examples for script tags, webpack-based bundlers, React bundlers, and Next.js

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

More detailed paths:

- `packages/web/src/real-time-vad.ts`: real-time microphone/audio-node VAD orchestration
- `packages/web/src/non-real-time-vad.ts`: async segmentation for prerecorded audio
- `packages/web/src/frame-processor.ts`: thresholding and speech segment boundary logic
- `packages/react/src/index.ts`: `useMicVAD` React hook lifecycle and state wrapper

## Compatibility Matrix 🧩

| Component | Environment |
| --- | --- |
| `@ricky0123/vad-web` | Modern browsers with WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | React apps (`react` / `react-dom` >= 16.8.0) |
| Docs toolchain | Python 3.10 + Poetry (per CI workflow) |
| CI Node runtime | Node 18 (per repository workflows) |

Repository snapshot package versions (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerequisites ✅

- Browser usage: a modern browser with `MediaDevices.getUserMedia`
- Local development: Node.js + npm workspaces
- Docs development: Python + Poetry (for MkDocs build)

Recommended local baseline based on CI config:

- Node.js 18.x
- Python 3.10.x

## Installation 📦

Install the browser package:

```bash
npm i @ricky0123/vad-web
```

Install the React wrapper:

```bash
npm i @ricky0123/vad-react
```

Install monorepo dependencies (for contributors):

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

To use the VAD via a script tag in the browser, include the following script tags:

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

Common options across the APIs include:

- `positiveSpeechThreshold` (default around `0.3` in real-time APIs)
- `negativeSpeechThreshold` (default around `0.25` in real-time APIs)
- `redemptionMs` (default around `1400` in real-time APIs)
- `preSpeechPadMs` (default around `800` in real-time APIs)
- `minSpeechMs` (default around `400` in real-time APIs)

Real-time APIs (`MicVAD`, `useMicVAD`) also support:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` or `"v5"`)
- `baseAssetPath` and `onnxWASMBasePath`
- `workletOptions`

See full API tables in the docs: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) and [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Configuration recipe: self-hosting model and runtime assets

When not using CDN defaults, make sure your app serves:

- `silero_vad_legacy.onnx` and/or `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` runtime files (`.wasm`; and `.mjs` for newer runtime builds)

Then configure:

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

Repository examples:

- `examples/script-tags`: basic script-tag setup
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js integration example

Example command from `examples/bundler`:

```bash
npm run build && npm run start
```

Documentation for bundling the voice activity detector for the browser or using it in node or React projects can be found on [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Development Notes 🛠️

Root workspace scripts:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

What they do:

- `npm run build`: builds all workspaces
- `npm run test`: runs workspace tests
- `npm run test:coverage`: coverage for `packages/web`
- `npm run typecheck`: checks TypeScript in packages, test-site, and tests
- `npm run format-check`: checks formatting for TS/TSX under `packages`, `examples`, `test-site`
- `npm run dev`: watches package and test-site sources, rebuilds, and serves `test-site/dist`

Docs build (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Additional notes:

- `./test-site/build.sh` copies required VAD/ONNX Runtime assets into `test-site/dist` and `test-site/dist/subpath`
- `./scripts/dev.sh` uses `nodemon` + `live-server` for local rebuild-and-serve loops on port `8080`
- `./check_vad_up_to_date.sh` is historical and references `silero_vad.onnx` (while this repo ships `silero_vad_legacy.onnx` and `silero_vad_v5.onnx`)

## CI & Quality Gates 🧱

GitHub workflows in `.github/workflows/` cover:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Docs build/deploy (`docs.yml`)
- Publish flow (`publish.yml`)

These workflows are a practical source of truth for expected runtime/tool versions and release checks.

## Troubleshooting 🩺

| Symptom | Check / Fix |
| --- | --- |
| Mic permission denied | Ensure the browser has microphone permission for your origin. |
| Assets fail to load (`.onnx`, `.wasm`, `.mjs`, worklet) | Set `baseAssetPath` / `onnxWASMBasePath` correctly and verify files are actually served. |
| Newer `onnxruntime-web` runtime issues | Also serve `.mjs` files, not just `.wasm`. |
| Local dev over insecure origin | Browser mic APIs typically require secure contexts (`https` or `localhost`). |
| Build-time bundler issues | Use the bundling guidance in [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Next.js integration issues | Use configuration patterns shown in [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) and verify static asset hosting paths. |

## Sponsorship ❤️

Please contribute to the project financially - especially if your commercial product relies on this package. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Important update about node support - Oct 2024 📢

I am going to wind down support for `ricky0123/vad-node`, the voice activity detection package for server-side node environments. I do not plan to publish any updates to the node package from here on out. I made this decision for the following reasons:

- My original use case for this project was client-side voice activity detection. I added node support because someone requested it and I wanted to be helpful. However, I don't have a lot of time to work on this project, and deprecating `ricky0123/vad-node` will give me more time to focus on `ricky0123/vad-web`.
- It is much easier for individual developers to create custom server-side voice activity detection solutions than it is for developers to learn how to work with onnxruntime-web, audio worklets, and other technologies to produce a client-side solution. Therefore, I see `ricky0123/vad-web` as providing more value to the community.
- Sharing code between the browser and node packages is fairly awkward because the environments are different in ways that are relevant to running and using the voice activity detection model.
- Most users, according to the [survey](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), are using `ricky0123/vad-web` (possibly with `ricky0123/vad-react`).

## Roadmap 🛣️

Current direction (based on repository state and maintainer note above):

- Continue focusing on browser-first APIs (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Maintain and improve docs/examples for bundlers and frameworks
- Improve contributor/developer documentation and test-site workflows
- Add and maintain translated READMEs under `i18n/`

## Contributing 🤝

- Read the hacking guide: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Open issues or PRs in this repository: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- For quick project context, see [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## License 📄

- Project license: ISC (see [LICENSE](LICENSE))
