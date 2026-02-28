[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)



[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Детекция голосовой активности для JavaScript

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

> Запускайте callbacks на фрагментах аудио с речью пользователя всего за несколько строк кода.

Этот пакет предназначен для точного и удобного в использовании детектора голосовой активности (VAD), работающего в браузере. С его помощью можно запросить у пользователя разрешение на доступ к микрофону, начать запись аудио, отправлять участки речи на сервер для обработки или показывать анимацию/индикатор, когда пользователь говорит. Обратите внимание, что я решил [отказаться от поддержки Node](#важное-обновление-о-поддержке-node---октябрь-2024-) в пользу браузерного сценария.

| 🧭 Вкратце | Подробности |
| --- | --- |
| Основные пакеты | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Основная среда выполнения | Браузер (`WebAudio` + `getUserMedia`) |
| Документация | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Живое демо | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Содержание

- [Быстрые ссылки 🔗](#быстрые-ссылки-)
- [Обзор 🧭](#обзор-)
- [Возможности ✨](#возможности-)
- [Структура проекта 🗂️](#структура-проекта-)
- [Матрица совместимости 🧩](#матрица-совместимости-)
- [Предварительные требования ✅](#предварительные-требования-)
- [Установка 📦](#установка-)
- [Использование 🚀](#использование-)
- [Конфигурация ⚙️](#конфигурация-)
- [Примеры 🧪](#примеры-)
- [Заметки по разработке 🛠️](#заметки-по-разработке-)
- [CI и контроль качества 🧱](#ci-и-контроль-качества-)
- [Устранение неполадок 🩺](#устранение-неполадок-)
- [Спонсорство ❤️](#спонсорство-)
- [Важное обновление о поддержке Node — октябрь 2024 📢](#важное-обновление-о-поддержке-node---октябрь-2024-)
- [Дорожная карта 🛣️](#дорожная-карта-)
- [Участие в разработке 🤝](#участие-в-разработке-)
- [Источники 📚](#источники-)
- [❤️ Support](#-support)
- [Лицензия 📄](#лицензия-)

## Быстрые ссылки 🔗

| Ресурс | Ссылка |
| --- | --- |
| Живое демо | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Документация | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Присоединиться к сообществу](https://discord.gg/4WPeGEaSpF) |
| Опрос | [Поделитесь кейсом использования](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Руководство для контрибьюторов | [Руководство для разработчика](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Документация проекта находится в `./docs`.
- Онбординг для контрибьюторов начинается здесь: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Вопросы приветствуются в issue или в Discord.

Внутри этих пакетов используется [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#источники) через [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (с историческими ссылками на ONNX Runtime Node.js из ранней поддержки Node). Огромное спасибо тем, кто сделал это возможным.

Примечание по i18n: каталог `i18n/` содержит переводы README для языков, перечисленных в верхней части этого файла.

## Обзор 🧭

Этот репозиторий — монорепозиторий с двумя основными опубликованными пакетами:

| Пакет | Назначение |
| --- | --- |
| `@ricky0123/vad-web` | Browser API, включая `MicVAD`, `AudioNodeVAD` и `NonRealTimeVAD` |
| `@ricky0123/vad-react` | React-обертка-хук (`useMicVAD`) для `vad-web` |

Проект построен с упором на браузер и включает:

- Колбэки сегментации речи в реальном времени микрофона (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire` и т. д.)
- Настраиваемые пороги алгоритма и временные параметры
- Поддержка legacy и v5 моделей Silero
- Демо/тестовые приложения и исходники сайта документации в этом репозитории

## Возможности ✨

- Browser-first VAD pipeline на базе ONNX-моделей Silero
- Работает с `script`-тегами, бандлерами и React
- Продуманные ограничения потока микрофона по умолчанию
- Переопределяемый lifecycle потока (`getStream`, `pauseStream`, `resumeStream`)
- Нерейлтайм сегментация речи для заранее записанного аудио через `NonRealTimeVAD`
- Настраиваемая загрузка модели и ассетов через `baseAssetPath` и `onnxWASMBasePath`
- Поддержка состояния legacy и v5-моделей через встроенные обертки
- Примеры для `script`-тегов, webpack-бандлеров, React-бандлеров и Next.js

## Структура проекта 🗂️

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

Дополнительные важные пути:

- `packages/web/src/real-time-vad.ts`: оркестрация real-time VAD для микрофона и audio-node
- `packages/web/src/non-real-time-vad.ts`: асинхронная сегментация для заранее записанного аудио
- `packages/web/src/frame-processor.ts`: пороги и логика границ сегментов речи
- `packages/react/src/index.ts`: жизненный цикл React-хука и обертки состояния `useMicVAD`

## Матрица совместимости 🧩

| Компонент | Окружение |
| --- | --- |
| `@ricky0123/vad-web` | Современные браузеры с WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Приложения React (`react` / `react-dom` >= 16.8.0) |
| Цепочка сборки документации | Python 3.10 + Poetry (по CI workflow) |
| Node runtime в CI | Node 18 (по CI-воркфлоу репозитория) |

Снимок версий пакетов (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Предварительные требования ✅

- Браузерное использование: современный браузер с `MediaDevices.getUserMedia`
- Локальная разработка: Node.js + npm workspaces
- Разработка документации: Python + Poetry (для сборки MkDocs)

Рекомендуемый локальный baseline по CI-конфигу:

- Node.js 18.x
- Python 3.10.x

## Установка 📦

Установка браузерного пакета:

```bash
npm i @ricky0123/vad-web
```

Установка React-обертки:

```bash
npm i @ricky0123/vad-react
```

Установка зависимостей монорепозитория (для контрибьюторов):

```bash
npm install
```

## Использование 🚀

### Быстрый старт (script-теги)

Чтобы использовать VAD через `script`-тег в браузере, подключите:

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

### Использование браузерного пакета (импорт модуля)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### React

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

### Нерельтайм-использование (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Конфигурация ⚙️

Типичные параметры для API:

- `positiveSpeechThreshold` (по умолчанию около `0.3` в real-time API)
- `negativeSpeechThreshold` (по умолчанию около `0.25` в real-time API)
- `redemptionMs` (по умолчанию около `1400` в real-time API)
- `preSpeechPadMs` (по умолчанию около `800` в real-time API)
- `minSpeechMs` (по умолчанию около `400` в real-time API)

Real-time API (`MicVAD`, `useMicVAD`) также поддерживают:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` или `"v5"`)
- `baseAssetPath` и `onnxWASMBasePath`
- `workletOptions`

Полные таблицы API в документации: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) и [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Рецепт конфигурации: self-hosting модели и runtime-ассетов

Если вы не используете CDN по умолчанию, убедитесь, что ваше приложение отдает:

- `silero_vad_legacy.onnx` и/или `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- runtime-файлы `onnxruntime-web` (`.wasm`; и `.mjs` для новых сборок runtime)

Затем настройте:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Примеры 🧪

Примеры из репозитория:

- `examples/script-tags`: базовая настройка с `script`-тегами
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: пример интеграции с Next.js

Пример команды из `examples/bundler`:

```bash
npm run build && npm run start
```

Документация по сборке voice activity detector для браузера или использовании его в Node/React-проектах находится на [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Заметки по разработке 🛠️

Скрипты root-рабочего пространства:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Что они делают:

- `npm run build`: собирает все workspaces
- `npm run test`: запускает тесты workspace
- `npm run test:coverage`: coverage для `packages/web`
- `npm run typecheck`: проверяет TypeScript в пакетах, test-site и tests
- `npm run format-check`: проверяет форматирование TS/TSX в `packages`, `examples`, `test-site`
- `npm run dev`: отслеживает исходники пакетов и test-site, пересобирает и запускает `test-site/dist`

Сборка документации (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Дополнительные заметки:

- `./test-site/build.sh` копирует обязательные VAD/ONNX Runtime ассеты в `test-site/dist` и `test-site/dist/subpath`
- `./scripts/dev.sh` использует `nodemon` + `live-server` для локальных циклов rebuild-and-serve на порту `8080`
- `./check_vad_up_to_date.sh` — исторический скрипт и ссылается на `silero_vad.onnx` (в то время как репозиторий содержит `silero_vad_legacy.onnx` и `silero_vad_v5.onnx`)

## CI и контроль качества 🧱

GitHub workflow в `.github/workflows/` охватывают:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Сборка/развертывание документации (`docs.yml`)
- Процесс публикации (`publish.yml`)

Эти workflows — практический источник правды по ожидаемым версиям runtime/tooling и проверкам релиза.

## Устранение неполадок 🩺

| Симптом | Проверка / Исправление |
| --- | --- |
| Доступ к микрофону отклонен | Проверьте, что у браузера есть разрешение на микрофон для вашего origin. |
| Не загружаются ассеты (`.onnx`, `.wasm`, `.mjs`, worklet) | Корректно настройте `baseAssetPath` / `onnxWASMBasePath` и убедитесь, что файлы реально отдаются. |
| Проблемы с более новой версией `onnxruntime-web` | Также отдавайте `.mjs` файлы, а не только `.wasm`. |
| Локальная разработка с небезопасным origin | API микрофона обычно требуют безопасный контекст (`https` или `localhost`). |
| Ошибки сборщика во время сборки | Используйте рекомендации в [документации браузера](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Проблемы интеграции с Next.js | Используйте паттерны конфигурации из [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) и проверьте пути размещения статических ассетов. |

## Спонсорство ❤️

Поддержите проект финансово — особенно если ваш коммерческий продукт опирается на этот пакет. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Важное обновление о поддержке Node — октябрь 2024 📢

Я прекращаю поддержку `ricky0123/vad-node`, пакета детекции голосовой активности для серверной среды Node. Я не планирую публиковать новые обновления этого node-пакета. Это решение принято по следующим причинам:

- Первоначально этот проект был сделан для client-side детекции голосовой активности. Я добавил поддержку Node, потому что это попросили, и я хотел помочь. Однако у меня мало времени на проект, и отказ от `ricky0123/vad-node` даст мне больше времени для разработки `ricky0123/vad-web`.
- Для отдельных разработчиков проще сделать собственное серверное решение VAD, чем осваивать onnxruntime-web, audio worklets и связанные технологии ради клиентского решения. Поэтому я считаю, что `ricky0123/vad-web` приносит сообществу больше пользы.
- Обмен кодом между браузерным и node-пакетами довольно неудобен, потому что окружения различаются по ряду аспектов, важных для запуска и использования модели детекции.
- По данным [опроса](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), большинство пользователей использует `ricky0123/vad-web` (возможно, вместе с `ricky0123/vad-react`).

## Дорожная карта 🛣️

Текущее направление (исходя из состояния репозитория и примечания мейнтейнера выше):

- Продолжать фокус на browser-first API (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Поддерживать и улучшать документацию/примеры для бандлеров и фреймворков
- Улучшать документацию для участников и процессы test-site
- Добавлять и поддерживать переводы README в `i18n/`

## Участие в разработке 🤝

- Ознакомьтесь с [руководством для разработчиков](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Открывайте issue или PR в этом репозитории: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Для быстрого контекста проекта см. [`HACKING.md`](HACKING.md)

## Источники 📚

1. Репозиторий Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Лицензия 📄

- Лицензия проекта: ISC (см. [LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
