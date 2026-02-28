[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Spracherkennung im Browser für JavaScript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Führe Callbacks auf Sprachsegmenten mit Benutzersprache mit nur wenigen Zeilen aus.

Dieses Paket soll einen präzisen und benutzerfreundlichen Voice-Activity-Detector (VAD) bereitstellen, der im Browser läuft. Mit diesem Paket können Sie den Nutzer um Mikrofonberechtigungen bitten, mit der Audioaufnahme starten, Sprachsegmente mit Sprache an Ihren Server zur Verarbeitung senden oder eine bestimmte Animation oder Anzeige anzeigen, wenn der Nutzer spricht. Beachten Sie, dass ich mich entschieden habe, [die Node-Unterstützung zu beenden](#wichtige-aktualisierung-zum-node-support---okt-2024-) und mich auf die Browser-Nutzung zu konzentrieren.

| Auf einen Blick | Details |
| --- | --- |
| Kernpakete | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Primäre Laufzeit | Browser (`WebAudio` + `getUserMedia`) |
| Dokumentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Live-Demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Inhaltsverzeichnis

- [Schnellzugriff 🔗](#schnellzugriff-)
- [Überblick 🧭](#uberblick-)
- [Funktionen ✨](#funktionen-)
- [Projektstruktur 🗂️](#projektstruktur-)
- [Kompatibilitätsmatrix 🧩](#kompatibilitatsmatrix-)
- [Voraussetzungen ✅](#voraussetzungen-)
- [Installation 📦](#installation-)
- [Verwendung 🚀](#verwendung-)
- [Konfiguration ⚙️](#konfiguration-)
- [Beispiele 🧪](#beispiele-)
- [Entwicklungsnotizen 🛠️](#entwicklungsnotizen-)
- [CI & Qualitätskontrollen 🧱](#ci--qualitatskontrollen-)
- [Fehlerbehebung 🩺](#fehlerbehebung-)
- [Sponsoring ❤️](#sponsoring-)
- [❤️ Support](#-support)
- [Wichtige Aktualisierung zum Node-Support - Okt 2024 📢](#wichtige-aktualisierung-zum-node-support---okt-2024-)
- [Roadmap 🛣️](#roadmap-)
- [Mitwirkung 🤝](#mitwirkung-)
- [Referenzen 📚](#referenzen-)
- [Lizenz 📄](#lizenz-)

## Schnellzugriff 🔗

| Ressource | Link |
| --- | --- |
| Live-Demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Dokumentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Gemeinschaft beitreten](https://discord.gg/4WPeGEaSpF) |
| Umfrage | [Nutzen Sie Ihren Fall ausfüllen](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Beitragsleitfaden | [Entwickler-Hacking-Leitfaden](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Die Dokumentationsquelle liegt in `./docs`.
- Das Einarbeiten von Beitragenden beginnt hier: [Entwickler-Hacking-Leitfaden](https://docs.vad.ricky0123.com/developer-guide/hacking/). Fragen sind willkommen über Issues oder Discord.

Im Hintergrund verwenden diese Pakete [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referenzen) mit [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (mit historischen Verweisen auf ONNX Runtime Node.js aus der früheren Node-Unterstützung). Vielen Dank an alle, die dies möglich gemacht haben.

Hinweis zum i18n-Status: `i18n/` enthält übersetzte README-Dateien für die Spracheinträge, die oben verlinkt sind.

## Überblick 🧭

Dieses Repository ist ein Monorepo mit zwei primären veröffentlichten Paketen:

| Paket | Zweck |
| --- | --- |
| `@ricky0123/vad-web` | Browser-APIs inkl. `MicVAD`, `AudioNodeVAD` und `NonRealTimeVAD` |
| `@ricky0123/vad-react` | React-Hook-Wraper (`useMicVAD`) für `vad-web` |

Das Projekt ist browser-first konzipiert und umfasst:

- Echtzeit-Mikrofon-Segmentierungs-Callbacks (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, usw.)
- Konfigurierbare Algorithmusschwellen und Zeitsteuerung
- Unterstützung für legacy- und v5-Silero-Modelle
- Demo-/Test-Apps und Quellen der Docs-Website in diesem Repository

## Funktionen ✨

- Browser-first VAD-Pipeline auf Basis von Silero ONNX-Modellen
- Funktioniert mit Script-Tags, Bundlern und React
- Sinnvolle Standard-Constraints für den Mikrofon-Stream
- Anpassbarer Stream-Lifecycle (`getStream`, `pauseStream`, `resumeStream`)
- Nicht-Echtzeit-Sprachsegmentierung für voraufgenommenes Audio über `NonRealTimeVAD`
- Konfigurierbares Modell-/Asset-Laden über `baseAssetPath` und `onnxWASMBasePath`
- Unterstützt legacy- und v5-Modellzustände über eingebaute Wrapper
- Enthält Beispiele für Script-Tags, webpack-basierte Bundler, React-Bundler und Next.js

## Projektstruktur 🗂️

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

Ausführlichere Pfade:

- `packages/web/src/real-time-vad.ts`: Echtzeit-Mikrofon/Audio-Node VAD-Orchestrierung
- `packages/web/src/non-real-time-vad.ts`: Asynchrone Segmentierung für voraufgenommenes Audio
- `packages/web/src/frame-processor.ts`: Schwellenwertsetzung und Ermittlung von Sprachsegmentgrenzen
- `packages/react/src/index.ts`: Lebenszyklus von `useMicVAD` und Zustandswrapper in React

## Kompatibilitatsmatrix 🧩

| Komponente | Umgebung |
| --- | --- |
| `@ricky0123/vad-web` | Moderne Browser mit WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | React-Apps (`react` / `react-dom` >= 16.8.0) |
| Docs-Toolchain | Python 3.10 + Poetry (gemäß CI-Workflow) |
| CI Node-Laufzeit | Node 18 (gemäß Repository-Workflows) |

Paketversionen zum Repository-Snapshot (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Voraussetzungen ✅

- Browser-Nutzung: ein moderner Browser mit `MediaDevices.getUserMedia`
- Lokale Entwicklung: Node.js + npm workspaces
- Dokumentationsentwicklung: Python + Poetry (für MkDocs-Build)

Empfohlene lokale Basis basierend auf der CI-Konfiguration:

- Node.js 18.x
- Python 3.10.x

## Installation 📦

Installiere das Browser-Paket:

```bash
npm i @ricky0123/vad-web
```

Installiere den React-Wrapper:

```bash
npm i @ricky0123/vad-react
```

Installiere Monorepo-Abhängigkeiten (für Beitragende):

```bash
npm install
```

## Verwendung 🚀

### Schnellstart (Script-Tags)

Um VAD im Browser per Script-Tag zu verwenden, binde die folgenden Script-Tags ein:

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

### Browser-Paket verwenden (Modulimport)

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

Gemeinsame Optionen über APIs hinweg beinhalten:

- `positiveSpeechThreshold` (Standardwert ca. `0.3` in Echtzeit-APIs)
- `negativeSpeechThreshold` (Standardwert ca. `0.25` in Echtzeit-APIs)
- `redemptionMs` (Standardwert ca. `1400` in Echtzeit-APIs)
- `preSpeechPadMs` (Standardwert ca. `800` in Echtzeit-APIs)
- `minSpeechMs` (Standardwert ca. `400` in Echtzeit-APIs)

Echtzeit-APIs (`MicVAD`, `useMicVAD`) unterstützen zusätzlich:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` oder `"v5"`)
- `baseAssetPath` und `onnxWASMBasePath`
- `workletOptions`

Siehe vollständige API-Tabellen in der Doku: [API-Referenz](https://docs.vad.ricky0123.com/user-guide/api/) und [Algorithmus-Guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Konfigurationsanleitung: Modell- und Laufzeit-Assets selbst hosten

Wenn keine CDN-Standardwerte verwendet werden, stellen Sie sicher, dass Ihre App Folgendes bereitstellt:

- `silero_vad_legacy.onnx` und/oder `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web`-Laufzeitdateien (`.wasm`; und `.mjs` für neuere Runtime-Builds)

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

- `examples/script-tags`: einfache Script-Tag-Einrichtung
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js-Integrationsbeispiel

Beispielbefehl aus `examples/bundler`:

```bash
npm run build && npm run start
```

Dokumentation zum Bundling des Sprachaktivitätserkennungsmoduls für den Browser oder zur Verwendung in Node- oder React-Projekten finden Sie auf [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Entwicklungsnotizen 🛠️

Root-Workspace-Skripte:

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
- `npm run typecheck`: prüft TypeScript in Paketen, test-site und Tests
- `npm run format-check`: prüft Formatierung für TS/TSX unter `packages`, `examples`, `test-site`
- `npm run dev`: beobachtet Package- und test-site-Quellen, baut neu und dient `test-site/dist`

Dokumentations-Build (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Weitere Hinweise:

- `./test-site/build.sh` kopiert erforderliche VAD/ONNX Runtime-Assets nach `test-site/dist` und `test-site/dist/subpath`
- `./scripts/dev.sh` nutzt `nodemon` + `live-server` für lokale Rebuild-and-serve-Schleifen auf Port `8080`
- `./check_vad_up_to_date.sh` ist historisch und verweist auf `silero_vad.onnx` (während dieses Repo `silero_vad_legacy.onnx` und `silero_vad_v5.onnx` liefert)

## CI & Qualitätskontrollen 🧱

Die GitHub-Workflows in `.github/workflows/` umfassen:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatierung (`format-check.yml`)
- Docs Build/Deployment (`docs.yml`)
- Publish-Flow (`publish.yml`)

Diese Workflows sind eine praktische Wahrheit über die erwarteten Laufzeit-/Tool-Versionen und Release-Prüfungen.

## Fehlerbehebung 🩺

| Symptom | Prüfung / Korrektur |
| --- | --- |
| Mikrofonberechtigung verweigert | Stellen Sie sicher, dass der Browser Berechtigungen für das Mikrofon Ihrer Origin hat. |
| Assets laden nicht (`.onnx`, `.wasm`, `.mjs`, Worklet) | Setzen Sie `baseAssetPath` / `onnxWASMBasePath` korrekt und verifizieren Sie, dass Dateien tatsächlich ausgeliefert werden. |
| Neuere `onnxruntime-web`-Runtime-Probleme | Stellen Sie auch `.mjs`-Dateien bereit, nicht nur `.wasm`. |
| Lokale Entwicklung über unsichere Origin | Browser-Mikrofon-APIs benötigen typischerweise sichere Kontexte (`https` oder `localhost`). |
| Build-Bundling-Probleme | Nutzen Sie die Bundling-Anleitung in der [Browser-Dokumentation](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Next.js-Integrationsprobleme | Verwenden Sie Konfigurationsmuster aus [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) und überprüfen Sie statische Asset-Hosting-Pfade. |

## Sponsoring ❤️

Bitte unterstützen Sie das Projekt finanziell – besonders wenn Ihr kommerzielles Produkt auf diesem Paket basiert. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazyingart/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Wichtige Aktualisierung zum Node-Support - Okt 2024 📢

Ich werde den Support für `ricky0123/vad-node`, das Paket für Sprachaktivitätserkennung in serverseitigen Node-Umgebungen, einstellen. Ich plane nicht, künftig Aktualisierungen für das Node-Paket zu veröffentlichen. Ich habe diese Entscheidung aus diesen Gründen getroffen:

- Mein ursprünglicher Anwendungsfall für dieses Projekt war die Sprachaktivitätserkennung auf der Client-Seite. Ich habe Node-Unterstützung hinzugefügt, weil jemand dies angefragt hatte und ich helfen wollte. Ich habe jedoch nicht viel Zeit mehr für dieses Projekt, und die Einstellung von `ricky0123/vad-node` gibt mir mehr Zeit, mich auf `ricky0123/vad-web` zu konzentrieren.
- Es ist deutlich einfacher für einzelne Entwickler, eigene serverseitige Sprachaktivitätserkennungs-Lösungen zu erstellen, als für Entwickler zu lernen, wie man mit onnxruntime-web, Audio Worklets und anderen Technologien eine clientseitige Lösung aufbaut. Deshalb sehe ich `ricky0123/vad-web` als wertvoller für die Gemeinschaft an.
- Das Teilen von Code zwischen Browser- und Node-Paketen ist ziemlich umständlich, da die Umgebungen in für den Betrieb und Einsatz des Sprachaktivitätsmodells relevanten Punkten unterschiedlich sind.
- Laut [Umfrage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) nutzen die meisten Nutzer `ricky0123/vad-web` (möglicherweise mit `ricky0123/vad-react`).

## Roadmap 🛣️

Aktuelle Richtung (basierend auf dem aktuellen Repository-Zustand und dem Wartungshinweis oben):

- Weiterhin Fokus auf browser-first APIs (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Pflege und Verbesserung von Docs/Beispielen für Bundler und Frameworks
- Verbesserung der Beitragenden-/Entwicklerdokumentation und test-site Workflows
- Hinzufügen und Pflegen übersetzter READMEs unter `i18n/`

## Mitwirkung 🤝

- Lesen Sie den Hacking-Leitfaden: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Öffnen Sie Issues oder PRs in diesem Repository: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Für schnellen Projekthintergrund siehe [`HACKING.md`](HACKING.md)

## Referenzen 📚

1. Silero VAD Repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Lizenz 📄

- Projektlizenz: ISC (siehe [LICENSE](LICENSE))
