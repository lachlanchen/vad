[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Phát hiện hoạt động giọng nói cho JavaScript

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

> Chạy callback trên các đoạn âm thanh có tiếng nói của người dùng chỉ trong vài dòng mã.

Gói này nhằm mục tiêu cung cấp một công cụ phát hiện hoạt động giọng nói (VAD) chính xác, thân thiện và chạy trực tiếp trong trình duyệt. Khi dùng gói này, bạn có thể yêu cầu quyền micro của người dùng, bắt đầu ghi âm, gửi các đoạn âm có giọng nói lên máy chủ để xử lý, hoặc hiển thị animation/chỉ báo khi người dùng đang nói. Lưu ý là tôi đã quyết định [ngừng hỗ trợ node](#important-update-about-node-support---oct-2024-) để tập trung cho trường hợp dùng trên trình duyệt.

| 🧭 Tóm tắt nhanh | Chi tiết |
| --- | --- |
| 📦 Gói lõi | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 Môi trường chính | Trình duyệt (`WebAudio` + `getUserMedia`) |
| 📚 Tài liệu | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 Demo trực tiếp | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Mục lục

- [Liên kết nhanh 🔗](#liên-kết-nhanh-)
- [Tổng quan 🧭](#tổng-quan-)
- [Tính năng ✨](#tính-năng-)
- [Cấu trúc dự án 🗂️](#cấu-trúc-dự-án-)
- [Ma trận tương thích 🧩](#ma-trận-tương-thích-)
- [Điều kiện tiên quyết ✅](#điều-kiện-tiên-quyết-)
- [Cài đặt 📦](#cài-đặt-)
- [Sử dụng 🚀](#sử-dụng-)
- [Cấu hình ⚙️](#cấu-hình-)
- [Ví dụ 🧪](#ví-dụ-)
- [Ghi chú phát triển 🛠️](#ghi-chú-phát-triển-)
- [CI & Cổng chất lượng 🧱](#ci--cổng-chất-lượng-)
- [Khắc phục sự cố 🩺](#khắc-phục-sự-cố-)
- [Tài trợ ❤️](#tài-trợ-)
- [Cập nhật quan trọng về hỗ trợ Node - Tháng 10 2024 📢](#cập-nhật-quan-trọng-về-hỗ-trợ-node---tháng-10-2024-)
- [Lộ trình 🛣️](#lộ-trình-)
- [Đóng góp 🤝](#đóng-góp-)
- [Tài liệu tham khảo 📚](#tài-liệu-tham-khảo-)
- [❤️ Support](#-support)
- [Giấy phép 📄](#giấy-phép-)

## Liên kết nhanh 🔗

| Tài nguyên | Liên kết |
| --- | --- |
| Demo trực tiếp | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Tài liệu | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Gia nhập cộng đồng](https://discord.gg/4WPeGEaSpF) |
| Khảo sát | [Chia sẻ use-case của bạn](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Hướng dẫn đóng góp | [Hướng dẫn phát triển](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Mã nguồn tài liệu nằm trong `./docs`.
- Quá trình onboarding cho contributor bắt đầu tại đây: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Bạn có thể đặt câu hỏi qua issues hoặc Discord.

Về bản chất, các gói này chạy [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#tài-liệu-tham-khảo-) thông qua [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (cùng với tham chiếu lịch sử tới ONNX Runtime Node.js khi trước đây còn hỗ trợ Node). Xin cảm ơn các cộng sự đã giúp công nghệ này thành hiện thực.

Ghi chú về i18n: `i18n/` gồm các README được dịch cho các ngôn ngữ được liệt kê ở đầu file.

## Tổng quan 🧭

Repo này là một monorepo có hai gói công bố chính:

| Gói | Mục đích |
| --- | --- |
| `@ricky0123/vad-web` | Các API trình duyệt bao gồm `MicVAD`, `AudioNodeVAD` và `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper hook React (`useMicVAD`) cho `vad-web` |

Dự án ưu tiên trình duyệt và bao gồm:

- Callback phân đoạn microphone thời gian thực (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, ...)
- Ngưỡng thuật toán và kiểm soát thời gian có thể cấu hình
- Hỗ trợ mô hình Silero legacy và v5
- Ứng dụng demo/test và mã nguồn docs site trong repo này

## Tính năng ✨

- Pipeline VAD ưu tiên trình duyệt, chạy bằng mô hình Silero ONNX
- Hoạt động với script tags, bundler và React
- Giới hạn luồng micro mặc định hợp lý
- Có thể ghi đè vòng đời stream (`getStream`, `pauseStream`, `resumeStream`)
- Phân đoạn giọng nói không thời gian thực cho file đã ghi sẵn qua `NonRealTimeVAD`
- Tải mô hình/tài nguyên có thể cấu hình qua `baseAssetPath` và `onnxWASMBasePath`
- Hỗ trợ xử lý trạng thái mô hình legacy và v5 bằng wrapper tích hợp sẵn
- Có ví dụ cho script tags, webpack bundler, React bundler và Next.js

## Cấu trúc dự án 🗂️

```text
.
├── README.md
├── docs/                     # Nguồn MkDocs cho docs.vad.ricky0123.com
├── examples/                 # script-tag, bundler, react-bundler, ví dụ nextjs
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # công cụ phát triển
├── test-site/                # playground tương tác cục bộ
├── i18n/                     # các README đã dịch
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

Các đường dẫn chi tiết:

- `packages/web/src/real-time-vad.ts`: điều phối VAD thời gian thực cho microphone/audio-node
- `packages/web/src/non-real-time-vad.ts`: phân đoạn không đồng bộ cho audio đã thu sẵn
- `packages/web/src/frame-processor.ts`: logic ngưỡng và logic ranh giới đoạn giọng nói
- `packages/react/src/index.ts`: vòng đời hook `useMicVAD` và lớp bọc trạng thái

## Ma trận tương thích 🧩

| Thành phần | Môi trường |
| --- | --- |
| `@ricky0123/vad-web` | Trình duyệt hiện đại với WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Ứng dụng React (`react` / `react-dom` >= 16.8.0) |
| Công cụ tài liệu | Python 3.10 + Poetry (theo workflow CI) |
| Runtime Node trong CI | Node 18 (theo workflow của repo) |

Phiên bản gói snapshot của repository (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Điều kiện tiên quyết ✅

- Sử dụng trong trình duyệt: một trình duyệt hiện đại có `MediaDevices.getUserMedia`
- Phát triển cục bộ: Node.js + npm workspaces
- Phát triển docs: Python + Poetry (để build MkDocs)

Cấu hình nền tảng gợi ý theo CI:

- Node.js 18.x
- Python 3.10.x

## Cài đặt 📦

Cài gói cho trình duyệt:

```bash
npm i @ricky0123/vad-web
```

Cài wrapper React:

```bash
npm i @ricky0123/vad-react
```

Cài dependency monorepo (cho contributor):

```bash
npm install
```

## Sử dụng 🚀

### Bắt đầu nhanh (script tags)

Để dùng VAD qua script tag trong trình duyệt, thêm các script sau:

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

### Sử dụng gói trình duyệt (import module)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### Sử dụng React

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

### Sử dụng không thời gian thực (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Cấu hình ⚙️

Các tùy chọn dùng chung cho các API bao gồm:

- `positiveSpeechThreshold` (mặc định khoảng `0.3` ở API thời gian thực)
- `negativeSpeechThreshold` (mặc định khoảng `0.25` ở API thời gian thực)
- `redemptionMs` (mặc định khoảng `1400` ở API thời gian thực)
- `preSpeechPadMs` (mặc định khoảng `800` ở API thời gian thực)
- `minSpeechMs` (mặc định khoảng `400` ở API thời gian thực)

API thời gian thực (`MicVAD`, `useMicVAD`) còn hỗ trợ:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` hoặc `"v5"`)
- `baseAssetPath` và `onnxWASMBasePath`
- `workletOptions`

Xem đầy đủ bảng API trong tài liệu: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) và [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Cấu hình mẫu: tự host model và runtime assets

Khi không dùng mặc định CDN, đảm bảo ứng dụng của bạn phục vụ:

- `silero_vad_legacy.onnx` và/hoặc `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- tệp runtime `onnxruntime-web` (`.wasm`; và `.mjs` cho build runtime mới hơn)

Sau đó cấu hình:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Ví dụ 🧪

Ví dụ trong repo:

- `examples/script-tags`: thiết lập cơ bản bằng script tag
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: ví dụ tích hợp Next.js

Ví dụ lệnh từ `examples/bundler`:

```bash
npm run build && npm run start
```

Tài liệu về cách đóng gói bộ phát hiện hoạt động giọng nói cho trình duyệt hoặc sử dụng trong dự án Node/React có trong [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Ghi chú phát triển 🛠️

Scripts workspace gốc:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Ý nghĩa:

- `npm run build`: build toàn bộ workspaces
- `npm run test`: chạy test cho tất cả workspace
- `npm run test:coverage`: đo coverage cho `packages/web`
- `npm run typecheck`: kiểm tra TypeScript trong packages, test-site và tests
- `npm run format-check`: kiểm tra định dạng TS/TSX trong `packages`, `examples`, `test-site`
- `npm run dev`: theo dõi source của package và test-site, build lại, và phục vụ `test-site/dist`

Build docs (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Ghi chú thêm:

- `./test-site/build.sh` sao chép các asset VAD/ONNX Runtime cần thiết vào `test-site/dist` và `test-site/dist/subpath`
- `./scripts/dev.sh` dùng `nodemon` + `live-server` cho vòng lặp rebuild-and-serve tại cổng `8080`
- `./check_vad_up_to_date.sh` là bản lịch sử và tham chiếu `silero_vad.onnx` (trong khi repo này đang có `silero_vad_legacy.onnx` và `silero_vad_v5.onnx`)

## CI & Cổng chất lượng 🧱

Các workflow GitHub trong `.github/workflows/` bao gồm:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Format-check (`format-check.yml`)
- Build/deploy docs (`docs.yml`)
- Luồng publish (`publish.yml`)

Các workflow này là nguồn tham chiếu thực tế cho phiên bản runtime/tool mong đợi và các kiểm tra phát hành.

## Khắc phục sự cố 🩺

| Triệu chứng | Kiểm tra / Khắc phục |
| --- | --- |
| Quyền microphone bị từ chối | Đảm bảo trình duyệt đã được cấp quyền microphone cho domain của bạn. |
| Tài nguyên không tải được (`.onnx`, `.wasm`, `.mjs`, worklet) | Đặt đúng `baseAssetPath` / `onnxWASMBasePath` và xác nhận các file thực sự được phục vụ. |
| Sự cố với onnxruntime-web bản mới | Cần phục vụ thêm file `.mjs`, không chỉ `.wasm`. |
| Phát triển local trên nguồn không an toàn | API microphone của trình duyệt thường đòi bối cảnh an toàn (`https` hoặc `localhost`). |
| Lỗi bundler lúc build-time | Dùng hướng dẫn đóng gói trong [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Vấn đề tích hợp Next.js | Dùng mẫu cấu hình trong [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) và xác nhận đường dẫn hosting asset tĩnh. |

## Tài trợ ❤️

Hãy đóng góp tài chính cho dự án — đặc biệt nếu sản phẩm thương mại của bạn phụ thuộc vào gói này. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Important update about node support - Oct 2024 📢

Tôi sẽ dừng dần hỗ trợ cho `ricky0123/vad-node`, gói phát hiện hoạt động giọng nói cho môi trường node phía server. Tôi sẽ không tiếp tục phát hành cập nhật cho gói Node nữa. Tôi quyết định như vậy vì các lý do sau:

- Mục tiêu ban đầu của dự án là phát hiện hoạt động giọng nói phía client. Tôi thêm hỗ trợ Node vì có người dùng đề nghị và tôi muốn giúp đỡ. Tuy nhiên, hiện tôi không còn nhiều thời gian cho dự án này, và ngừng `ricky0123/vad-node` sẽ giúp tôi tập trung hơn cho `ricky0123/vad-web`.
- Với một lập trình viên, việc tự xây giải pháp VAD phía server thường dễ hơn nhiều so với việc học cách dùng onnxruntime-web, audio worklets và các công nghệ khác để tạo giải pháp client-side. Vì vậy, tôi cho rằng `ricky0123/vad-web` mang lại giá trị lớn hơn cho cộng đồng.
- Việc chia sẻ mã giữa gói trình duyệt và node khá khó khăn vì môi trường khác nhau ở những điểm quan trọng khi chạy và dùng mô hình phát hiện hoạt động giọng nói.
- Theo [khảo sát](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), đa số người dùng đang dùng `ricky0123/vad-web` (có thể kèm `ricky0123/vad-react`).

## Lộ trình 🛣️

Hướng đi hiện tại (dựa trên trạng thái repo và ghi chú maintainer ở trên):

- Tiếp tục tập trung vào các API ưu tiên trình duyệt (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Duy trì và cải thiện docs/examples cho bundlers và framework
- Cải thiện tài liệu cho contributor/dev và luồng làm việc test-site
- Bổ sung và duy trì README đã dịch trong `i18n/`

## Đóng góp 🤝

- Đọc hướng dẫn hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Mở issue hoặc PR trong repository: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Để nắm nhanh ngữ cảnh project, xem [`HACKING.md`](HACKING.md)

## Tài liệu tham khảo 📚

1. Repository Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Giấy phép 📄

- Giấy phép dự án: ISC (xem [LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
