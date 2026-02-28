[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


---

[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)
---

# 🎙️ Sprachaktivitätserkennung für JavaScript

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

> Führe Callbacks auf Audiosegmenten mit Sprache in nur wenigen Zeilen Code aus.

Dieses Paket soll einen präzisen, benutzerfreundlichen Sprachaktivitätserkennungs-Detektor (VAD) bereitstellen, der im Browser läuft. Mit diesem Paket können Sie die Mikrofonberechtigung anfragen, die Audioaufnahme starten, Sprachsegmente mit gesprochener Sprache an Ihren Server zur Verarbeitung senden oder eine Animation/Anzeige einblenden, wenn der Nutzer spricht. Beachten Sie, dass ich mich entschieden habe, [den Node-Support einzustellen](#wichtige-aktualisierung-zur-node-unterstützung---okt-2024-) um mich auf den Browser-Fall zu konzentrieren.

| 🧭 Auf einen Blick | Details |
| --- | --- |
| 📦 Kernpakete | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 Primäre Laufzeitumgebung | Browser (`WebAudio` + `getUserMedia`) |
| 📚 Dokumentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 Live-Demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Inhaltsverzeichnis

- [Schnellstart-Links 🔗](#schnellstart-links-)
- [Überblick 🧭](#überblick-)
- [Funktionen ✨](#funktionen-)
- [Projektstruktur 🗂️](#projektstruktur-)
- [Kompatibilitätsmatrix 🧩](#kompatibilitätsmatrix-)
- [Voraussetzungen ✅](#voraussetzungen-)
- [Installation 📦](#installation-)
- [Verwendung 🚀](#verwendung-)
- [Konfiguration ⚙️](#konfiguration-)
- [Beispiele 🧪](#beispiele-)
- [Entwicklungsnotizen 🛠️](#entwicklungsnotizen-)
- [CI & Qualitätskontrollen 🧱](#ci--qualitätskontrollen-)
- [Fehlerbehebung 🩺](#fehlerbehebung-)
- [Sponsoring ❤️](#sponsoring-)
- [Wichtige Aktualisierung zur Node-Unterstützung - Okt 2024 📢](#wichtige-aktualisierung-zur-node-unterstützung---okt-2024-)
- [Roadmap 🛣️](#roadmap-)
- [Beitrag leisten 🤝](#beitrag-leisten-)
- [Referenzen 📚](#referenzen-)
- [❤️ Support](#-support)
- [Lizenz 📄](#lizenz-)

## Schnellstart-Links 🔗

| Ressource | Link |
| --- | --- |
| Live-Demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Dokumentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Community beitreten](https://discord.gg/4WPeGEaSpF) |
| Umfrage | [Anwendungsfall teilen](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Beitragshandbuch | [Hacker-Leitfaden für Entwickler](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Die Dokumentationsquelle liegt in `./docs`.
- Das Onboarding für Beitragende beginnt hier: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Fragen sind willkommen über Issues oder Discord.

Im Hintergrund nutzen diese Pakete [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referenzen-) über [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (mit historischen Verweisen auf ONNX Runtime Node.js aus der früheren Node-Unterstützung). Vielen Dank an diese Leute dafür, dass das möglich ist.

Hinweis zum i18n-Status: `i18n/` enthält Übersetzungen der README-Dateien für die am Anfang verlinkten Sprachen.

## Überblick 🧭

Dieses Repository ist ein Monorepo mit zwei primär veröffentlichten Paketen:

| Paket | Zweck |
| --- | --- |
| `@ricky0123/vad-web` | Browser-APIs inkl. `MicVAD`, `AudioNodeVAD` und `NonRealTimeVAD` |
| `@ricky0123/vad-react` | React-Wrapper (`useMicVAD`) für `vad-web` |

Das Projekt ist browser-zentriert und umfasst:

- Echtzeit-Callbacks für Mikrofonsegmentierung (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` usw.)
- Konfigurierbare Algorithmusschwellen und Zeitsteuerung
- Unterstützung für Legacy- und V5-Silero-Modelle
- Demo-/Test-Apps und die Quell-Dateien der Dokumentation in diesem Repository

## Funktionen ✨

- Browser-first VAD-Pipeline, betrieben von Silero ONNX-Modellen
- Funktioniert mit Script-Tags, Bundlern und React
- Sinnvolle Standardwerte für Mikrofon-Stream-Einschränkungen
- Überschreibbarer Stream-Lebenszyklus (`getStream`, `pauseStream`, `resumeStream`)
- Nicht-echtzeitliche Sprachsegmentierung für voraufgezeichnetes Audio über `NonRealTimeVAD`
- Konfigurierbares Laden von Modell- und Laufzeitdateien über `baseAssetPath` und `onnxWASMBasePath`
- Unterstützt sowohl den Legacy- als auch den V5-Modellzustand über eingebaute Wrapper
- Enthält Beispiele für Script-Tags, webpack-basierte Bundler, React-Bundler und Next.js

## Projektstruktur 🗂️

```text
.
├── README.md
├── docs/                     # MkDocs-Quelle für docs.vad.ricky0123.com
├── examples/                 # script-tag, bundler, react-bundler, nextjs Beispiele
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # Entwicklungshilfen
├── test-site/                # lokaler interaktiver Spielplatz
├── i18n/                     # übersetzte README-Dateien
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

Weitere Pfade:

- `packages/web/src/real-time-vad.ts`: Orchestrierung der Echtzeit-Mikrofon-/Audio-Node-VAD
- `packages/web/src/non-real-time-vad.ts`: Async-Segmentierung für voraufgezeichnetes Audio
- `packages/web/src/frame-processor.ts`: Thresholding- und Sprachsegmentgrenzenlogik
- `packages/react/src/index.ts`: Lifecycle des React Hooks `useMicVAD` und State-Wrapper

## Kompatibilitätsmatrix 🧩

| Komponente | Umgebung |
| --- | --- |
| `@ricky0123/vad-web` | Moderne Browser mit WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | React-Apps (`react` / `react-dom` >= 16.8.0) |
| Docs-Toolchain | Python 3.10 + Poetry (laut CI-Workflow) |
| CI Node-Laufzeit | Node 18 (laut Repository-Workflows) |

Snapshot-Paketversionen des Repositories (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Voraussetzungen ✅

- Browsernutzung: Ein moderner Browser mit `MediaDevices.getUserMedia`
- Lokale Entwicklung: Node.js + npm workspaces
- Dokumentationsentwicklung: Python + Poetry (für MkDocs-Build)

Empfohlene lokale Basis je nach CI-Konfiguration:

- Node.js 18.x
- Python 3.10.x

## Installation 📦

Installation des Browser-Pakets:

```bash
npm i @ricky0123/vad-web
```

Installation des React-Wrapper:

```bash
npm i @ricky0123/vad-react
```

Installation der Monorepo-Abhängigkeiten (für Beitragende):

```bash
npm install
```

## Verwendung 🚀

### Schnellstart (Script-Tags)

Um VAD im Browser über ein Script-Tag zu verwenden, binden Sie diese Script-Tags ein:

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

### Verwendung des Browser-Pakets (Modulimport)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React-Verwendung

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

### Nicht-Echtzeit-Verwendung (Batch-Audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Konfiguration ⚙️

Gemeinsame Optionen über alle APIs hinweg:

- `positiveSpeechThreshold` (Standardwert bei Echtzeit-APIs: ca. `0.3`)
- `negativeSpeechThreshold` (Standardwert bei Echtzeit-APIs: ca. `0.25`)
- `redemptionMs` (Standardwert bei Echtzeit-APIs: ca. `1400`)
- `preSpeechPadMs` (Standardwert bei Echtzeit-APIs: ca. `800`)
- `minSpeechMs` (Standardwert bei Echtzeit-APIs: ca. `400`)

Echtzeit-APIs (`MicVAD`, `useMicVAD`) unterstützen außerdem:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` oder `"v5"`)
- `baseAssetPath` und `onnxWASMBasePath`
- `workletOptions`

Vollständige API-Tabellen finden Sie in der Dokumentation: [API-Referenz](https://docs.vad.ricky0123.com/user-guide/api/) und [Algorithmus-Leitfaden](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Konfigurationsrezept: Modell und Runtime-Assets selbst hosten

Wenn Sie nicht die CDN-Standardwerte nutzen, stellen Sie sicher, dass Ihre App Folgendes ausliefert:

- `silero_vad_legacy.onnx` und/oder `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web` Runtime-Dateien (`.wasm`; und `.mjs` für neuere Runtime-Builds)

Dann konfigurieren Sie:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Beispiele 🧪

Repository-Beispiele:

- `examples/script-tags`: grundlegende Script-Tag-Konfiguration
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js-Integrationsbeispiel

Beispielbefehl aus `examples/bundler`:

```bash
npm run build && npm run start
```

Die Dokumentation zum Bündeln des Sprachaktivitätserkenners für den Browser oder zur Nutzung in Node- oder React-Projekten finden Sie auf [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Entwicklungsnotizen 🛠️

Workspace-Skripte im Repository-Root:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Was sie tun:

- `npm run build`: baut alle Workspaces
- `npm run test`: führt Workspace-Tests aus
- `npm run test:coverage`: Coverage für `packages/web`
- `npm run typecheck`: prüft TypeScript in packages, test-site und Tests
- `npm run format-check`: prüft die Formatierung für TS/TSX unter `packages`, `examples`, `test-site`
- `npm run dev`: überwacht die Package- und test-site-Quellen, baut neu und serviert `test-site/dist`

Dokumentations-Build (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Weitere Hinweise:

- `./test-site/build.sh` kopiert erforderliche VAD/ONNX Runtime-Assets nach `test-site/dist` und `test-site/dist/subpath`
- `./scripts/dev.sh` verwendet `nodemon` + `live-server` für lokale Rebuild-and-Serve-Schleifen auf Port `8080`
- `./check_vad_up_to_date.sh` ist historisch und verweist auf `silero_vad.onnx` (während dieses Repository `silero_vad_legacy.onnx` und `silero_vad_v5.onnx` ausliefert)

## CI & Qualitätskontrollen 🧱

Die GitHub-Workflows in `.github/workflows/` umfassen:

- Test (`test.yml`)
- Typprüfung (`typecheck.yml`)
- Formatierung (`format-check.yml`)
- Docs-Build/-Deployment (`docs.yml`)
- Publish-Flow (`publish.yml`)

Diese Workflows sind eine praktische Quelle für erwartete Laufzeit-/Tool-Versionen und Release-Prüfungen.

## Fehlerbehebung 🩺

| Symptom | Prüfung / Lösung |
| --- | --- |
| Mikrofonzugriff verweigert | Stellen Sie sicher, dass der Browser für Ihre Origin die Mikrofonberechtigung hat. |
| Assets werden nicht geladen (`.onnx`, `.wasm`, `.mjs`, worklet) | Setzen Sie `baseAssetPath` / `onnxWASMBasePath` korrekt und prüfen Sie, dass die Dateien tatsächlich ausgeliefert werden. |
| Neuere `onnxruntime-web` Runtime-Probleme | Stellen Sie zusätzlich `.mjs`-Dateien bereit, nicht nur `.wasm`. |
| Lokale Entwicklung über unsicherem Ursprung | Browser-Mikrofon-APIs erfordern meist sichere Kontexte (`https` oder `localhost`). |
| Build-Fehler beim Bundler | Verwenden Sie die Bundle-Hinweise in der [Browser-Dokumentation](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Next.js-Integrationsprobleme | Nutzen Sie die in [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) gezeigten Konfigurationsmuster und prüfen Sie die Hosting-Pfade statischer Assets. |

## Sponsoring ❤️

Bitte tragen Sie finanziell zum Projekt bei – insbesondere wenn Ihr kommerzielles Produkt auf diesem Paket basiert. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Wichtige Aktualisierung zur Node-Unterstützung - Okt 2024 📢

Ich werde die Unterstützung für `ricky0123/vad-node`, das Sprachaktivitätserkennungs-Paket für Node-Serverumgebungen, herunterfahren. Ich plane nicht, in Zukunft weitere Updates für das Node-Paket zu veröffentlichen. Ich habe diese Entscheidung aus folgenden Gründen getroffen:

- Mein ursprünglicher Anwendungsfall für dieses Projekt war die clientseitige Sprachaktivitätserkennung. Ich habe Node-Support ergänzt, weil jemand darum gebeten hat und ich hilfreich sein wollte. Allerdings habe ich nicht viel Zeit, um an diesem Projekt zu arbeiten, und die Einstellung von `ricky0123/vad-node` gibt mir mehr Zeit, mich auf `ricky0123/vad-web` zu konzentrieren.
- Für einzelne Entwickler ist es deutlich einfacher, eine eigene serverseitige Spracherkennungs-Lösung zu bauen, als sich in onnxruntime-web, Audio Worklets und andere Technologien einzuarbeiten, um eine clientseitige Lösung zu erstellen. Deshalb sehe ich `ricky0123/vad-web` als größeren Nutzen für die Community.
- Das Teilen von Code zwischen Browser- und Node-Paketen ist ziemlich umständlich, da sich die Umgebungen in für das Ausführen und Verwenden des VAD-Modells relevanten Punkten deutlich unterscheiden.
- Die Mehrheit der Nutzer verwendet laut [Umfrage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) `ricky0123/vad-web` (möglicherweise mit `ricky0123/vad-react`).

## Roadmap 🛣️

Aktuelle Richtung (basierend auf dem Repository-Zustand und dem Hinweis des Maintainers oben):

- Weiterhin Fokus auf browser-first APIs (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Dokumentation und Beispiele für Bundler und Frameworks pflegen und verbessern
- Entwickler-/Beitragsdokumentation und Workflows für test-site verbessern
- Übersetzte READMEs unter `i18n/` hinzufügen und pflegen

## Beitrag leisten 🤝

- Lesen Sie den Hacking-Leitfaden: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Eröffnen Sie Issues oder PRs in diesem Repository: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Für schnellen Projektkontext siehe [`HACKING.md`](HACKING.md)

## Referenzen 📚

1. Silero-VAD-Repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Lizenz 📄

- Projektlizenz: ISC (siehe [LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
