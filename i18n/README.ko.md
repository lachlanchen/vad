[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Javascript용 음성 활동 감지 (VAD)

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 몇 줄의 코드로 사용자 음성이 포함된 오디오 구간에서 콜백을 실행하세요.

이 패키지는 브라우저에서 동작하는 정확하고 사용하기 쉬운 음성 활동 감지기(VAD)를 제공하는 것을 목표로 합니다. 이 패키지를 사용하면 마이크 권한 요청, 오디오 녹음 시작, 음성이 포함된 오디오 구간을 서버로 전송해 후처리, 또는 사용자가 말할 때 특정 애니메이션/인디케이터 표시를 할 수 있습니다. 참고로 브라우저 사용 사례에 집중하기 위해 [node 지원 중단](#important-update-about-node-support---oct-2024-)을 결정했습니다.

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

| 리소스 | 링크 |
| --- | --- |
| 라이브 데모 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 문서 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [커뮤니티 참여](https://discord.gg/4WPeGEaSpF) |
| 설문조사 | [사용 사례 공유](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 기여 가이드 | [개발자 해킹 가이드](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 문서 원본 소스는 `./docs` 디렉터리에 있습니다.
- 기여하고 싶다면 패키지 해킹 시작 가이드를 [여기](https://docs.vad.ricky0123.com/developer-guide/hacking/)에 작성해 두었습니다. 질문이 있다면 이 저장소에 이슈를 열거나 Discord에 메시지를 남겨 주세요.

내부적으로 이 패키지들은 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references)를 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node) 위에서 실행합니다. 이를 가능하게 해 준 모든 분들께 감사드립니다.

i18n 상태 참고: `i18n/` 디렉터리가 존재하며 여러 번역 README 파일을 포함합니다. 위의 언어 선택기에는 이 저장소 스냅샷에 아직 없을 수 있는 예정/플레이스홀더 번역(`README.de.md`, `README.ru.md`) 링크도 포함되어 있습니다.

## Overview 🧭

이 저장소는 두 개의 주요 퍼블리시 패키지로 구성된 모노레포입니다.

| 패키지 | 용도 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`, `AudioNodeVAD`, `NonRealTimeVAD`를 포함한 브라우저 API |
| `@ricky0123/vad-react` | `vad-web`용 React 훅 래퍼(`useMicVAD`) |

이 프로젝트는 브라우저 우선(browser-first)이며 다음을 포함합니다.

- 실시간 마이크 구간 분할 콜백 (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` 등)
- 알고리즘 임계값 및 타이밍 제어의 설정 가능성
- Legacy 및 v5 Silero 모델 지원
- 이 저장소에 포함된 데모/테스트 앱 및 문서 사이트 소스

## Features ✨

- Silero ONNX 모델 기반의 브라우저 우선 VAD 파이프라인
- script 태그, 번들러, React 환경에서 동작
- 합리적인 기본 마이크 스트림 제약값 제공
- 스트림 생명주기 오버라이드 가능 (`getStream`, `pauseStream`, `resumeStream`)
- `NonRealTimeVAD`를 통한 사전 녹음 오디오의 비실시간 음성 구간 분할
- `baseAssetPath` 및 `onnxWASMBasePath`를 통한 모델/에셋 로딩 설정
- 내장 래퍼를 통한 legacy와 v5 모델 상태 처리 모두 지원
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

더 자세한 경로:

- `packages/web/src/real-time-vad.ts`: 실시간 마이크/오디오 노드 VAD 오케스트레이션
- `packages/web/src/non-real-time-vad.ts`: 사전 녹음 오디오용 비동기 구간 분할
- `packages/web/src/frame-processor.ts`: 임계값 처리와 음성 구간 경계 로직
- `packages/react/src/index.ts`: `useMicVAD` React 훅 생명주기 및 상태 래퍼

## Compatibility Matrix 🧩

| 컴포넌트 | 환경 |
| --- | --- |
| `@ricky0123/vad-web` | WebAudio + `MediaDevices.getUserMedia`를 지원하는 최신 브라우저 |
| `@ricky0123/vad-react` | React 앱 (`react` / `react-dom` >= 16.8.0) |
| 문서 도구체인 | Python 3.10 + Poetry (CI 워크플로우 기준) |
| CI Node 런타임 | Node 18 (저장소 워크플로우 기준) |

가정 참고: 예제와 문서는 이 저장소 스냅샷의 현재 패키지 버전(`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`)과 일치합니다.

## Prerequisites ✅

- 브라우저 사용: `MediaDevices.getUserMedia`를 지원하는 최신 브라우저
- 로컬 개발: Node.js + npm workspaces
- 문서 개발: Python + Poetry (MkDocs 빌드용)

CI 설정 기반 권장 로컬 기준:

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

브라우저에서 script 태그로 VAD를 사용하려면 다음 script 태그를 포함하세요.

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

API 전반에서 공통으로 사용할 수 있는 옵션:

- `positiveSpeechThreshold` (실시간 API 기본값 약 `0.3`)
- `negativeSpeechThreshold` (실시간 API 기본값 약 `0.25`)
- `redemptionMs` (실시간 API 기본값 약 `1400`)
- `preSpeechPadMs` (실시간 API 기본값 약 `800`)
- `minSpeechMs` (실시간 API 기본값 약 `400`)

실시간 API (`MicVAD`, `useMicVAD`)는 다음도 지원합니다.

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` 또는 `"v5"`)
- `baseAssetPath` 및 `onnxWASMBasePath`
- `workletOptions`

전체 API 표는 문서를 참고하세요: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) 및 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Configuration recipe: self-hosting model and runtime assets

CDN 기본값을 사용하지 않는 경우, 앱에서 아래 파일을 제공해야 합니다.

- `silero_vad_legacy.onnx` 및/또는 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 런타임 파일 (`.wasm`; 최신 런타임 빌드에서는 `.mjs`도 필요)

그다음 이렇게 설정합니다:

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

- `examples/script-tags`: 기본 script-tag 설정
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js 통합 예제

`examples/bundler`의 예시 명령:

```bash
npm run build && npm run start
```

브라우저용 번들링, 또는 node/React 프로젝트에서의 사용 문서는 [vad.ricky0123.com](https://www.vad.ricky0123.com)에서 확인할 수 있습니다.

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

- `npm run build`: 모든 워크스페이스를 빌드
- `npm run test`: 워크스페이스 테스트 실행
- `npm run test:coverage`: `packages/web` 커버리지 실행
- `npm run typecheck`: packages, test-site, tests의 TypeScript 검사
- `npm run format-check`: `packages`, `examples`, `test-site` 하위 TS/TSX 포맷 검사
- `npm run dev`: 패키지 및 test-site 소스 변경 감시, 재빌드, `test-site/dist` 서빙

문서 빌드 (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

추가 참고:

- `./test-site/build.sh`는 필요한 VAD/ONNX Runtime 에셋을 `test-site/dist` 및 `test-site/dist/subpath`로 복사합니다.
- `./scripts/dev.sh`는 포트 `8080`에서 로컬 재빌드-서빙 루프를 위해 `nodemon` + `live-server`를 사용합니다.
- `./check_vad_up_to_date.sh`는 과거 스크립트이며 `silero_vad.onnx`를 참조합니다(현재 저장소에는 `silero_vad_legacy.onnx`, `silero_vad_v5.onnx`가 포함됨).

## CI & Quality Gates 🧱

`.github/workflows/`의 GitHub 워크플로우는 다음을 다룹니다.

- 테스트 (`test.yml`)
- 타입체크 (`typecheck.yml`)
- 포맷 검사 (`format-check.yml`)
- 문서 빌드/배포 (`docs.yml`)
- 퍼블리시 플로우 (`publish.yml`)

이 워크플로우들은 기대 런타임/도구 버전 및 릴리스 점검 항목의 실질적인 기준입니다.

## Troubleshooting 🩺

| 증상 | 점검 / 해결 |
| --- | --- |
| 마이크 권한 거부 | 브라우저에서 해당 origin에 마이크 권한이 허용되어 있는지 확인하세요. |
| 에셋 로드 실패 (`.onnx`, `.wasm`, `.mjs`, worklet) | `baseAssetPath` / `onnxWASMBasePath`를 올바르게 설정하고 파일이 실제로 서빙되는지 확인하세요. |
| 최신 `onnxruntime-web` 런타임 이슈 | `.wasm`뿐 아니라 `.mjs` 파일도 함께 제공하세요. |
| 안전하지 않은 origin에서 로컬 개발 | 브라우저 마이크 API는 일반적으로 보안 컨텍스트(`https` 또는 `localhost`)를 요구합니다. |
| 빌드 시 번들러 이슈 | [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/)의 번들링 가이드를 따르세요. |
| Next.js 통합 이슈 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js)의 설정 패턴을 사용하고 정적 에셋 호스팅 경로를 확인하세요. |

## Sponsorship ❤️

특히 상용 제품이 이 패키지에 의존한다면 프로젝트에 재정적으로 기여해 주세요. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Important update about node support - Oct 2024 📢

서버 측 node 환경용 음성 활동 감지 패키지 `ricky0123/vad-node` 지원을 단계적으로 종료할 예정입니다. 앞으로 node 패키지 업데이트는 배포하지 않을 계획입니다. 이유는 다음과 같습니다.

- 이 프로젝트의 원래 사용 사례는 클라이언트 측 음성 활동 감지였습니다. 누군가의 요청으로 node 지원을 추가했지만, 프로젝트에 투자할 시간이 많지 않아 `ricky0123/vad-node`를 정리하면 `ricky0123/vad-web`에 더 집중할 수 있습니다.
- 개별 개발자가 서버 측 맞춤 음성 활동 감지 솔루션을 만드는 것보다, onnxruntime-web, audio worklet 등으로 클라이언트 측 솔루션을 구성하는 방법을 익히는 편이 더 어렵습니다. 따라서 커뮤니티에 더 큰 가치를 제공하는 쪽은 `ricky0123/vad-web`이라고 판단했습니다.
- 브라우저 패키지와 node 패키지 간 코드 공유는, 모델 실행/사용에 영향을 주는 환경 차이 때문에 꽤 까다롭습니다.
- [설문조사](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)에 따르면 대부분의 사용자는 `ricky0123/vad-web`(및 경우에 따라 `ricky0123/vad-react`)을 사용하고 있습니다.

## Roadmap 🛣️

현재 방향(저장소 상태와 위 유지관리자 공지 기준):

- 브라우저 우선 API(`@ricky0123/vad-web`, `@ricky0123/vad-react`)에 계속 집중
- 번들러/프레임워크용 문서 및 예제를 유지·개선
- 기여자/개발자 문서와 test-site 워크플로우 개선
- `i18n/` 하위 번역 README 추가 및 유지

## Contributing 🤝

- 해킹 가이드 읽기: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 이 저장소에서 이슈 또는 PR 열기: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 빠른 프로젝트 맥락 파악: [`HACKING.md`](HACKING.md)

## References 📚

1. Silero VAD 저장소: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## License 📄

- 프로젝트 라이선스: ISC ( [LICENSE](LICENSE) 참조)
