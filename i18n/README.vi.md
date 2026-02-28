[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Voice Activity Detection cho JavaScript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Chạy callback trên các đoạn âm thanh có giọng nói của người dùng chỉ trong vài dòng mã.

Gói này nhằm mục tiêu cung cấp một bộ phát hiện hoạt động giọng nói (VAD) chính xác và thân thiện với người dùng chạy trực tiếp trong trình duyệt. Khi dùng gói này, bạn có thể yêu cầu quyền truy cập micro của người dùng, bắt đầu ghi âm, gửi các đoạn âm thanh có giọng nói lên máy chủ để xử lý, hoặc hiển thị hoạt ảnh/chỉ báo khi người dùng đang nói. Lưu ý tôi đã quyết định [ngừng hỗ trợ node](#cập-nhật-quan-trọng-về-hỗ-trợ-node---tháng-10-2024-) để tập trung hoàn toàn vào trường hợp sử dụng trong trình duyệt.

| Tóm tắt nhanh | Chi tiết |
| --- | --- |
| Gói lõi | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Môi trường chạy chính | Trình duyệt (`WebAudio` + `getUserMedia`) |
| Tài liệu | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Demo trực tiếp | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Mục lục

- [Liên kết nhanh 🔗](#liên-kết-nhanh-)
- [Tổng quan 🧭](#tổng-quan-)
- [Tính năng ✨](#tính-năng-)
- [Cấu trúc dự án 🗂️](#cấu-trúc-dự-án-️)
- [Ma trận tương thích 🧩](#ma-trận-tương-thích-)
- [Điều kiện tiên quyết ✅](#điều-kiện-tiên-quyết-)
- [Cài đặt 📦](#cài-đặt-)
- [Cách dùng 🚀](#cách-dùng-)
- [Cấu hình ⚙️](#cấu-hình-️)
- [Ví dụ 🧪](#ví-dụ-)
- [Ghi chú phát triển 🛠️](#ghi-chú-phát-triển-️)
- [CI & cổng chất lượng 🧱](#ci--cổng-chất-lượng-)
- [Khắc phục sự cố 🩺](#khắc-phục-sự-cố-)
- [Tài trợ ❤️](#tài-trợ-️)
- [❤️ Support](#-support)
- [Cập nhật quan trọng về hỗ trợ node - Tháng 10 2024 📢](#cập-nhật-quan-trọng-về-hỗ-trợ-node---tháng-10-2024-)
- [Lộ trình 🛣️](#lộ-trình-️)
- [Đóng góp 🤝](#đóng-góp-)
- [Tài liệu tham khảo 📚](#tài-liệu-tham-khảo-)
- [Giấy phép 📄](#giấy-phép-)

## Liên kết nhanh 🔗

| Tài nguyên | Liên kết |
| --- | --- |
| Demo trực tiếp | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Tài liệu | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Gia nhập cộng đồng](https://discord.gg/4WPeGEaSpF) |
| Khảo sát | [Chia sẻ use-case của bạn](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Hướng dẫn đóng góp | [Tài liệu phát triển](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Mã nguồn tài liệu nằm trong `./docs`.
- Hướng dẫn onboarding cho contributor bắt đầu tại đây: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Vấn đề thắc mắc có thể gửi qua issue hoặc Discord.

Phía dưới, các gói này chạy [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#tài-liệu-tham-khảo-) bằng [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (kèm theo tham chiếu lịch sử đến ONNX Runtime Node.js từ giai đoạn hỗ trợ Node trước đây). Xin cảm ơn các tác giả đã giúp điều này khả thi.

Ghi chú về i18n: Thư mục `i18n/` chứa các bản README đã dịch cho các tùy chọn ngôn ngữ ở trên đầu file.

## Tổng quan 🧭

Repository này là monorepo gồm hai gói phát hành chính:

| Gói | Mục đích |
| --- | --- |
| `@ricky0123/vad-web` | Các API trình duyệt gồm `MicVAD`, `AudioNodeVAD` và `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper React hook (`useMicVAD`) cho `vad-web` |

Dự án được thiết kế theo hướng trình duyệt trước và bao gồm:

- Callbacks phân đoạn micro theo thời gian thực (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, ...)
- Ngưỡng thuật toán và điều khiển thời gian có thể cấu hình
- Hỗ trợ mô hình Silero legacy và v5
- Ứng dụng demo/test và mã nguồn docs nằm trong repo này

## Tính năng ✨

- Pipeline VAD ưu tiên trình duyệt, chạy bằng mô hình ONNX của Silero
- Hoạt động với script tags, bundler, và React
- Ràng buộc luồng micro mặc định hợp lý
- Có thể ghi đè vòng đời stream (`getStream`, `pauseStream`, `resumeStream`)
- Phân đoạn giọng nói không thời gian thực cho audio đã ghi sẵn thông qua `NonRealTimeVAD`
- Tải mô hình/tài nguyên có thể cấu hình qua `baseAssetPath` và `onnxWASMBasePath`
- Hỗ trợ cả quản lý trạng thái mô hình legacy và v5 qua các wrapper tích hợp sẵn
- Bao gồm ví dụ cho script tags, webpack-based bundlers, React bundlers và Next.js

## Cấu trúc dự án 🗂️

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

Đường dẫn chi tiết:

- `packages/web/src/real-time-vad.ts`: điều phối VAD theo thời gian thực cho micro/audio-node
- `packages/web/src/non-real-time-vad.ts`: phân đoạn không đồng bộ cho audio đã ghi sẵn
- `packages/web/src/frame-processor.ts`: logic ngưỡng và ranh giới đoạn giọng nói
- `packages/react/src/index.ts`: vòng đời `useMicVAD` và lớp bao trạng thái của React

## Ma trận tương thích 🧩

| Thành phần | Môi trường |
| --- | --- |
| `@ricky0123/vad-web` | Trình duyệt hiện đại với WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Ứng dụng React (`react` / `react-dom` >= 16.8.0) |
| Toolchain docs | Python 3.10 + Poetry (theo CI workflow) |
| Runtime Node cho CI | Node 18 (theo workflows repository) |

Phiên bản package tại thời điểm snapshot (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Điều kiện tiên quyết ✅

- Sử dụng trình duyệt: trình duyệt hiện đại có `MediaDevices.getUserMedia`
- Phát triển local: Node.js + npm workspaces
- Phát triển docs: Python + Poetry (để build MkDocs)

Mốc cơ sở cục bộ khuyến nghị theo cấu hình CI:

- Node.js 18.x
- Python 3.10.x

## Cài đặt 📦

Cài đặt gói trình duyệt:

```bash
npm i @ricky0123/vad-web
```

Cài đặt wrapper React:

```bash
npm i @ricky0123/vad-react
```

Cài đặt phụ thuộc monorepo (dành cho contributor):

```bash
npm install
```

## Cách dùng 🚀

### Khởi động nhanh (script tags)

Để dùng VAD qua script tag trong trình duyệt, thêm các thẻ sau:

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

### Dùng gói trình duyệt (import module)

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

### Sử dụng non-real-time (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Cấu hình ⚙️

Các tùy chọn chung giữa các API gồm:

- `positiveSpeechThreshold` (mặc định khoảng `0.3` trong các API thời gian thực)
- `negativeSpeechThreshold` (mặc định khoảng `0.25` trong các API thời gian thực)
- `redemptionMs` (mặc định khoảng `1400` trong các API thời gian thực)
- `preSpeechPadMs` (mặc định khoảng `800` trong các API thời gian thực)
- `minSpeechMs` (mặc định khoảng `400` trong các API thời gian thực)

API thời gian thực (`MicVAD`, `useMicVAD`) cũng hỗ trợ:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` hoặc `"v5"`)
- `baseAssetPath` và `onnxWASMBasePath`
- `workletOptions`

Xem đầy đủ bảng API trong docs: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) và [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Công thức cấu hình: self-host model và runtime assets

Khi không dùng mặc định CDN, đảm bảo ứng dụng của bạn phục vụ:

- `silero_vad_legacy.onnx` và/hoặc `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Các runtime của `onnxruntime-web` (`.wasm`; và `.mjs` cho bản build runtime mới)

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

Ví dụ trong repository:

- `examples/script-tags`: cài đặt cơ bản với script tags
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: ví dụ tích hợp Next.js

Lệnh ví dụ từ `examples/bundler`:

```bash
npm run build && npm run start
```

Tài liệu hướng dẫn bundle bộ phát hiện hoạt động giọng nói cho trình duyệt hoặc sử dụng trong dự án Node hay React có tại [vad.ricky0123.com](https://www.vad.ricky0123.com).

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

Chức năng:

- `npm run build`: build toàn bộ workspaces
- `npm run test`: chạy test cho tất cả workspace
- `npm run test:coverage`: đo coverage cho `packages/web`
- `npm run typecheck`: kiểm tra TypeScript trong packages, test-site và tests
- `npm run format-check`: kiểm tra định dạng TS/TSX trong `packages`, `examples`, `test-site`
- `npm run dev`: theo dõi code của package và test-site, rebuild, và phục vụ `test-site/dist`

Build docs (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Ghi chú bổ sung:

- `./test-site/build.sh` sao chép các asset VAD/ONNX Runtime bắt buộc vào `test-site/dist` và `test-site/dist/subpath`
- `./scripts/dev.sh` dùng `nodemon` + `live-server` cho vòng lặp rebuild-and-serve cục bộ trên cổng `8080`
- `./check_vad_up_to_date.sh` là script lịch sử và tham chiếu tới `silero_vad.onnx` (trong khi repo hiện tại dùng `silero_vad_legacy.onnx` và `silero_vad_v5.onnx`)

## CI và cổng chất lượng 🧱

GitHub workflows trong `.github/workflows/` bao gồm:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Docs build/deploy (`docs.yml`)
- Publish flow (`publish.yml`)

Những workflow này là nguồn tham chiếu thực tế cho runtime/tool versions kỳ vọng và các kiểm tra phát hành.

## Khắc phục sự cố 🩺

| Triệu chứng | Kiểm tra / Cách xử lý |
| --- | --- |
| Quyền truy cập mic bị từ chối | Đảm bảo trình duyệt có quyền micro cho origin của bạn. |
| Tải asset lỗi (`.onnx`, `.wasm`, `.mjs`, worklet) | Cấu hình đúng `baseAssetPath` / `onnxWASMBasePath` và xác nhận file thực sự được phục vụ. |
| Lỗi với runtime `onnxruntime-web` mới hơn | Hãy phục vụ cả file `.mjs`, không chỉ `.wasm`. |
| Dev local trên origin không an toàn | API mic trình duyệt thường yêu cầu secure context (`https` hoặc `localhost`). |
| Vấn đề khi build bundler | Dùng hướng dẫn bundling trong [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Vấn đề tích hợp Next.js | Dùng mẫu cấu hình trong [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) và xác nhận đường dẫn host tài nguyên tĩnh. |

## Tài trợ ❤️

Vui lòng đóng góp tài chính cho dự án, đặc biệt nếu sản phẩm thương mại của bạn dựa vào gói này. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Cập nhật quan trọng về hỗ trợ node - Tháng 10 2024 📢

Tôi sẽ dần ngừng hỗ trợ `ricky0123/vad-node`, gói phát hiện hoạt động giọng nói cho môi trường node phía server. Từ giờ tôi không dự định phát hành thêm bản cập nhật cho package node. Quyết định này đến từ các lý do sau:

- Use case gốc của dự án là phát hiện hoạt động giọng nói phía client. Tôi thêm hỗ trợ node vì có người dùng yêu cầu và tôi muốn hỗ trợ cộng đồng. Tuy nhiên thời gian của mình có hạn, nên giảm dần hỗ trợ `ricky0123/vad-node` giúp tôi tập trung nhiều hơn cho `ricky0123/vad-web`.
- Việc mỗi nhà phát triển tự xây giải pháp VAD phía server thường dễ hơn nhiều so với tự học onnxruntime-web, audio worklets và các công nghệ liên quan để tạo giải pháp client-side. Vì vậy, tôi coi `ricky0123/vad-web` mang lại giá trị cao hơn cho cộng đồng.
- Chia sẻ mã giữa package trình duyệt và node khá khó vì môi trường khác nhau ở những điểm ảnh hưởng trực tiếp đến việc chạy và dùng model VAD.
- Theo [khảo sát](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), phần lớn người dùng đang dùng `ricky0123/vad-web` (có thể đi kèm `ricky0123/vad-react`).

## Lộ trình 🛣️

Hướng đi hiện tại (dựa trên trạng thái repo và ghi chú của maintainer ở trên):

- Tiếp tục tập trung vào API ưu tiên trình duyệt (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Duy trì và cải tiến docs/examples cho bundlers và các framework
- Cải thiện tài liệu cho contributor/developer và quy trình làm việc với test-site
- Bổ sung và duy trì các README đã dịch trong `i18n/`

## Đóng góp 🤝

- Đọc hướng dẫn hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Mở issue hoặc PR trong repository này: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Để nắm nhanh bối cảnh dự án, xem [`HACKING.md`](HACKING.md)

## Tài liệu tham khảo 📚

1. Repository Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Giấy phép 📄

- Giấy phép dự án: ISC (xem [LICENSE](LICENSE))
