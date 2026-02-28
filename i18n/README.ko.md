[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript용 음성 활동 감지(VAD)

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 코드 몇 줄만으로 사용자 음성이 있는 오디오 구간에서 콜백을 실행하세요.

이 패키지는 브라우저에서 동작하는 정확하고 사용하기 쉬운 음성 활동 감지기(VAD)를 제공하는 것을 목표로 합니다. 이 패키지를 사용하면 마이크 권한을 요청하고, 오디오 녹음을 시작하며, 음성이 포함된 오디오 구간을 서버로 전송해 처리하거나, 사용자가 말할 때 특정 애니메이션/표시기(indicator)를 보여 줄 수 있습니다. 또한 브라우저 사용 사례에 집중하기 위해 [Node 지원을 중단](#important-update-about-node-support---oct-2024-)하기로 결정했습니다.

| 한눈에 보기 | 상세 정보 |
| --- | --- |
| 핵심 패키지 | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 기본 런타임 | 브라우저 (`WebAudio` + `getUserMedia`) |
| 문서 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 라이브 데모 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

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

| 리소스 | 링크 |
| --- | --- |
| 라이브 데모 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 문서 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [커뮤니티에 참여하기](https://discord.gg/4WPeGEaSpF) |
| 설문 | [사용 사례 공유하기](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 기여 가이드 | [개발자 해킹 가이드](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 문서 원본은 `./docs`에 있습니다.
- 기여자 온보딩은 여기서 시작하세요: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). 질문은 issue 또는 Discord로 받습니다.

기본 동작은 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references) 기반이며, [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web)를 사용합니다(예전 Node 지원 시절에는 ONNX Runtime Node.js의 역사적 참고사항이 있었습니다). 이 기능을 가능하게 해 준 분들께 감사드립니다.

참고: `i18n/`에는 이 파일 상단에 링크된 언어 옵션의 번역본 README가 들어 있습니다.

## Overview 🧭

이 저장소는 다음 두 개의 공개 패키지가 있는 모노레포입니다.

| 패키지 | 용도 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`, `AudioNodeVAD`, `NonRealTimeVAD`를 포함한 브라우저 API |
| `@ricky0123/vad-react` | `vad-web`용 React 훅 래퍼 (`useMicVAD`) |

해당 프로젝트는 브라우저 우선이며 다음을 포함합니다:

- 실시간 마이크 분할 콜백 (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` 등)
- 설정 가능한 알고리즘 임계값/타이밍 제어
- 레거시 및 v5 Silero 모델 지원
- 데모/테스트 앱과 문서 사이트 소스가 이 저장소에 포함

## Features ✨

- Silero ONNX 모델 기반 브라우저 우선 VAD 파이프라인
- script 태그, 번들러, React와 함께 사용 가능
- 실용적인 기본 마이크 스트림 제약 조건
- 스트림 생명주기 오버라이드 가능 (`getStream`, `pauseStream`, `resumeStream`)
- `NonRealTimeVAD`로 사전 녹음 오디오 비실시간 음성 분할
- `baseAssetPath`와 `onnxWASMBasePath`로 모델/에셋 로딩 구성
- 내장 래퍼를 통해 레거시/ v5 모델 상태 처리 모두 지원
- script 태그, webpack 기반 번들러, React 번들러, Next.js 예제 포함

## Project Structure 🗂️

```text
.
├── README.md
├── docs/                     # docs.vad.ricky0123.com용 MkDocs 소스
├── examples/                 # script-tag, bundler, react-bundler, nextjs 예제
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # 개발 보조 스크립트
├── test-site/                # 로컬 인터랙티브 플레이그라운드
├── i18n/                     # 번역된 README 파일
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

더 자세한 경로는 다음과 같습니다:

- `packages/web/src/real-time-vad.ts`: 실시간 마이크/audio-node VAD 오케스트레이션
- `packages/web/src/non-real-time-vad.ts`: 미리 녹음한 오디오용 비동기 분할
- `packages/web/src/frame-processor.ts`: 임계값 처리 및 음성 구간 경계 로직
- `packages/react/src/index.ts`: `useMicVAD` React 훅의 생명주기 및 상태 래퍼

## Compatibility Matrix 🧩

| 구성요소 | 환경 |
| --- | --- |
| `@ricky0123/vad-web` | WebAudio + `MediaDevices.getUserMedia`를 지원하는 최신 브라우저 |
| `@ricky0123/vad-react` | React 앱 (`react` / `react-dom` >= 16.8.0) |
| 문서 도구 체인 | Python 3.10 + Poetry (CI 워크플로우 기준) |
| CI Node 런타임 | Node 18 (레포지토리 워크플로우 기준) |

저장소 스냅샷 패키지 버전 (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerequisites ✅

- 브라우저 사용: `MediaDevices.getUserMedia`
- 로컬 개발: Node.js + npm 워크스페이스
- 문서 개발: Python + Poetry (MkDocs 빌드용)

CI 설정 기준 권장 로컬 환경:

- Node.js 18.x
- Python 3.10.x

## Installation 📦

브라우저 패키지 설치:

```bash
npm i @ricky0123/vad-web
```

React 래퍼 설치:

```bash
npm i @ricky0123/vad-react
```

모노레포 의존성 설치(기여자용):

```bash
npm install
```

## Usage 🚀

### Quick Start (script tags)

브라우저에서 script 태그로 VAD를 사용하려면 다음 태그들을 포함하세요.

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

API 전반에서 공통으로 사용하는 옵션:

- `positiveSpeechThreshold` (실시간 API 기본값 약 `0.3`)
- `negativeSpeechThreshold` (실시간 API 기본값 약 `0.25`)
- `redemptionMs` (실시간 API 기본값 약 `1400`)
- `preSpeechPadMs` (실시간 API 기본값 약 `800`)
- `minSpeechMs` (실시간 API 기본값 약 `400`)

실시간 API (`MicVAD`, `useMicVAD`)도 다음을 지원합니다:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` 또는 `"v5"`)
- `baseAssetPath` 및 `onnxWASMBasePath`
- `workletOptions`

자세한 API는 문서의 [API reference](https://docs.vad.ricky0123.com/user-guide/api/)와 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)를 참고하세요.

### Configuration recipe: self-hosting model and runtime assets

CDN 기본값을 사용하지 않을 때는 앱에서 다음 항목을 제공해야 합니다:

- `silero_vad_legacy.onnx` 및/또는 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 런타임 파일 (`.wasm`; 최근 런타임 빌드는 `.mjs`도 필요)

그다음 이렇게 설정하세요:

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

저장소 예제:

- `examples/script-tags`: 기본 script 태그 설정
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js 통합 예제

`examples/bundler` 실행 명령:

```bash
npm run build && npm run start
```

브라우저용 음성 활동 감지기 번들링이나 node/React 프로젝트에서 사용 방법은 [vad.ricky0123.com](https://www.vad.ricky0123.com)에서 확인할 수 있습니다.

## Development Notes 🛠️

루트 워크스페이스 스크립트:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

각 스크립트 설명:

- `npm run build`: 모든 워크스페이스 빌드
- `npm run test`: 워크스페이스 테스트 실행
- `npm run test:coverage`: `packages/web` 커버리지 실행
- `npm run typecheck`: `packages/web`, `test-site`, `tests`의 TypeScript 검사
- `npm run format-check`: `packages`, `examples`, `test-site`에서 TS/TSX 포맷 검사
- `npm run dev`: 패키지 및 test-site 소스 감시, 재빌드, `test-site/dist` 서빙

문서 빌드 (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

추가 참고사항:

- `./test-site/build.sh`는 필수 VAD/ONNX Runtime 에셋을 `test-site/dist` 및 `test-site/dist/subpath`로 복사합니다.
- `./scripts/dev.sh`는 포트 `8080`에서 로컬 재빌드·서빙 루프를 위해 `nodemon` + `live-server`를 사용합니다.
- `./check_vad_up_to_date.sh`는 과거 스크립트로 `silero_vad.onnx`를 참조합니다(현재 저장소는 `silero_vad_legacy.onnx`와 `silero_vad_v5.onnx`를 제공합니다).

## CI & Quality Gates 🧱

`.github/workflows/`의 GitHub 워크플로우는 다음을 다룹니다:

- 테스트 (`test.yml`)
- 타입 검사 (`typecheck.yml`)
- 포맷 검사 (`format-check.yml`)
- 문서 빌드/배포 (`docs.yml`)
- 배포 흐름 (`publish.yml`)

이 워크플로우는 기대 런타임/도구 버전과 배포 체크의 실질적 기준입니다.

## Troubleshooting 🩺

| 증상 | 점검/해결 |
| --- | --- |
| 마이크 권한 거부됨 | 브라우저에서 오리진에 대한 마이크 권한이 허용되어 있는지 확인하세요. |
| 에셋 로드 실패 (`.onnx`, `.wasm`, `.mjs`, worklet) | `baseAssetPath`/`onnxWASMBasePath` 값을 정확히 설정하고 파일이 실제로 서빙되는지 확인하세요. |
| 최신 `onnxruntime-web` 런타임 문제 | `.wasm`만이 아닌 `.mjs`도 함께 제공해야 합니다. |
| 보안되지 않은 오리진에서 로컬 개발 | 브라우저 마이크 API는 일반적으로 보안 컨텍스트(`https` 또는 `localhost`)를 요구합니다. |
| 빌드 시 번들러 이슈 | [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/)의 번들링 가이드를 참고하세요. |
| Next.js 통합 이슈 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js)의 설정 패턴을 사용하고 정적 에셋 호스팅 경로를 확인하세요. |

## Sponsorship ❤️

프로젝트에 재정적으로 기여해 주세요. 특히 상용 제품이 이 패키지에 의존한다면 더 도움이 됩니다. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2f)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Important update about node support - Oct 2024 📢

이후로 `ricky0123/vad-node`(서버 측에서 사용하는 음성 활동 감지 패키지)에 대한 지원을 축소할 예정입니다. 앞으로는 node 패키지 업데이트를 더 이상 발표할 계획이 없습니다. 이 결정을 내린 이유는 다음과 같습니다:

- 이 프로젝트의 원래 사용 사례는 클라이언트 측 음성 활동 감지였습니다. 누군가의 요청으로 node 지원을 추가했지만, 현재 프로젝트를 진행할 시간이 충분하지 않아 `ricky0123/vad-node`를 종료하면 `ricky0123/vad-web`에 더 집중할 수 있습니다.
- 브라우저 측 해결책을 만들려면 onnxruntime-web, audio worklet 같은 기술과 작업해야 하므로, 개별 개발자가 서버 측 맞춤형 VAD 솔루션을 직접 만드는 것이 더 쉽습니다. 따라서 커뮤니티에 더 큰 가치를 주는 쪽은 `ricky0123/vad-web`이라고 판단합니다.
- 브라우저 패키지와 node 패키지 간 코드 공유는 실행/사용 환경의 차이 때문에 꽤 까다롭습니다.
- [설문조사](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)에 따르면 대부분의 사용자가 `ricky0123/vad-web`(필요시 `ricky0123/vad-react`)를 사용합니다.

## Roadmap 🛣️

현재 방향(저장소 상태와 유지관리자 공지를 기준으로):

- 브라우저 우선 API (`@ricky0123/vad-web`, `@ricky0123/vad-react`)에 계속 집중
- 번들러/프레임워크 대상 문서 및 예제 유지/개선
- 기여자/개발자 문서와 test-site 워크플로우 개선
- `i18n/` 아래에서 번역 README 추가 및 유지

## Contributing 🤝

- 해킹 가이드를 읽으세요: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 이 저장소에서 issue 또는 PR 열기: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 프로젝트 빠른 맥락 파악: [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD 저장소: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## License 📄

- 프로젝트 라이선스: ISC ([LICENSE](LICENSE) 참조)
