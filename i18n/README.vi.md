[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Phát hiện hoạt động giọng nói cho Javascript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Chạy callback trên các đoạn âm thanh có giọng nói của người dùng chỉ với vài dòng mã.

Gói này nhằm cung cấp một bộ phát hiện hoạt động giọng nói (VAD) chính xác, thân thiện với người dùng và chạy trong trình duyệt. Khi dùng gói này, bạn có thể yêu cầu quyền truy cập micro từ người dùng, bắt đầu ghi âm, gửi các đoạn âm thanh có giọng nói lên máy chủ để xử lý, hoặc hiển thị một hiệu ứng/chỉ báo khi người dùng đang nói. Lưu ý rằng tôi đã quyết định [ngừng hỗ trợ node](#cập-nhật-quan-trọng-về-hỗ-trợ-node---tháng-10-2024-) để tập trung vào trường hợp sử dụng trên trình duyệt.

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
- [CI và cổng chất lượng 🧱](#ci-và-cổng-chất-lượng-)
- [Khắc phục sự cố 🩺](#khắc-phục-sự-cố-)
- [Tài trợ ❤️](#tài-trợ-️)
- [Cập nhật quan trọng về hỗ trợ node - Tháng 10 2024 📢](#cập-nhật-quan-trọng-về-hỗ-trợ-node---tháng-10-2024-)
- [Lộ trình 🛣️](#lộ-trình-️)
- [Đóng góp 🤝](#đóng-góp-)
- [Tham khảo 📚](#tham-khảo-)
- [Giấy phép 📄](#giấy-phép-)

## Liên kết nhanh 🔗

| Tài nguyên | Liên kết |
| --- | --- |
| Demo trực tiếp | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Tài liệu | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Tham gia cộng đồng](https://discord.gg/4WPeGEaSpF) |
| Khảo sát | [Chia sẻ trường hợp sử dụng](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Hướng dẫn đóng góp | [Hướng dẫn hack cho lập trình viên](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Duyệt tài liệu, phần mã nguồn nằm trong thư mục `./docs`.
- Nếu bạn muốn đóng góp, tôi đã bắt đầu viết tài liệu về cách bắt đầu phát triển các gói này [tại đây](https://docs.vad.ricky0123.com/developer-guide/hacking/). Nếu có câu hỏi, bạn có thể mở issue tại đây hoặc để lại tin nhắn trên Discord.

Bên dưới, các gói này chạy [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#tham-khảo-) bằng [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node). Cảm ơn rất nhiều tới những người đã giúp điều này trở thành hiện thực.

Lưu ý về trạng thái i18n: `i18n/` đã tồn tại và bao gồm nhiều tệp README đã dịch. Bộ chọn ngôn ngữ phía trên cũng có liên kết cho các bản dịch dự kiến/bản giữ chỗ (`README.de.md`, `README.ru.md`) có thể chưa có trong ảnh chụp repository này.

## Tổng quan 🧭

Repository này là một monorepo với hai gói phát hành chính:

| Gói | Mục đích |
| --- | --- |
| `@ricky0123/vad-web` | API trình duyệt gồm `MicVAD`, `AudioNodeVAD`, và `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper hook React (`useMicVAD`) cho `vad-web` |

Dự án ưu tiên trình duyệt và bao gồm:

- Callback phân đoạn micro theo thời gian thực (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, v.v.)
- Ngưỡng thuật toán và điều khiển thời gian có thể cấu hình
- Hỗ trợ cả mô hình Silero legacy và v5
- Ứng dụng demo/test và mã nguồn trang tài liệu ngay trong repository này

## Tính năng ✨

- Pipeline VAD ưu tiên trình duyệt, chạy trên mô hình ONNX của Silero
- Hoạt động với script tag, bundler và React
- Thiết lập ràng buộc luồng micro mặc định hợp lý
- Có thể ghi đè vòng đời luồng (`getStream`, `pauseStream`, `resumeStream`)
- Phân đoạn giọng nói không thời gian thực cho âm thanh ghi sẵn qua `NonRealTimeVAD`
- Có thể cấu hình tải mô hình/tài nguyên qua `baseAssetPath` và `onnxWASMBasePath`
- Hỗ trợ cả cơ chế trạng thái mô hình legacy và v5 thông qua wrapper tích hợp sẵn
- Bao gồm ví dụ cho script tag, bundler dùng webpack, bundler React và Next.js

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

Đường dẫn chi tiết hơn:

- `packages/web/src/real-time-vad.ts`: điều phối VAD micro/audio-node theo thời gian thực
- `packages/web/src/non-real-time-vad.ts`: phân đoạn bất đồng bộ cho âm thanh ghi sẵn
- `packages/web/src/frame-processor.ts`: logic ngưỡng và ranh giới đoạn giọng nói
- `packages/react/src/index.ts`: vòng đời và wrapper trạng thái cho hook React `useMicVAD`

## Ma trận tương thích 🧩

| Thành phần | Môi trường |
| --- | --- |
| `@ricky0123/vad-web` | Trình duyệt hiện đại có WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Ứng dụng React (`react` / `react-dom` >= 16.8.0) |
| Bộ công cụ docs | Python 3.10 + Poetry (theo workflow CI) |
| Runtime Node cho CI | Node 18 (theo workflow của repository) |

Ghi chú giả định: ví dụ và tài liệu khớp với các phiên bản gói hiện tại trong ảnh chụp repository này (`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`).

## Điều kiện tiên quyết ✅

- Dùng trên trình duyệt: trình duyệt hiện đại có `MediaDevices.getUserMedia`
- Phát triển cục bộ: Node.js + npm workspaces
- Phát triển tài liệu: Python + Poetry (để build MkDocs)

Mốc cơ sở cục bộ được khuyến nghị theo cấu hình CI:

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

Cài dependencies monorepo (dành cho contributor):

```bash
npm install
```

## Cách dùng 🚀

### Bắt đầu nhanh (script tags)

Để dùng VAD qua script tag trong trình duyệt, hãy thêm các script tag sau:

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

### Dùng với React

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

### Dùng không thời gian thực (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Cấu hình ⚙️

Các tùy chọn chung giữa các API bao gồm:

- `positiveSpeechThreshold` (mặc định khoảng `0.3` trong API thời gian thực)
- `negativeSpeechThreshold` (mặc định khoảng `0.25` trong API thời gian thực)
- `redemptionMs` (mặc định khoảng `1400` trong API thời gian thực)
- `preSpeechPadMs` (mặc định khoảng `800` trong API thời gian thực)
- `minSpeechMs` (mặc định khoảng `400` trong API thời gian thực)

API thời gian thực (`MicVAD`, `useMicVAD`) cũng hỗ trợ:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` hoặc `"v5"`)
- `baseAssetPath` và `onnxWASMBasePath`
- `workletOptions`

Xem bảng API đầy đủ trong docs: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) và [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Công thức cấu hình: tự host mô hình và tài nguyên runtime

Khi không dùng mặc định CDN, hãy đảm bảo ứng dụng của bạn phục vụ:

- `silero_vad_legacy.onnx` và/hoặc `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Tệp runtime `onnxruntime-web` (`.wasm`; và `.mjs` cho các bản runtime mới hơn)

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

- `examples/script-tags`: thiết lập script-tag cơ bản
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: ví dụ tích hợp Next.js

Lệnh ví dụ từ `examples/bundler`:

```bash
npm run build && npm run start
```

Tài liệu về cách bundle voice activity detector cho trình duyệt hoặc dùng trong dự án node hay React có tại [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Ghi chú phát triển 🛠️

Script workspace ở thư mục gốc:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Chức năng:

- `npm run build`: build tất cả workspace
- `npm run test`: chạy test cho các workspace
- `npm run test:coverage`: coverage cho `packages/web`
- `npm run typecheck`: kiểm tra TypeScript trong packages, test-site và tests
- `npm run format-check`: kiểm tra định dạng TS/TSX dưới `packages`, `examples`, `test-site`
- `npm run dev`: theo dõi source package và test-site, rebuild và phục vụ `test-site/dist`

Build docs (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Ghi chú bổ sung:

- `./test-site/build.sh` sao chép các tài nguyên VAD/ONNX Runtime cần thiết vào `test-site/dist` và `test-site/dist/subpath`
- `./scripts/dev.sh` dùng `nodemon` + `live-server` cho vòng lặp rebuild và serve cục bộ trên cổng `8080`
- `./check_vad_up_to_date.sh` là script cũ và tham chiếu `silero_vad.onnx` (trong khi repo này cung cấp `silero_vad_legacy.onnx` và `silero_vad_v5.onnx`)

## CI và cổng chất lượng 🧱

Các workflow GitHub trong `.github/workflows/` bao gồm:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Build/deploy docs (`docs.yml`)
- Luồng publish (`publish.yml`)

Các workflow này là nguồn thực tế đáng tin cậy về phiên bản runtime/tool được kỳ vọng và các bước kiểm tra trước phát hành.

## Khắc phục sự cố 🩺

| Triệu chứng | Kiểm tra / Cách khắc phục |
| --- | --- |
| Quyền micro bị từ chối | Đảm bảo trình duyệt đã cấp quyền microphone cho origin của bạn. |
| Không tải được tài nguyên (`.onnx`, `.wasm`, `.mjs`, worklet) | Đặt đúng `baseAssetPath` / `onnxWASMBasePath` và xác minh tệp thực sự đang được phục vụ. |
| Lỗi với runtime `onnxruntime-web` mới hơn | Hãy phục vụ thêm tệp `.mjs`, không chỉ `.wasm`. |
| Phát triển cục bộ trên origin không bảo mật | API mic trên trình duyệt thường yêu cầu secure context (`https` hoặc `localhost`). |
| Lỗi bundler khi build | Dùng hướng dẫn bundling trong [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Lỗi tích hợp Next.js | Dùng mẫu cấu hình trong [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) và xác minh đường dẫn host tài nguyên tĩnh. |

## Tài trợ ❤️

Vui lòng đóng góp tài chính cho dự án, đặc biệt nếu sản phẩm thương mại của bạn phụ thuộc vào gói này. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Cập nhật quan trọng về hỗ trợ node - Tháng 10 2024 📢

Tôi sẽ dần ngừng hỗ trợ `ricky0123/vad-node`, gói phát hiện hoạt động giọng nói cho môi trường node phía server. Tôi không có kế hoạch phát hành thêm bản cập nhật nào cho gói node kể từ bây giờ. Tôi đưa ra quyết định này vì các lý do sau:

- Trường hợp sử dụng ban đầu của tôi cho dự án này là phát hiện hoạt động giọng nói phía client. Tôi đã thêm hỗ trợ node vì có người yêu cầu và tôi muốn giúp. Tuy nhiên, tôi không có nhiều thời gian để làm dự án này, và việc ngừng `ricky0123/vad-node` sẽ giúp tôi có thêm thời gian tập trung vào `ricky0123/vad-web`.
- Các nhà phát triển cá nhân tự xây dựng giải pháp phát hiện hoạt động giọng nói phía server thường dễ hơn nhiều so với việc học cách làm việc với onnxruntime-web, audio worklet và các công nghệ khác để tạo giải pháp phía client. Vì vậy, tôi cho rằng `ricky0123/vad-web` mang lại nhiều giá trị hơn cho cộng đồng.
- Việc chia sẻ mã giữa gói trình duyệt và gói node khá bất tiện vì hai môi trường khác nhau ở những điểm liên quan trực tiếp đến việc chạy và sử dụng mô hình phát hiện hoạt động giọng nói.
- Theo [khảo sát](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), phần lớn người dùng đang dùng `ricky0123/vad-web` (có thể kèm `ricky0123/vad-react`).

## Lộ trình 🛣️

Hướng đi hiện tại (dựa trên trạng thái repository và ghi chú của maintainer ở trên):

- Tiếp tục tập trung vào API ưu tiên trình duyệt (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Duy trì và cải thiện docs/ví dụ cho bundler và framework
- Cải thiện tài liệu cho contributor/developer và workflow của test-site
- Bổ sung và duy trì các README đã dịch trong `i18n/`

## Đóng góp 🤝

- Đọc hướng dẫn hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Mở issue hoặc PR trong repository này: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Để nắm bối cảnh dự án nhanh, xem [`HACKING.md`](HACKING.md)

## Tham khảo 📚

1. Repository Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Giấy phép 📄

- Giấy phép dự án: ISC (xem [LICENSE](LICENSE))
