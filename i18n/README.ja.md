[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ JavaScript 向け音声活動検出

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

> わずか数行のコードで、ユーザー音声のある音声区間に対してコールバックを実行できます。

このパッケージは、ブラウザで動作する正確で使いやすい音声活動検出器（VAD）を提供することを目的としています。このパッケージを使うことで、ユーザーにマイク許可を依頼し、録音を開始し、音声が含まれる音声区間をサーバーへ送信して処理したり、ユーザーが話しているときにアニメーションやインジケーターを表示したりできます。
ブラウザユースケースに集中するため、[Node サポートを終了](#node-サポートに関する重要な更新---2024年10月-10-)することにしました。

| 🧭 概要 | 詳細 |
| --- | --- |
| 📦 コアパッケージ | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 主な実行環境 | ブラウザ（`WebAudio` + `getUserMedia`） |
| 📚 ドキュメント | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 デモ | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## 目次

- [クイックリンク 🔗](#クイックリンク-)
- [概要 🧭](#概要-)
- [特徴 ✨](#特徴-)
- [プロジェクト構成 🗂️](#プロジェクト構成-)
- [互換性マトリクス 🧩](#互換性マトリクス-)
- [前提条件 ✅](#前提条件-)
- [インストール 📦](#インストール-)
- [使い方 🚀](#使い方-)
- [設定 ⚙️](#設定-)
- [サンプル 🧪](#サンプル-)
- [開発ノート 🛠️](#開発ノート-)
- [CI と品質ゲート 🧱](#ci--品質ゲート-)
- [トラブルシューティング 🩺](#トラブルシューティング-)
- [スポンサーシップ ❤️](#スポンサーシップ-)
- [Node サポートに関する重要な更新 - 2024年10月 📢](#node-サポートに関する重要な更新---2024年10月-)
- [ロードマップ 🛣️](#ロードマップ-)
- [コントリビュート 🤝](#コントリビュート-)
- [参考文献 📚](#参考文献-)
- [❤️ Support](#-support)
- [ライセンス 📄](#ライセンス-)

## クイックリンク 🔗

| リソース | リンク |
| --- | --- |
| デモ | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| ドキュメント | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [コミュニティへ参加](https://discord.gg/4WPeGEaSpF) |
| アンケート | [利用ケースを共有](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| 貢献ガイド | [Developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- ドキュメントソースは `./docs` にあります。
- コントリビューター向けのオンボーディングはここから始まります: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/)。質問は issue や Discord で受け付けています。

内部では、これらのパッケージは [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) を使って [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#参考文献-) を実行しています（以前の Node サポート時代の ONNX Runtime Node.js の履歴的リファレンスあり）。この実現に協力してくれた方々に感謝します。

i18n の状態について: `i18n/` には、このファイル上部にリンクされている言語ごとの README の翻訳版が含まれます。

## 概要 🧭

このリポジトリは、2つの公開パッケージを持つモノレポです。

| パッケージ | 用途 |
| --- | --- |
| `@ricky0123/vad-web` | `MicVAD`, `AudioNodeVAD`, `NonRealTimeVAD` を含むブラウザ API |
| `@ricky0123/vad-react` | `vad-web` 向けの React フックラッパー（`useMicVAD`） |

このプロジェクトはブラウザファーストで、次の機能を含みます。

- 音声区間のリアルタイム取得コールバック（`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` など）
- アルゴリズム閾値とタイミング制御のカスタマイズ
- レガシーと v5 の Silero モデル対応
- デモ/テストアプリとこのリポジトリ内のドキュメントサイトソース

## 特徴 ✨

- Silero ONNX モデルによるブラウザ優先の VAD パイプライン
- script タグ、バンドラ、React で動作
- 妥当なデフォルトのマイクストリーム制約
- ストリームのライフサイクルを上書き可能 (`getStream`, `pauseStream`, `resumeStream`)
- `NonRealTimeVAD` による事前録音オーディオ向けの非リアルタイム音声分割
- `baseAssetPath` と `onnxWASMBasePath` によるモデル/アセット読み込みの設定
- 組み込みラッパーでレガシーと v5 のモデル状態をサポート
- script タグ、webpack 系バンドラ、React バンドラ、Next.js の例を含む

## プロジェクト構成 🗂️

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

より詳細なパス:

- `packages/web/src/real-time-vad.ts`: マイク/音声ノードのリアルタイム VAD オーケストレーション
- `packages/web/src/non-real-time-vad.ts`: 事前録音音声の非同期セグメンテーション
- `packages/web/src/frame-processor.ts`: 閾値処理と音声区間境界ロジック
- `packages/react/src/index.ts`: `useMicVAD` の React フックライフサイクルと状態ラッパー

## 互換性マトリクス 🧩

| コンポーネント | 実行環境 |
| --- | --- |
| `@ricky0123/vad-web` | モダンブラウザ（`WebAudio` + `MediaDevices.getUserMedia`） |
| `@ricky0123/vad-react` | React アプリ (`react` / `react-dom` >= 16.8.0) |
| Docs ツールチェーン | Python 3.10 + Poetry（CI ワークフロー準拠） |
| CI Node runtime | Node 18（リポジトリワークフロー準拠） |

リポジトリスナップショットのパッケージバージョン（`packages/*/package.json`）:

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## 前提条件 ✅

- ブラウザ利用: `MediaDevices.getUserMedia` をサポートするモダンブラウザ
- ローカル開発: Node.js + npm workspaces
- ドキュメント開発: Python + Poetry（MkDocs ビルド用）

CI 設定に基づく推奨のローカル基準:

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

ブラウザで script タグ経由で VAD を使う場合は、次の script タグを読み込みます。

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

API 全体で共通のオプション:

- `positiveSpeechThreshold`（リアルタイム API の既定値はおよそ `0.3`）
- `negativeSpeechThreshold`（リアルタイム API の既定値はおよそ `0.25`）
- `redemptionMs`（リアルタイム API の既定値はおよそ `1400`）
- `preSpeechPadMs`（リアルタイム API の既定値はおよそ `800`）
- `minSpeechMs`（リアルタイム API の既定値はおよそ `400`）

リアルタイム API（`MicVAD`, `useMicVAD`）はさらに以下をサポートします。

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model`（`"legacy"` または `"v5"`）
- `baseAssetPath` と `onnxWASMBasePath`
- `workletOptions`

詳細 API テーブルはドキュメントをご確認ください: [API リファレンス](https://docs.vad.ricky0123.com/user-guide/api/) と [アルゴリズムガイド](https://docs.vad.ricky0123.com/user-guide/algorithm/)。

### 設定レシピ: モデルとランタイムアセットをセルフホスティングする

CDN デフォルトを使わない場合は、アプリが次を配信していることを確認します。

- `silero_vad_legacy.onnx` と/または `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` ランタイムファイル（`.wasm`、および新しいランタイムでは `.mjs`）

その後、次のように設定します。

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

- `examples/script-tags`: script-tag の基本構成
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js の統合例

`examples/bundler` の実行例:

```bash
npm run build && npm run start
```

ブラウザ向け音声活動検出器のバンドルや、Node/React プロジェクトでの利用方法については [vad.ricky0123.com](https://www.vad.ricky0123.com) を参照してください。

## 開発ノート 🛠️

ルートワークスペースのスクリプト:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

各コマンドの役割:

- `npm run build`: すべてのワークスペースをビルド
- `npm run test`: ワークスペーステストを実行
- `npm run test:coverage`: `packages/web` のカバレッジを取得
- `npm run typecheck`: `packages`、`test-site`、`tests` の TypeScript チェック
- `npm run format-check`: `packages`、`examples`、`test-site` 配下の TS/TSX の書式を確認
- `npm run dev`: パッケージと test-site のソースを監視、再ビルドし、`test-site/dist` を配信

ドキュメントビルド（MkDocs + Poetry）:

```bash
poetry install
poetry run mkdocs serve
```

補足メモ:

- `./test-site/build.sh` は必要な VAD/ONNX Runtime アセットを `test-site/dist` と `test-site/dist/subpath` にコピーします。
- `./scripts/dev.sh` は `nodemon` + `live-server` を使って、ローカルの再ビルド&配信ループをポート `8080` で実行します。
- `./check_vad_up_to_date.sh` は履歴的なもので、`silero_vad.onnx` を参照します。現在のリポジトリには `silero_vad_legacy.onnx` と `silero_vad_v5.onnx` が同梱されています。

## CI と品質ゲート 🧱

`.github/workflows/` にある GitHub ワークフロー:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Format Check (`format-check.yml`)
- Docs build/deploy (`docs.yml`)
- Publish (`publish.yml`)

これらのワークフローは、想定されるランタイム/ツールバージョンとリリースチェックの実際の基準となります。

## トラブルシューティング 🩺

| 症状 | 確認 / 対処 |
| --- | --- |
| マイクの許可が拒否される | ブラウザがオリジンに対してマイク権限を持っていることを確認してください。 |
| アセットの読み込み失敗（`.onnx`, `.wasm`, `.mjs`, worklet） | `baseAssetPath` / `onnxWASMBasePath` を正しく設定し、ファイルが実際に配信されていることを確認してください。 |
| 新しい `onnxruntime-web` での問題 | `.wasm` だけでなく `.mjs` も配信してください。 |
| ローカル開発時の安全でないオリジン | ブラウザのマイク API は通常、セキュアコンテキスト（`https` または `localhost`）を必要とします。 |
| ビルド時のバンドル問題 | [ブラウザ向けドキュメント](https://docs.vad.ricky0123.com/user-guide/browser/) のバンドルガイドに従ってください。 |
| Next.js 統合の問題 | [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) にある設定パターンを使い、静的アセット配信パスを確認してください。 |

## スポンサーシップ ❤️

このプロジェクトはぜひ経済的にサポートしてください。特に、商用プロダクトでこのパッケージを利用している場合は要件があります。
[![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Node サポートに関する重要な更新 - 2024年10月 📢

`ricky0123/vad-node`（サーバーサイド Node 環境向け音声活動検出パッケージ）のサポートを停止します。今後、このリポジトリから Node パッケージを更新していく予定はありません。
この決定は次の理由によります。

- このプロジェクトの元々のユースケースはクライアント側の音声活動検出でした。Node サポートは誰かの要望で追加したもので、協力のために導入しました。しかし、現在の開発時間は限られているため、`ricky0123/vad-node` を終了し、`ricky0123/vad-web` に集中する時間を増やしたいです。
- 個人開発者にとって、onnxruntime-web、audio worklet、その他の技術を学んでクライアント側ソリューションを作るよりも、サーバー側で独自の音声活動検出ソリューションを作る方が一般に簡単です。従って、コミュニティには `ricky0123/vad-web` の価値がより高いと考えています。
- ブラウザと Node の実行環境は、VAD モデルを実行・利用する際に重要な点で異なるため、両パッケージ間でコードを共有するのはかなり難しいです。
- [アンケート](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)結果でも、ほとんどのユーザーが `ricky0123/vad-web`（必要に応じて `ricky0123/vad-react`）を利用しています。

## ロードマップ 🛣️

現在の方針（リポジトリ状態と保守者ノートに基づく）:

- ブラウザ優先 API（`@ricky0123/vad-web`, `@ricky0123/vad-react`）への注力を継続
- バンドラとフレームワーク向けのドキュメント/サンプルの維持と改善
- コントリビューター/開発者向けドキュメントと test-site ワークフローの改善
- `i18n/` 配下の翻訳 README の追加と維持

## コントリビュート 🤝

- hacking ガイドを読む: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- このリポジトリで issue や PR を作成: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- すばやく全体像を把握するには、[`HACKING.md`](HACKING.md) を確認してください。

## 参考文献 📚

1. Silero VAD リポジトリ: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ライセンス 📄

- プロジェクトライセンス: ISC（[LICENSE](LICENSE) 参照）


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
