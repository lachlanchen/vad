[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


---

[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript용 음성 활동 감지(VAD)

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

> 코드 몇 줄만으로 사용자 발화 구간에서 콜백을 실행하세요.

이 패키지는 브라우저에서 동작하는 정확하고 사용하기 쉬운 음성 활동 감지기(VAD)를 제공하는 것을 목표로 합니다. 이 패키지를 사용하면 마이크 권한 요청, 오디오 녹음 시작, 발화가 포함된 오디오 조각을 서버로 보내 처리, 사용자가 말할 때 특정 애니메이션이나 표시기 노출을 처리할 수 있습니다. 브라우저 사용 사례에 집중하기 위해 [Node 지원을 중단](#important-update-about-node-support---oct-2024-)하기로 결정했습니다.

| 🧭 한눈에 보기 | 세부 내용 |
| --- | --- |
| 📦 핵심 패키지 | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 기본 실행 환경 | 브라우저 (`WebAudio` + `getUserMedia`) |
| 📚 문서 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 실시간 데모 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## 목차

- [빠른 링크 🔗](#빠른-링크-)
- [개요 🧭](#개요-)
- [기능 ✨](#기능-)
- [프로젝트 구조 🗂️](#프로젝트-구조-)
- [호환성 매트릭스 🧩](#호환성-매트릭스-)
- [사전 요구사항 ✅](#사전-요구사항-)
- [설치 📦](#설치-)
- [사용법 🚀](#사용법-)
- [설정 ⚙️](#설정-)
- [예시 🧪](#예시-)
- [개발 노트 🛠️](#개발-노트-)
- [CI 및 품질 게이트 🧱](#ci-및-품질-게이트-)
- [문제 해결 🩺](#문제-해결-)
- [후원 ❤️](#후원-)
- [중요 공지: Node 지원 변경 - 2024년 10월 📢](#important-update-about-node-support---oct-2024-)
- [로드맵 🛣️](#로드맵-)
- [기여하기 🤝](#기여하기-)
- [참고 자료 📚](#참고-자료-)
- [❤️ Support](#-support)
- [라이선스 📄](#라이선스-)

## 빠른 링크 🔗

| 자료 | 링크 |
| --- | --- |
| 실시간 데모 | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| 문서 | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [커뮤니티 참여](https://discord.gg/4WPeGEaSpF) |
| 설문 | [사용 사례 공유](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 기여 가이드 | [개발자 가이드](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- 문서 소스는 `./docs`에 있습니다.
- 기여자 오리엔테이션은 [개발자 가이드](https://docs.vad.ricky0123.com/developer-guide/hacking/)에서 시작하세요. 질문은 issue나 Discord로 남겨 주세요.

근본적으로 이 패키지들은 [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#참고-자료-)를 사용해 [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (이전 Node 지원 시점의 ONNX Runtime Node.js 참고 자료 포함)로 동작합니다. 이 기능을 가능하게 해 준 모든 분들께 감사드립니다.

참고로 `i18n/`에는 이 파일 상단에 있는 언어 링크에 포함된 번역본들이 들어 있습니다.

## 개요 🧭

이 저장소는 두 가지 공개 패키지를 가진 모노레포입니다:

| 패키지 | 용도 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`, `AudioNodeVAD`, `NonRealTimeVAD`를 제공하는 브라우저 API |
| `@ricky0123/vad-react` | `vad-web`용 React 훅 래퍼 (`useMicVAD`) |

이 프로젝트는 브라우저 우선이며 다음을 포함합니다.

- 실시간 마이크 세분화 콜백 (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` 등)
- 조절 가능한 알고리즘 임계값 및 타이밍 제어
- 레거시 및 v5 Silero 모델 지원
- 데모/테스트 앱과 문서 사이트 소스가 같은 저장소에 포함

## 기능 ✨

- Silero ONNX 모델 기반의 브라우저 우선 VAD 파이프라인
- script 태그, 번들러, React에서 사용 가능
- 실용적인 기본 마이크 스트림 제약 조건
- 스트림 수명주기 오버라이드 (`getStream`, `pauseStream`, `resumeStream`)
- `NonRealTimeVAD`를 통한 사전 녹음 오디오의 비실시간 분할
- `baseAssetPath` 및 `onnxWASMBasePath`로 모델/에셋 로딩 구성
- 내장 래퍼에서 legacy와 v5 모델 상태 처리 모두 지원
- script 태그, webpack 기반 번들러, React 번들러, Next.js 예시 포함

## 프로젝트 구조 🗂️

```text
.
├── README.md
├── docs/                     # docs.vad.ricky0123.com의 MkDocs 소스
├── examples/                 # script-tag, bundler, react-bundler, nextjs 예제
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # 개발용 스크립트
├── test-site/                # 로컬 대화형 플레이그라운드
├── i18n/                     # 번역 README 파일
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

상세 경로:

- `packages/web/src/real-time-vad.ts`: 실시간 마이크/audio-node VAD 오케스트레이션
- `packages/web/src/non-real-time-vad.ts`: 사전 녹음 오디오용 비동기 분할
- `packages/web/src/frame-processor.ts`: 임계값 산정 및 발화 구간 경계 로직
- `packages/react/src/index.ts`: `useMicVAD` React 훅 수명주기와 상태 래퍼

## 호환성 매트릭스 🧩

| 구성 요소 | 환경 |
| --- | --- |
| `@ricky0123/vad-web` | `WebAudio` + `MediaDevices.getUserMedia`를 지원하는 최신 브라우저 |
| `@ricky0123/vad-react` | React 앱 (`react` / `react-dom` >= 16.8.0) |
| 문서 툴체인 | Python 3.10 + Poetry (CI 워크플로 기준) |
| CI Node 런타임 | Node 18 (레포지토리 워크플로 기준) |

저장소 스냅샷 패키지 버전 (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## 사전 요구사항 ✅

- 브라우저 사용: `MediaDevices.getUserMedia`를 지원하는 브라우저
- 로컬 개발: Node.js + npm workspaces
- 문서 개발: Python + Poetry (MkDocs 빌드용)

CI 기반 권장 로컬 기준:

- Node.js 18.x
- Python 3.10.x

## 설치 📦

브라우저 패키지 설치:

```bash
npm i @ricky0123/vad-web
```

React 래퍼 설치:

```bash
npm i @ricky0123/vad-react
```

모노레포 의존성 설치(기여자 대상):

```bash
npm install
```

## 사용법 🚀

### 빠른 시작 (script 태그)

브라우저에서 script 태그로 VAD를 사용하려면 아래 태그를 포함하세요.

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

### 브라우저 패키지 사용 (모듈 import)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React 사용

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

### 비실시간 사용 (batch 오디오)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## 설정 ⚙️

공통 옵션:

- `positiveSpeechThreshold` (실시간 API의 기본값 약 `0.3`)
- `negativeSpeechThreshold` (실시간 API의 기본값 약 `0.25`)
- `redemptionMs` (실시간 API의 기본값 약 `1400`)
- `preSpeechPadMs` (실시간 API의 기본값 약 `800`)
- `minSpeechMs` (실시간 API의 기본값 약 `400`)

실시간 API (`MicVAD`, `useMicVAD`)도 다음을 지원합니다.

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` 또는 `"v5"`)
- `baseAssetPath` 및 `onnxWASMBasePath`
- `workletOptions`

전체 API 표는 문서의 [API reference](https://docs.vad.ricky0123.com/user-guide/api/)와 [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)를 참고하세요.

### 구성 예시: 모델과 런타임 자산 자체 호스팅

CDN 기본값을 사용하지 않는 경우 앱이 다음 항목을 제공하는지 확인하세요.

- `silero_vad_legacy.onnx` 및/또는 `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` 런타임 파일 (`.wasm`; 최신 런타임 빌드는 `.mjs`)

그다음 다음처럼 설정합니다.

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## 예시 🧪

저장소 예시 목록:

- `examples/script-tags`: 기본 script 태그 설정
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js 통합 예시

`examples/bundler` 예시 실행:

```bash
npm run build && npm run start
```

브라우저용 음성 활동 감지기 번들링 또는 node/React 프로젝트에서의 사용 방법은 [vad.ricky0123.com](https://www.vad.ricky0123.com)에 문서가 있습니다.

## 개발 노트 🛠️

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
- `npm run typecheck`: `packages/web`, `test-site`, `tests`의 TypeScript 타입 검사
- `npm run format-check`: `packages`, `examples`, `test-site`의 TS/TSX 포맷 검사
- `npm run dev`: 패키지와 test-site 소스 감시, 재빌드, `test-site/dist` 서빙

문서 빌드 (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

추가 참고:

- `./test-site/build.sh`는 필요한 VAD/ONNX Runtime 자산을 `test-site/dist`와 `test-site/dist/subpath`로 복사합니다.
- `./scripts/dev.sh`는 `nodemon` + `live-server`를 사용해 로컬 재빌드 후 서버 제공 루프를 `8080` 포트에서 실행합니다.
- `./check_vad_up_to_date.sh`는 과거 스크립트로, `silero_vad.onnx`를 참조합니다(이 저장소는 `silero_vad_legacy.onnx`와 `silero_vad_v5.onnx`를 제공합니다).

## CI 및 품질 게이트 🧱

`.github/workflows/`의 GitHub 워크플로는 다음을 다룹니다:

- 테스트 (`test.yml`)
- 타입체크 (`typecheck.yml`)
- 포맷 검사 (`format-check.yml`)
- 문서 빌드/배포 (`docs.yml`)
- 배포 플로우 (`publish.yml`)

이 워크플로는 실제 실행 환경/도구 버전과 릴리스 검증의 실무 기준 역할을 합니다.

## 문제 해결 🩺

| 증상 | 점검 / 해결 |
| --- | --- |
| 마이크 권한 거부 | 브라우저에서 해당 원본(origin)의 마이크 권한이 허용되어 있는지 확인하세요. |
| 자산 로딩 실패 (`.onnx`, `.wasm`, `.mjs`, worklet) | `baseAssetPath` / `onnxWASMBasePath`를 정확히 설정하고 파일이 실제로 서빙되는지 확인하세요. |
| 최신 `onnxruntime-web` 런타임 이슈 | `.wasm` 파일만이 아니라 `.mjs` 파일도 함께 서빙하세요. |
| 보안되지 않은 origin에서 로컬 개발 | 브라우저 마이크 API는 보통 보안 컨텍스트(`https` 또는 `localhost`)가 필요합니다. |
| 빌드 시 번들러 이슈 | [브라우저 문서](https://docs.vad.ricky0123.com/user-guide/browser/)의 번들 가이드를 따라보세요. |
| Next.js 통합 이슈 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js)에 있는 설정 패턴을 참고해 정적 자산 호스팅 경로를 확인하세요. |

## 후원 ❤️

이 프로젝트를 재정적으로 후원해 주세요. 특히 상용 제품이 이 패키지에 의존한다면 기여가 큰 도움이 됩니다. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## important update about node support - oct 2024 📢

`ricky0123/vad-node`(서버 측 음성 활동 감지 패키지) 지원을 중단합니다. 앞으로는 이 저장소에서 node 패키지 업데이트를 더 이상 공개하지 않을 예정입니다. 이 결정을 내린 이유는 다음과 같습니다:

- 이 프로젝트의 초기 사용 사례는 클라이언트 측 음성 활동 감지였습니다. 누군가의 요청으로 node 지원을 추가했지만, 현재는 시간 투입이 제한돼 있어 `ricky0123/vad-node`를 중단하면 `ricky0123/vad-web`에 더 집중할 수 있습니다.
- 개인 개발자 입장에서 브라우저용 해법을 만들기 위해 onnxruntime-web, 오디오 워크렛, 기타 기술을 모두 익혀야 하는 것보다, 서버 측 음성 활동 감지 솔루션을 직접 구현하는 것이 더 쉬운 편입니다. 따라서 커뮤니티에는 `ricky0123/vad-web`이 더 큰 가치를 제공합니다.
- 브라우저 패키지와 node 패키지는 실행과 사용 모델이 다르므로 코드를 공유하기가 다소 번거롭습니다.
- [설문조사](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)에 따르면 대부분의 사용자가 `ricky0123/vad-web`(필요 시 `ricky0123/vad-react`)을 사용합니다.

## 로드맵 🛣️

현재 방향 (현재 저장소 상태와 메인테이너 노트 기준):

- 브라우저 우선 API (`@ricky0123/vad-web`, `@ricky0123/vad-react`)에 계속 집중
- 번들러와 프레임워크용 문서/예시를 유지하고 개선
- 기여자/개발자 문서와 test-site 워크플로 개선
- `i18n/` 아래 번역 README 추가 및 유지보수

## 기여하기 🤝

- 해킹 가이드 읽기: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- 이 저장소에서 issue 또는 PR 열기: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 프로젝트 전체 맥락은 [`HACKING.md`](HACKING.md) 참조

## 참고 자료 📚

1. Silero VAD 저장소: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## 라이선스 📄

- 프로젝트 라이선스: ISC ([LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
