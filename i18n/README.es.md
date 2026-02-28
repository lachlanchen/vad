[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)



[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Detección de actividad de voz para JavaScript

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

> Ejecuta callbacks en segmentos de audio con voz de usuario en pocas líneas de código.

Este paquete busca ofrecer un detector de actividad de voz (VAD) preciso y fácil de usar que funcione en el navegador. Con este paquete puedes pedir permisos de micrófono al usuario, iniciar la grabación de audio, enviar segmentos con voz a tu servidor para procesarlos o mostrar una animación/indicador cuando el usuario está hablando. Ten en cuenta que decidí [dejar de dar soporte a Node](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-) para enfocarme en el caso de uso del navegador.

| 🧭 En resumen | Detalles |
| --- | --- |
| 📦 Paquetes principales | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 Entorno principal | Navegador (`WebAudio` + `getUserMedia`) |
| 📚 Documentación | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 Demo en vivo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Tabla de contenidos

- [Enlaces rápidos 🔗](#enlaces-r%C3%A1pidos-)
- [Vista general 🧭](#vista-general-)
- [Características ✨](#caracteristicas-)
- [Estructura del proyecto 🗂️](#estructura-del-proyecto-)
- [Matriz de compatibilidad 🧩](#matriz-de-compatibilidad-)
- [Prerrequisitos ✅](#prerrequisitos-)
- [Instalación 📦](#instalacion-)
- [Uso 🚀](#uso-)
- [Configuración ⚙️](#configuracion-)
- [Ejemplos 🧪](#ejemplos-)
- [Notas de desarrollo 🛠️](#notas-de-desarrollo-)
- [CI y puertas de calidad 🧱](#ci-y-puertas-de-calidad-)
- [Solución de problemas 🩺](#solucion-de-problemas-)
- [Patrocinio ❤️](#patrocinio-)
- [Actualización importante sobre el soporte de Node - Oct 2024 📢](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-)
- [Hoja de ruta 🛣️](#hoja-de-ruta-)
- [Contribuir 🤝](#contribuir-)
- [Referencias 📚](#referencias-)
- [❤️ Support](#-support)
- [Licencia 📄](#licencia-)

## Enlaces rápidos 🔗

| Recurso | Enlace |
| --- | --- |
| Demo en vivo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentación | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Únete a la comunidad](https://discord.gg/4WPeGEaSpF) |
| Encuesta | [Comparte tu caso de uso](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Guía de contribución | [Guía para desarrolladores](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- La fuente de documentación vive en `./docs`.
- La incorporación de colaboradores empieza aquí: [guía para desarrolladores](https://docs.vad.ricky0123.com/developer-guide/hacking/). Las preguntas son bienvenidas por issues o Discord.

Bajo el capó, estos paquetes ejecutan [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referencias-) usando [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (con referencias históricas a ONNX Runtime Node.js de cuando sí había soporte para Node). Muchísimas gracias a quienes hicieron esto posible.

Nota del estado de i18n: `i18n/` incluye archivos README traducidos para las opciones de idioma enlazadas en la parte superior.

## Vista general 🧭

Este repositorio es un monorepo con dos paquetes publicados principales:

| Paquete | Propósito |
| --- | --- |
| `@ricky0123/vad-web` | APIs del navegador incluyendo `MicVAD`, `AudioNodeVAD` y `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper de hook de React (`useMicVAD`) para `vad-web` |

El proyecto está orientado primero al navegador e incluye:

- Callbacks de segmentación del micrófono en tiempo real (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Umbrales de algoritmo y controles de tiempo configurables
- Soporte de modelo Silero legacy y v5
- Apps de demo/pruebas y fuentes del sitio de documentación en este repositorio

## Características ✨

- Pipeline VAD orientado al navegador impulsado por modelos Silero ONNX
- Funciona con tags de script, empaquetadores y React
- Restricciones de stream de micrófono razonables por defecto
- Ciclo de vida del stream sobrescribible (`getStream`, `pauseStream`, `resumeStream`)
- Segmentación de voz fuera de tiempo real para audio pregrabado vía `NonRealTimeVAD`
- Carga configurable de modelo/recursos con `baseAssetPath` y `onnxWASMBasePath`
- Soporte de estados de modelo legacy y v5 mediante wrappers incluidos
- Incluye ejemplos para tags de script, empaquetadores con webpack, empaquetadores de React y Next.js

## Estructura del proyecto 🗂️

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

Rutas más detalladas:

- `packages/web/src/real-time-vad.ts`: orquestación VAD en tiempo real para micrófono/audio-node
- `packages/web/src/non-real-time-vad.ts`: segmentación asíncrona para audio pregrabado
- `packages/web/src/frame-processor.ts`: lógica de umbrales y límites de segmentos de voz
- `packages/react/src/index.ts`: ciclo de vida y wrapper de estado del hook `useMicVAD`

## Matriz de compatibilidad 🧩

| Componente | Entorno |
| --- | --- |
| `@ricky0123/vad-web` | Navegadores modernos con WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Apps React (`react` / `react-dom` >= 16.8.0) |
| Cadena de herramientas de docs | Python 3.10 + Poetry (según workflow de CI) |
| Runtime de Node en CI | Node 18 (según workflows del repositorio) |

Versiones de paquetes en el estado del repositorio (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prerrequisitos ✅

- Uso en navegador: un navegador moderno con `MediaDevices.getUserMedia`
- Desarrollo local: Node.js + npm workspaces
- Desarrollo de docs: Python + Poetry (para build de MkDocs)

Línea base recomendada según configuración de CI:

- Node.js 18.x
- Python 3.10.x

## Instalación 📦

Instala el paquete para navegador:

```bash
npm i @ricky0123/vad-web
```

Instala el wrapper de React:

```bash
npm i @ricky0123/vad-react
```

Instala dependencias del monorepo (para contribuyentes):

```bash
npm install
```

## Uso 🚀

### Inicio rápido (tags de script)

Para usar VAD con una etiqueta script en el navegador, incluye los tags siguientes:

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

### Uso del paquete del navegador (importación de módulo)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### Uso con React

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

### Uso no en tiempo real (audio por lotes)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuración ⚙️

Opciones comunes en las APIs:

- `positiveSpeechThreshold` (por defecto alrededor de `0.3` en APIs en tiempo real)
- `negativeSpeechThreshold` (por defecto alrededor de `0.25` en APIs en tiempo real)
- `redemptionMs` (por defecto alrededor de `1400` en APIs en tiempo real)
- `preSpeechPadMs` (por defecto alrededor de `800` en APIs en tiempo real)
- `minSpeechMs` (por defecto alrededor de `400` en APIs en tiempo real)

Las APIs en tiempo real (`MicVAD`, `useMicVAD`) también soportan:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` o `"v5"`)
- `baseAssetPath` y `onnxWASMBasePath`
- `workletOptions`

Consulta las tablas completas en la documentación: [referencia de API](https://docs.vad.ricky0123.com/user-guide/api/) y [guía del algoritmo](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Receta de configuración: autoalojar modelo y recursos de runtime

Si no usas valores CDN por defecto, asegúrate de que tu app sirva:

- `silero_vad_legacy.onnx` y/o `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Archivos del runtime de `onnxruntime-web` (`.wasm`; y `.mjs` para builds de runtime más nuevos)

Luego configura:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Ejemplos 🧪

Ejemplos del repositorio:

- `examples/script-tags`: configuración básica con script-tag
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: ejemplo de integración con Next.js

Comando de ejemplo de `examples/bundler`:

```bash
npm run build && npm run start
```

La documentación para empaquetar el detector de actividad de voz para navegador o usarlo en proyectos Node/React está en [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Notas de desarrollo 🛠️

Scripts del workspace raíz:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Qué hacen:

- `npm run build`: construye todos los workspaces
- `npm run test`: ejecuta tests de workspaces
- `npm run test:coverage`: cobertura para `packages/web`
- `npm run typecheck`: valida TypeScript en `packages`, `test-site` y tests
- `npm run format-check`: verifica el formato de TS/TSX en `packages`, `examples`, `test-site`
- `npm run dev`: observa fuentes de paquete y test-site, recompila y sirve `test-site/dist`

Build de docs (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Notas adicionales:

- `./test-site/build.sh` copia los assets de VAD/ONNX Runtime requeridos en `test-site/dist` y `test-site/dist/subpath`
- `./scripts/dev.sh` usa `nodemon` + `live-server` para bucles locales de reconstruir y servir en el puerto `8080`
- `./check_vad_up_to_date.sh` es histórico y referencia `silero_vad.onnx` (mientras este repo distribuye `silero_vad_legacy.onnx` y `silero_vad_v5.onnx`)

## CI y puertas de calidad 🧱

Los workflows de GitHub en `.github/workflows/` cubren:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formato (`format-check.yml`)
- Build/despliegue de docs (`docs.yml`)
- Flujo de publicación (`publish.yml`)

Estos workflows son una fuente práctica de verdad para las versiones esperadas de runtime/herramientas y las comprobaciones de release.

## Solución de problemas 🩺

| Síntoma | Comprobación / Corrección |
| --- | --- |
| Permiso de micrófono denegado | Asegúrate de que el navegador tenga permisos de micrófono para tu origen. |
| Los assets no cargan (`.onnx`, `.wasm`, `.mjs`, worklet) | Configura correctamente `baseAssetPath` / `onnxWASMBasePath` y verifica que los archivos realmente se estén sirviendo. |
| Problemas con `onnxruntime-web` más reciente | También sirve archivos `.mjs`, no solo `.wasm`. |
| Desarrollo local en origen inseguro | Las APIs de micrófono del navegador suelen requerir contextos seguros (`https` o `localhost`). |
| Problemas de bundling en build-time | Usa la guía de bundling en [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problemas de integración de Next.js | Usa los patrones de configuración que aparecen en [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) y verifica rutas de hosting de assets estáticos. |

## Patrocinio ❤️

Contribuye financieramente al proyecto, especialmente si tu producto comercial depende de este paquete. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Actualización importante sobre el soporte de Node - Oct 2024 📢

Voy a dejar de dar soporte a `ricky0123/vad-node`, el paquete de detección de actividad de voz para entornos de Node del lado del servidor. No planeo publicar más actualizaciones del paquete Node a partir de ahora. Tomé esta decisión por los siguientes motivos:

- Mi caso de uso original para este proyecto era la detección de actividad de voz del lado del cliente. Añadí soporte de Node porque alguien lo pidió y quise ser útil. Sin embargo, no tengo mucho tiempo para trabajar en este proyecto, y retirar `ricky0123/vad-node` me dará más tiempo para enfocarme en `ricky0123/vad-web`.
- Para desarrolladores individuales es mucho más fácil crear soluciones de detección de actividad de voz en servidor que aprender a usar onnxruntime-web, audio worklets y otras tecnologías para una solución del lado del cliente. Por eso considero que `ricky0123/vad-web` aporta más valor a la comunidad.
- Compartir código entre los paquetes de navegador y Node es bastante incómodo porque los entornos difieren en aspectos que afectan la ejecución y uso del modelo de detección de actividad de voz.
- La mayoría de usuarios, según la [encuesta](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), usan `ricky0123/vad-web` (posiblemente con `ricky0123/vad-react`).

## Hoja de ruta 🛣️

Dirección actual (basada en el estado del repositorio y la nota del mantenedor):

- Mantener el foco en APIs first para navegador (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Mantener y mejorar docs/ejemplos para bundlers y frameworks
- Mejorar documentación para contribuyentes/desarrolladores y flujos de `test-site`
- Agregar y mantener READMEs traducidos bajo `i18n/`

## Contribuir 🤝

- Lee la guía de hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Abre issues o PRs en este repositorio: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Para contexto rápido del proyecto, mira [`HACKING.md`](HACKING.md)

## Referencias 📚

1. Repositorio Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Licencia 📄

- Licencia del proyecto: ISC (ver [LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
