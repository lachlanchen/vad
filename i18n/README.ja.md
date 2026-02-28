[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Voice Activity Detection for Javascript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> 数行のコードで、ユーザーの発話を含む音声区間に対してコールバックを実行できます。

このパッケージは、ブラウザ上で動作する高精度かつ使いやすい音声活動検出（VAD）を提供することを目的としています。これを使うことで、マイク権限の取得、録音開始、発話を含む音声区間のサーバー送信、またはユーザー発話時のアニメーションやインジケーター表示を行えます。なお、ブラウザ向けユースケースに注力するため、[Nodeサポートは終了](#nodeサポートに関する重要なお知らせ---2024年10月-)することにしました。

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
- [CIと品質ゲート 🧱](#ciと品質ゲート-)
- [トラブルシューティング 🩺](#トラブルシューティング-)
- [スポンサーシップ ❤️](#スポンサーシップ-)
- [Nodeサポートに関する重要なお知らせ - 2024年10月 📢](#nodeサポートに関する重要なお知らせ---2024年10月-)
- [ロードマップ 🛣️](#ロードマップ-)
- [コントリビューション 🤝](#コントリビューション-)
- [参考資料 📚](#参考資料-)
- [ライセンス 📄](#ライセンス-)

## クイックリンク 🔗

| リソース | リンク |
| --- | --- |
| ライブデモ | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| ドキュメント | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [コミュニティに参加](https://discord.gg/4WPeGEaSpF) |
| Survey | [ユースケースを共有](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| コントリビューションガイド | [開発者向けハッキングガイド](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- ドキュメントを参照できます。ソースコードは `./docs` ディレクトリにあります。
- 貢献したい場合は、これらのパッケージの開発を始めるためのドキュメントを[こちら](https://docs.vad.ricky0123.com/developer-guide/hacking/)に書き始めています。質問があれば、このリポジトリで issue を作成するか Discord でメッセージを送ってください。

内部では、これらのパッケージは [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#参考資料-) を [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node) とともに利用しています。実現を可能にしてくれた皆さんに感謝します。

i18n の状況に関する注記: `i18n/` は存在し、複数の翻訳版 README を含んでいます。上部の言語セレクターには、将来追加予定またはプレースホルダーの翻訳（`README.de.md`, `README.ru.md`）へのリンクも含まれており、これらはこのリポジトリのスナップショットには存在しない場合があります。

## 概要 🧭

このリポジトリは、公開済みの主要パッケージを2つ含むモノレポです。

| パッケージ | 目的 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`、`AudioNodeVAD`、`NonRealTimeVAD` を含むブラウザAPI |
| `@ricky0123/vad-react` | `vad-web` 用の React フックラッパー（`useMicVAD`） |

このプロジェクトは browser-first で、以下を含みます。

- リアルタイムのマイク区間分割コールバック（`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` など）
- 調整可能なアルゴリズム閾値とタイミング制御
- Legacy および v5 Silero モデルのサポート
- このリポジトリ内のデモ/テストアプリとドキュメントサイトのソース

## 機能 ✨

- Silero ONNX モデルを活用した browser-first の VAD パイプライン
- script tags、バンドラー、React で利用可能
- 実用的なデフォルトのマイクストリーム制約
- ストリームライフサイクルのオーバーライド（`getStream`, `pauseStream`, `resumeStream`）
- `NonRealTimeVAD` による事前録音音声の非リアルタイム区間分割
- `baseAssetPath` と `onnxWASMBasePath` によるモデル/アセット読み込み設定
- 組み込みラッパーにより legacy と v5 のモデル状態処理をサポート
- script tags、webpack ベースのバンドラー、React バンドラー、Next.js の各サンプルを収録

## プロジェクト構成 🗂️

```text
.
├── README.md
├── docs/                     # docs.vad.ricky0123.com の MkDocs ソース
├── examples/                 # script-tag, bundler, react-bundler, nextjs の例
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # 開発補助スクリプト
├── test-site/                # ローカルのインタラクティブ検証環境
├── i18n/                     # 翻訳済み README ファイル
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

より詳細な主要パス:

- `packages/web/src/real-time-vad.ts`: リアルタイムのマイク/AudioNode VAD オーケストレーション
- `packages/web/src/non-real-time-vad.ts`: 事前録音音声の非同期区間分割
- `packages/web/src/frame-processor.ts`: 閾値判定と発話区間境界ロジック
- `packages/react/src/index.ts`: `useMicVAD` の React フックライフサイクルと状態ラッパー

## 互換性マトリクス 🧩

| コンポーネント | 環境 |
| --- | --- |
| `@ricky0123/vad-web` | WebAudio + `MediaDevices.getUserMedia` を備えたモダンブラウザ |
| `@ricky0123/vad-react` | React アプリ（`react` / `react-dom` >= 16.8.0） |
| Docs toolchain | Python 3.10 + Poetry（CI workflow 準拠） |
| CI Node runtime | Node 18（リポジトリ workflow 準拠） |

前提メモ: サンプルとドキュメントは、このリポジトリスナップショット時点のパッケージ版（`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`）と整合しています。

## 前提条件 ✅

- ブラウザ利用: `MediaDevices.getUserMedia` が使えるモダンブラウザ
- ローカル開発: Node.js + npm workspaces
- ドキュメント開発: Python + Poetry（MkDocs ビルド用）

CI 設定に基づく推奨ローカル基準:

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

### クイックスタート（script tags）

ブラウザで script tag 経由で VAD を使うには、以下の script tag を追加します。

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

### ブラウザパッケージ利用（module import）

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React での利用

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

API 全体で共通する主なオプション:

- `positiveSpeechThreshold`（リアルタイムAPIでの既定値はおよそ `0.3`）
- `negativeSpeechThreshold`（リアルタイムAPIでの既定値はおよそ `0.25`）
- `redemptionMs`（リアルタイムAPIでの既定値はおよそ `1400`）
- `preSpeechPadMs`（リアルタイムAPIでの既定値はおよそ `800`）
- `minSpeechMs`（リアルタイムAPIでの既定値はおよそ `400`）

リアルタイムAPI（`MicVAD`, `useMicVAD`）で利用可能な追加オプション:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` または `"v5"`）
- `baseAssetPath` と `onnxWASMBasePath`
- `workletOptions`

完全なAPI表はドキュメントを参照してください: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) と [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### 設定レシピ: モデルとランタイムアセットのセルフホスト

CDN のデフォルトを使わない場合、アプリが以下を配信していることを確認してください。

- `silero_vad_legacy.onnx` および/または `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` のランタイムファイル（`.wasm`、および新しいランタイムビルド向けの `.mjs`）

そのうえで次のように設定します。

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

リポジトリ内のサンプル:

- `examples/script-tags`: 基本的な script-tag 構成
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js 統合例

`examples/bundler` のコマンド例:

```bash
npm run build && npm run start
```

ブラウザ向けの voice activity detector のバンドル方法や、node / React プロジェクトでの利用方法は [vad.ricky0123.com](https://www.vad.ricky0123.com) のドキュメントで確認できます。

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

各スクリプトの内容:

- `npm run build`: すべてのワークスペースをビルド
- `npm run test`: ワークスペースのテストを実行
- `npm run test:coverage`: `packages/web` のカバレッジを実行
- `npm run typecheck`: packages、test-site、tests の TypeScript を検査
- `npm run format-check`: `packages`、`examples`、`test-site` 配下の TS/TSX フォーマットを検査
- `npm run dev`: package と test-site ソースを監視し、再ビルドして `test-site/dist` を配信

Docs ビルド（MkDocs + Poetry）:

```bash
poetry install
poetry run mkdocs serve
```

補足:

- `./test-site/build.sh` は必要な VAD/ONNX Runtime アセットを `test-site/dist` と `test-site/dist/subpath` にコピーします
- `./scripts/dev.sh` は `nodemon` + `live-server` を使い、ポート `8080` でローカルの再ビルド・配信ループを実行します
- `./check_vad_up_to_date.sh` は過去のスクリプトで、`silero_vad.onnx` を参照しています（このリポジトリに含まれるのは `silero_vad_legacy.onnx` と `silero_vad_v5.onnx`）

## CIと品質ゲート 🧱

`.github/workflows/` の GitHub workflow でカバーしているもの:

- テスト（`test.yml`）
- 型チェック（`typecheck.yml`）
- フォーマットチェック（`format-check.yml`）
- Docs のビルド/デプロイ（`docs.yml`）
- 公開フロー（`publish.yml`）

これらの workflow は、想定ランタイム/ツールのバージョンやリリースチェックの実運用上の信頼できる基準です。

## トラブルシューティング 🩺

| 症状 | 確認 / 対処 |
| --- | --- |
| マイク権限が拒否される | ブラウザで対象オリジンにマイク権限が付与されているか確認してください。 |
| アセットの読み込み失敗（`.onnx`, `.wasm`, `.mjs`, worklet） | `baseAssetPath` / `onnxWASMBasePath` を正しく設定し、実際にファイルが配信されているか確認してください。 |
| 新しめの `onnxruntime-web` ランタイムで問題が出る | `.wasm` だけでなく `.mjs` も配信してください。 |
| 安全でないオリジンでのローカル開発 | ブラウザのマイクAPIは通常、安全なコンテキスト（`https` または `localhost`）が必要です。 |
| ビルド時のバンドラー問題 | [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/) のバンドルガイドを参照してください。 |
| Next.js 統合での問題 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) の設定パターンを使い、静的アセット配信パスを確認してください。 |

## スポンサーシップ ❤️

ぜひプロジェクトへの金銭的支援をご検討ください。特に商用プロダクトがこのパッケージに依存している場合は支援をお願いします。[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Nodeサポートに関する重要なお知らせ - 2024年10月 📢

サーバーサイドの node 環境向け音声活動検出パッケージ `ricky0123/vad-node` のサポートは段階的に終了します。今後、node パッケージの更新を公開する予定はありません。この判断をした理由は次のとおりです。

- このプロジェクトの本来のユースケースはクライアントサイドの音声活動検出でした。誰かから要望を受けて node サポートを追加しましたが、プロジェクトに割ける時間は限られており、`ricky0123/vad-node` を非推奨化することで `ricky0123/vad-web` により集中できます。
- 個々の開発者がサーバーサイド向けの独自VADソリューションを作ることは、onnxruntime-web、audio worklets などを使ってクライアントサイド実装を学ぶより容易です。そのため、`ricky0123/vad-web` のほうがコミュニティに提供できる価値が大きいと考えています。
- ブラウザ向けと node 向けパッケージの間でコードを共有するのは、VADモデルの実行・利用に関わる環境差異のため比較的扱いづらいです。
- [survey](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) によると、大半のユーザーは `ricky0123/vad-web`（および `ricky0123/vad-react`）を利用しています。

## ロードマップ 🛣️

現在の方向性（このリポジトリ状態と上記メンテナー注記に基づく）:

- browser-first API（`@ricky0123/vad-web`, `@ricky0123/vad-react`）への注力を継続
- バンドラーやフレームワーク向け docs/examples の維持と改善
- コントリビューター/開発者向けドキュメントと test-site ワークフローの改善
- `i18n/` 配下の翻訳READMEの追加とメンテナンス

## コントリビューション 🤝

- ハッキングガイドを確認: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- このリポジトリで issue や PR を作成: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- プロジェクトの概要を素早く把握するには [`HACKING.md`](HACKING.md) を参照

## 参考資料 📚

1. Silero VAD repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ライセンス 📄

- プロジェクトライセンス: ISC（[LICENSE](LICENSE) を参照）
