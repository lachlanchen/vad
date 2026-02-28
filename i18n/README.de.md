[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Voice Activity Detection für Javascript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Führe Callbacks für Audiobereiche mit gesprochener Sprache in wenigen Codezeilen aus.

Dieses Paket hat das Ziel, einen präzisen und benutzerfreundlichen Voice Activity Detector (VAD) bereitzustellen, der im Browser läuft. Mit diesem Paket kannst du den Nutzer nach Mikrofonberechtigungen fragen, Audioaufnahmen starten, Audiobereiche mit Sprache zur Verarbeitung an deinen Server senden oder eine bestimmte Animation bzw. einen Indikator anzeigen, wenn der Nutzer spricht. Beachte, dass ich mich entschieden habe, [die Node-Unterstützung einzustellen](#wichtiges-update-zur-node-unterstützung---okt-2024-), um mich auf den Browser-Anwendungsfall zu konzentrieren.

## Inhaltsverzeichnis

- [Schnellzugriffe 🔗](#schnellzugriffe-)
- [Überblick 🧭](#überblick-)
- [Funktionen ✨](#funktionen-)
- [Projektstruktur 🗂️](#projektstruktur-)
- [Kompatibilitätsmatrix 🧩](#kompatibilitätsmatrix-)
- [Voraussetzungen ✅](#voraussetzungen-)
- [Installation 📦](#installation-)
- [Verwendung 🚀](#verwendung-)
- [Konfiguration ⚙️](#konfiguration-)
- [Beispiele 🧪](#beispiele-)
- [Entwicklungshinweise 🛠️](#entwicklungshinweise-)
- [CI & Quality Gates 🧱](#ci--quality-gates-)
- [Fehlerbehebung 🩺](#fehlerbehebung-)
- [Sponsoring ❤️](#sponsoring-)
- [Wichtiges Update zur Node-Unterstützung - Okt 2024 📢](#wichtiges-update-zur-node-unterstützung---okt-2024-)
- [Roadmap 🛣️](#roadmap-)
- [Beitragen 🤝](#beitragen-)
- [Referenzen 📚](#referenzen-)
- [Lizenz 📄](#lizenz-)

## Schnellzugriffe 🔗

| Ressource | Link |
| --- | --- |
| Live-Demo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Dokumentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Community beitreten](https://discord.gg/4WPeGEaSpF) |
| Umfrage | [Teile deinen Anwendungsfall](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Leitfaden zum Beitragen | [Developer-Hacking-Guide](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Durchsuche die Dokumentation, deren Quellcode sich im Verzeichnis `./docs` befindet.
- Wenn du beitragen möchtest, habe ich [hier](https://docs.vad.ricky0123.com/developer-guide/hacking/) begonnen, eine Dokumentation zum Einstieg in die Entwicklung an diesen Paketen zu schreiben. Wenn du Fragen hast, kannst du hier ein Issue eröffnen oder eine Nachricht auf Discord hinterlassen.

Unter der Haube führen diese Pakete [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referenzen) über [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node) aus. Vielen Dank an alle Beteiligten, die das möglich machen.

Hinweis zum i18n-Status: `i18n/` existiert und enthält mehrere übersetzte README-Dateien. Der Sprachselektor oben enthält außerdem Links für geplante/Platzhalter-Übersetzungen (`README.de.md`, `README.ru.md`), die in diesem Repository-Snapshot möglicherweise nicht vorhanden sind.

## Überblick 🧭

Dieses Repository ist ein Monorepo mit zwei primären veröffentlichten Paketen:

| Paket | Zweck |
| --- | --- |
| `@ricky0123/vad-web` | Browser-APIs einschließlich `MicVAD`, `AudioNodeVAD` und `NonRealTimeVAD` |
| `@ricky0123/vad-react` | React-Hook-Wrapper (`useMicVAD`) für `vad-web` |

Das Projekt ist browser-first und umfasst:

- Echtzeit-Callbacks für Mikrofonsegmentierung (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` usw.)
- Konfigurierbare Algorithmus-Schwellenwerte und Timing-Steuerungen
- Unterstützung für Legacy- und v5-Silero-Modelle
- Demo-/Test-Apps und Quellen der Dokumentationsseite in diesem Repository

## Funktionen ✨

- Browser-first-VAD-Pipeline auf Basis von Silero-ONNX-Modellen
- Funktioniert mit Script-Tags, Bundlern und React
- Sinnvolle Standard-Stream-Constraints für das Mikrofon
- Überschreibbarer Stream-Lebenszyklus (`getStream`, `pauseStream`, `resumeStream`)
- Nicht-Echtzeit-Sprachsegmentierung für voraufgezeichnetes Audio über `NonRealTimeVAD`
- Konfigurierbares Laden von Modell/Assets über `baseAssetPath` und `onnxWASMBasePath`
- Unterstützt sowohl Legacy- als auch v5-Modellzustandsverwaltung über integrierte Wrapper
- Enthält Beispiele für Script-Tags, webpack-basierte Bundler, React-Bundler und Next.js

## Projektstruktur 🗂️

```text
.
├── README.md
├── docs/                     # MkDocs-Quellen für docs.vad.ricky0123.com
├── examples/                 # script-tag-, bundler-, react-bundler-, nextjs-Beispiele
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # Entwicklungs-Helfer
├── test-site/                # lokaler interaktiver Playground
├── i18n/                     # übersetzte README-Dateien
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

Detailliertere Pfade:

- `packages/web/src/real-time-vad.ts`: Echtzeit-Orchestrierung für Mikrofon/Audio-Node-VAD
- `packages/web/src/non-real-time-vad.ts`: asynchrone Segmentierung für voraufgezeichnetes Audio
- `packages/web/src/frame-processor.ts`: Schwellwertlogik und Logik für Sprachsegmentgrenzen
- `packages/react/src/index.ts`: Lebenszyklus- und Zustands-Wrapper des React-Hooks `useMicVAD`

## Kompatibilitätsmatrix 🧩

| Komponente | Umgebung |
| --- | --- |
| `@ricky0123/vad-web` | Moderne Browser mit WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | React-Apps (`react` / `react-dom` >= 16.8.0) |
| Docs-Toolchain | Python 3.10 + Poetry (laut CI-Workflow) |
| CI-Node-Runtime | Node 18 (laut Repository-Workflows) |

Annahme-Hinweis: Beispiele und Dokumentation sind konsistent mit den aktuellen Paketversionen in diesem Repository-Snapshot (`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`).

## Voraussetzungen ✅

- Browser-Nutzung: ein moderner Browser mit `MediaDevices.getUserMedia`
- Lokale Entwicklung: Node.js + npm-Workspaces
- Entwicklung der Dokumentation: Python + Poetry (für MkDocs-Build)

Empfohlene lokale Basis laut CI-Konfiguration:

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

Installiere Monorepo-Abhängigkeiten (für Mitwirkende):

```bash
npm install
```

## Verwendung 🚀

### Schnellstart (Script-Tags)

Um den VAD im Browser über ein Script-Tag zu verwenden, füge die folgenden Script-Tags ein:

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

Häufige Optionen über die APIs hinweg sind:

- `positiveSpeechThreshold` (Standard in Echtzeit-APIs ungefähr `0.3`)
- `negativeSpeechThreshold` (Standard in Echtzeit-APIs ungefähr `0.25`)
- `redemptionMs` (Standard in Echtzeit-APIs ungefähr `1400`)
- `preSpeechPadMs` (Standard in Echtzeit-APIs ungefähr `800`)
- `minSpeechMs` (Standard in Echtzeit-APIs ungefähr `400`)

Echtzeit-APIs (`MicVAD`, `useMicVAD`) unterstützen außerdem:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` oder `"v5"`)
- `baseAssetPath` und `onnxWASMBasePath`
- `workletOptions`

Vollständige API-Tabellen findest du in der Dokumentation: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) und [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Konfigurationsrezept: Modell- und Runtime-Assets selbst hosten

Wenn du keine CDN-Standards verwendest, stelle sicher, dass deine App Folgendes bereitstellt:

- `silero_vad_legacy.onnx` und/oder `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- `onnxruntime-web`-Runtime-Dateien (`.wasm`; und `.mjs` für neuere Runtime-Builds)

Dann konfiguriere:

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

Beispiele im Repository:

- `examples/script-tags`: grundlegendes Script-Tag-Setup
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: Next.js-Integrationsbeispiel

Beispielbefehl aus `examples/bundler`:

```bash
npm run build && npm run start
```

Dokumentation zum Bundling des Voice Activity Detectors für den Browser oder zur Verwendung in Node- oder React-Projekten findest du auf [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Entwicklungshinweise 🛠️

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
- `npm run dev`: beobachtet Package- und test-site-Quellen, baut neu und stellt `test-site/dist` bereit

Docs-Build (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Zusätzliche Hinweise:

- `./test-site/build.sh` kopiert benötigte VAD-/ONNX-Runtime-Assets nach `test-site/dist` und `test-site/dist/subpath`
- `./scripts/dev.sh` verwendet `nodemon` + `live-server` für lokale Rebuild-und-Serve-Schleifen auf Port `8080`
- `./check_vad_up_to_date.sh` ist historisch und referenziert `silero_vad.onnx` (während dieses Repo `silero_vad_legacy.onnx` und `silero_vad_v5.onnx` ausliefert)

## CI & Quality Gates 🧱

GitHub-Workflows unter `.github/workflows/` decken ab:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Docs-Build/Deployment (`docs.yml`)
- Publish-Flow (`publish.yml`)

Diese Workflows sind eine praktische Quelle der Wahrheit für erwartete Runtime-/Tool-Versionen und Release-Checks.

## Fehlerbehebung 🩺

| Symptom | Prüfen / Beheben |
| --- | --- |
| Mikrofonberechtigung verweigert | Stelle sicher, dass der Browser Mikrofonzugriff für deinen Origin hat. |
| Assets laden nicht (`.onnx`, `.wasm`, `.mjs`, worklet) | Setze `baseAssetPath` / `onnxWASMBasePath` korrekt und prüfe, ob die Dateien tatsächlich bereitgestellt werden. |
| Probleme mit neuerer `onnxruntime-web`-Runtime | Stelle zusätzlich `.mjs`-Dateien bereit, nicht nur `.wasm`. |
| Lokale Entwicklung über unsicheren Origin | Browser-Mikrofon-APIs erfordern typischerweise sichere Kontexte (`https` oder `localhost`). |
| Bundler-Probleme zur Build-Zeit | Nutze die Bundling-Hinweise in den [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Probleme bei der Next.js-Integration | Verwende Konfigurationsmuster aus [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) und prüfe die Hosting-Pfade statischer Assets. |

## Sponsoring ❤️

Bitte unterstütze das Projekt finanziell, insbesondere wenn dein kommerzielles Produkt von diesem Paket abhängt. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Wichtiges Update zur Node-Unterstützung - Okt 2024 📢

Ich werde die Unterstützung für `ricky0123/vad-node`, das Voice-Activity-Detection-Paket für serverseitige Node-Umgebungen, auslaufen lassen. Ich plane, ab jetzt keine Updates mehr für das Node-Paket zu veröffentlichen. Ich habe diese Entscheidung aus folgenden Gründen getroffen:

- Mein ursprünglicher Anwendungsfall für dieses Projekt war clientseitige Voice Activity Detection. Ich habe Node-Unterstützung hinzugefügt, weil jemand darum gebeten hat und ich helfen wollte. Ich habe jedoch nicht viel Zeit, an diesem Projekt zu arbeiten, und die Abkündigung von `ricky0123/vad-node` gibt mir mehr Zeit, mich auf `ricky0123/vad-web` zu konzentrieren.
- Für einzelne Entwickler ist es deutlich einfacher, maßgeschneiderte serverseitige Voice-Activity-Detection-Lösungen zu erstellen, als zu lernen, wie man mit onnxruntime-web, Audio-Worklets und anderen Technologien eine clientseitige Lösung umsetzt. Deshalb sehe ich in `ricky0123/vad-web` einen größeren Mehrwert für die Community.
- Das Teilen von Code zwischen Browser- und Node-Paketen ist eher umständlich, weil sich die Umgebungen in für den Betrieb und die Verwendung des Voice-Activity-Detection-Modells relevanten Punkten unterscheiden.
- Laut der [Umfrage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) nutzen die meisten Anwender `ricky0123/vad-web` (möglicherweise zusammen mit `ricky0123/vad-react`).

## Roadmap 🛣️

Aktuelle Richtung (basierend auf dem Repository-Status und dem Maintainer-Hinweis oben):

- Weiterer Fokus auf browser-first-APIs (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Pflege und Verbesserung der Dokumentation/Beispiele für Bundler und Frameworks
- Verbesserung der Mitwirkenden-/Entwicklerdokumentation und der test-site-Workflows
- Hinzufügen und Pflegen übersetzter READMEs unter `i18n/`

## Beitragen 🤝

- Lies den Hacking-Guide: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Eröffne Issues oder PRs in diesem Repository: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Für schnellen Projektkontext siehe [`HACKING.md`](HACKING.md)

## Referenzen 📚

1. Silero-VAD-Repository: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Lizenz 📄

- Projektlizenz: ISC (siehe [LICENSE](LICENSE))
