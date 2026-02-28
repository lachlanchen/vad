[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript向け音声アクティビティ検出

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 数行のコードで、ユーザーの発話を含む音声区間でコールバックを実行できます。

このパッケージは、ブラウザ上で動作する正確で使いやすい音声アクティビティ検出（VAD）を提供することを目的としています。これを使うことで、マイク権限の取得、録音の開始、発話を含む音声区間をサーバーへ送信、またはユーザーが話しているときにアニメーションやインジケーターを表示できます。なお、ブラウザユースケースに集中するため、[Node サポートを中止](#node-support--oct-2024-)することにしました。

| 概要 | 詳細 |
| --- | --- |
| 主要パッケージ | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 主な実行環境 | ブラウザ (`WebAudio` + `getUserMedia`) |
| ドキュメント | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| ライブデモ | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## 目次

- [クイックリンク 🔗](#クイックリンク-)
- [概要 🧭](#概要-)
- [機能 ✨](#機能-)
- [プロジェクト構成 🗂️](#プロジェクト構成-)
- [互換性マトリクス 🧩](#互換性マトリクス-)
- [前提条件 ✅](#前提条件-)
- [インストール 📦](#インストール-)
- [使い方 🚀](#使い方-)
- [設定 ⚙️](#設定-)
- [サンプル 🧪](#サンプル-)
- [開発メモ 🛠️](#開発メモ-)
- [CI と品質ゲート 🧱](#ci-と品質ゲート-)
- [トラブルシューティング 🩺](#トラブルシューティング-)
- [スポンサーシップ ❤️](#スポンサーシップ-)
- [❤️ Support](#--support)
- [Node サポートに関する重要なお知らせ - 2024年10月 📢](#node-サポートに関する重要なお知らせ---2024年10月-)
- [ロードマップ 🛣️](#ロードマップ-)
- [コントリビューション 🤝](#コントリビューション-)
- [参照 📚](#参照-)
- [ライセンス 📄](#ライセンス-)

## クイックリンク 🔗

| リソース | リンク |
| --- | --- |
| ライブデモ | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| ドキュメント | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [コミュニティに参加](https://discord.gg/4WPeGEaSpF) |
| アンケート | [ユースケースを共有](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| コントリビューションガイド | [開発者ガイド](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- ドキュメントのソースは `./docs` にあります。
- 貢献を始める場所は [開発者ハッキングガイド](https://docs.vad.ricky0123.com/developer-guide/hacking/) です。ご質問は issue や Discord で受け付けています。

裏側では、これらのパッケージは [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#参照-) を [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) で実行しています（過去の Node サポート時代には ONNX Runtime Node.js 参照もありました）。この実現を支援してくれた皆さんに感謝します。

i18n の状況について: `i18n/` には、このファイル上部の言語リンクで示す翻訳版 README が含まれています。

## 概要 🧭

このリポジトリは、公開済みの主要パッケージを2つ含むモノレポです。

| パッケージ | 目的 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`、`AudioNodeVAD`、`NonRealTimeVAD` を含むブラウザ API |
| `@ricky0123/vad-react` | `vad-web` 向けの React フックラッパー (`useMicVAD`) |

本プロジェクトはブラウザファーストで、次の機能を含みます。

- リアルタイムのマイク区間分割コールバック（`onSpeechStart`、`onSpeechEnd`、`onVADMisfire` など）
- 調整可能なアルゴリズム閾値とタイミング制御
- レガシーおよび v5 Silero モデルのサポート
- デモ・テストアプリとドキュメントサイトのソース

## 機能 ✨

- Silero ONNX モデルによるブラウザファーストの VAD パイプライン
- script タグ、バンドラー、React で利用可能
- 実用的なデフォルトのマイクストリーム制約
- ストリームのライフサイクルを上書き可能（`getStream`、`pauseStream`、`resumeStream`）
- `NonRealTimeVAD` による事前録音音声の非リアルタイム区間分割
- `baseAssetPath` と `onnxWASMBasePath` によるモデル/アセットの読み込み設定
- 組み込みラッパーでレガシーと v5 のモデル状態処理をサポート
- script タグ、webpack ベースのバンドラー、React バンドラー、Next.js の例を含む

## プロジェクト構成 🗂️

```text
.
├── README.md
├── docs/                     # docs.vad.ricky0123.com の MkDocs ソース
├── examples/                 # script-tag, bundler, react-bundler, nextjs の例
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # 開発ヘルパー
├── test-site/                # ローカルのインタラクティブプレイグラウンド
├── i18n/                     # 翻訳済み README
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

より詳細な主なパス:

- `packages/web/src/real-time-vad.ts`: リアルタイムのマイク / オーディオノード VAD オーケストレーション
- `packages/web/src/non-real-time-vad.ts`: 事前録音音声の非同期区間分割
- `packages/web/src/frame-processor.ts`: 閾値処理と発話区間境界ロジック
- `packages/react/src/index.ts`: `useMicVAD` の React フックライフサイクルと状態ラッパー

## 互換性マトリクス 🧩

| コンポーネント | 実行環境 |
| --- | --- |
| `@ricky0123/vad-web` | WebAudio + `MediaDevices.getUserMedia` を備えたモダンブラウザ |
| `@ricky0123/vad-react` | React アプリ (`react` / `react-dom` >= 16.8.0) |
| Docs toolchain | Python 3.10 + Poetry（CI ワークフロー準拠） |
| CI Node runtime | Node 18（リポジトリワークフロー準拠） |

リポジトリスナップショット時点のパッケージバージョン（`packages/*/package.json`）:

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## 前提条件 ✅

- ブラウザ利用: `MediaDevices.getUserMedia` を利用できるモダンブラウザ
- ローカル開発: Node.js + npm ワークスペース
- ドキュメント開発: Python + Poetry（MkDocs ビルド用）

CI 設定に基づく推奨ローカルベースライン:

- Node.js 18.x
- Python 3.10.x

## インストール 📦

ブラウザ向けパッケージをインストール:

```bash
npm i @ricky0123/vad-web
```

React ラッパーをインストール:

```bash
npm i @ricky0123/vad-react
```

モノレポ依存関係をインストール（コントリビューター向け）:

```bash
npm install
```

## 使い方 🚀

### クイックスタート（script タグ）

ブラウザで VAD を script タグとして使うには、次のタグを読み込みます。

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

### ブラウザパッケージ利用（モジュールインポート）

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React 利用

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

### 非リアルタイム利用（バッチ音声）

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## 設定 ⚙️

各 API 共通の主な設定項目:

- `positiveSpeechThreshold`（リアルタイム API の既定値は約 `0.3`）
- `negativeSpeechThreshold`（リアルタイム API の既定値は約 `0.25`）
- `redemptionMs`（リアルタイム API の既定値は約 `1400`）
- `preSpeechPadMs`（リアルタイム API の既定値は約 `800`）
- `minSpeechMs`（リアルタイム API の既定値は約 `400`）

リアルタイム API（`MicVAD`、`useMicVAD`）では次もサポートします:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` または `"v5"`）
- `baseAssetPath` と `onnxWASMBasePath`
- `workletOptions`

完全な API 表はドキュメントを参照: [API リファレンス](https://docs.vad.ricky0123.com/user-guide/api/) と [アルゴリズムガイド](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### 設定レシピ: モデルとランタイムアセットをセルフホストする

CDN のデフォルトを使わない場合、アプリで次を配信していることを確認してください。

- `silero_vad_legacy.onnx` および/または `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` のランタイムファイル（`.wasm`、新しいランタイムビルド向けの `.mjs`）

そのうえで設定します。

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## サンプル 🧪

リポジトリ内の例:

- `examples/script-tags`: 基本的な script タグ構成
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js 統合例

`examples/bundler` のコマンド例:

```bash
npm run build && npm run start
```

ブラウザ向けの voice activity detector のバンドル方法、または node / React プロジェクトでの利用方法は [vad.ricky0123.com](https://www.vad.ricky0123.com) のドキュメントにあります。

## 開発メモ 🛠️

ルートワークスペースのスクリプト:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

各コマンドの説明:

- `npm run build`: すべてのワークスペースをビルド
- `npm run test`: ワークスペーステストを実行
- `npm run test:coverage`: `packages/web` のカバレッジを実施
- `npm run typecheck`: packages、test-site、tests の TypeScript を検査
- `npm run format-check`: `packages`、`examples`、`test-site` 配下の TS/TSX のフォーマットを検査
- `npm run dev`: パッケージと test-site のソースを監視し、再ビルドして `test-site/dist` を提供

Docs ビルド（MkDocs + Poetry）:

```bash
poetry install
poetry run mkdocs serve
```

補足:

- `./test-site/build.sh` は必要な VAD / ONNX Runtime アセットを `test-site/dist` と `test-site/dist/subpath` にコピーします
- `./scripts/dev.sh` は `nodemon` + `live-server` を使用し、ローカルで再ビルドと配信のループをポート `8080` 上で行います
- `./check_vad_up_to_date.sh` は過去のスクリプトで、`silero_vad.onnx` を参照しています（このリポジトリでは `silero_vad_legacy.onnx` と `silero_vad_v5.onnx` が配備）

## CI と品質ゲート 🧱

`.github/workflows/` の GitHub ワークフロー:

- テスト (`test.yml`)
- 型チェック (`typecheck.yml`)
- フォーマットチェック (`format-check.yml`)
- ドキュメントのビルド/デプロイ (`docs.yml`)
- 公開フロー (`publish.yml`)

これらのワークフローは、期待されるランタイム / ツールのバージョンやリリースチェックを示す実務上の基準です。

## トラブルシューティング 🩺

| 症状 | 確認 / 修正 |
| --- | --- |
| マイク権限が拒否された | ブラウザで元のオリジンに対してマイク権限が許可されているか確認 |
| アセットの読み込み失敗（`.onnx`, `.wasm`, `.mjs`, worklet） | `baseAssetPath` / `onnxWASMBasePath` を正しく設定し、ファイルが実際に配信されていることを確認 |
| `onnxruntime-web` の新しいランタイムで問題が発生 | `.wasm` だけでなく `.mjs` も配信 |
| ローカル開発が安全でないオリジン上 | ブラウザのマイク API は一般に安全なコンテキスト（`https` または `localhost`）を要求 |
| ビルド時のバンドラー問題 | [ブラウザ用ドキュメント](https://docs.vad.ricky0123.com/user-guide/browser/) のバンドルガイドを参照 |
| Next.js 統合の問題 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) にある設定パターンを使い、静的アセットの配信パスを確認 |

## スポンサーシップ ❤️

このプロジェクトの継続的な開発を支援してください。特に商用製品がこのパッケージに依存している場合は、支援をお願いします。 [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Node サポートに関する重要なお知らせ - 2024年10月 📢

`ricky0123/vad-node`（サーバーサイド node 環境向け音声活動検出パッケージ）のサポートを段階的に終了します。今後、この node パッケージのアップデートを公開する予定はありません。以下の理由でこの判断をしました。

- このプロジェクトの元のユースケースはクライアントサイドの音声活動検出でした。誰かの要望で node サポートを追加しましたが、私にはこのプロジェクトに費やせる時間が限られており、`ricky0123/vad-node` を縮小することで `ricky0123/vad-web` に集中できるようになります。
- 開発者個々人にとって、サーバーサイドで独自の音声活動検出ソリューションを作ることのほうが、onnxruntime-web、Audio Worklet などを習得してクライアントサイド実装を作るより容易です。したがって、コミュニティにとって `ricky0123/vad-web` のほうが価値が高いです。
- ブラウザ用と node 用パッケージ間でコードを共有するのは、音声活動検出モデルの実行と利用で環境差分が大きく、扱いにくいためです。
- [アンケート](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) の結果、ほとんどのユーザーが `ricky0123/vad-web`（場合によっては `ricky0123/vad-react`）を利用していることが分かっています。

## ロードマップ 🛣️

現在の方針（リポジトリ状態とメンテナー注記に基づく）:

- ブラウザファースト API（`@ricky0123/vad-web`, `@ricky0123/vad-react`）に引き続き注力
- バンドラーや各種フレームワーク向けドキュメント・サンプルの改善継続
- コントリビューター向け／開発者向けドキュメントと test-site ワークフローの改善
- `i18n/` 配下の翻訳 README の追加と保守

## コントリビューション 🤝

- 開発ガイド: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- このリポジトリで issue / PR を作成: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- 参考のため、[HACKING.md](HACKING.md) を参照

## 参照 📚

1. Silero VAD リポジトリ: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ライセンス 📄

- プロジェクトライセンス: ISC（[LICENSE](LICENSE) を参照）
