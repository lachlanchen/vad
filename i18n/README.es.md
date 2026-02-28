[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Detección de Actividad de Voz para Javascript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Ejecuta callbacks en segmentos de audio con voz del usuario en unas pocas líneas de código.

Este paquete busca ofrecer un detector de actividad de voz (VAD) preciso y fácil de usar que funciona en el navegador. Al usar este paquete, puedes solicitar permisos de micrófono al usuario, empezar a grabar audio, enviar al servidor segmentos de audio con voz para su procesamiento, o mostrar cierta animación o indicador cuando el usuario está hablando. Ten en cuenta que he decidido [discontinue node support](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-) para centrarme en el caso de uso del navegador.

## Tabla de Contenido

- [Enlaces Rápidos 🔗](#enlaces-rapidos-)
- [Resumen General 🧭](#resumen-general-)
- [Características ✨](#caracteristicas-)
- [Estructura del Proyecto 🗂️](#estructura-del-proyecto-️)
- [Matriz de Compatibilidad 🧩](#matriz-de-compatibilidad-)
- [Requisitos Previos ✅](#requisitos-previos-)
- [Instalación 📦](#instalacion-)
- [Uso 🚀](#uso-)
- [Configuración ⚙️](#configuracion-️)
- [Ejemplos 🧪](#ejemplos-)
- [Notas de Desarrollo 🛠️](#notas-de-desarrollo-️)
- [CI y Puertas de Calidad 🧱](#ci-y-puertas-de-calidad-)
- [Solución de Problemas 🩺](#solucion-de-problemas-)
- [Patrocinio ❤️](#patrocinio-️)
- [Actualización importante sobre el soporte de node - Oct 2024 📢](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-)
- [Hoja de Ruta 🛣️](#hoja-de-ruta-️)
- [Contribuir 🤝](#contribuir-)
- [Referencias 📚](#referencias-)
- [Licencia 📄](#licencia-)

## Enlaces Rápidos 🔗

| Recurso | Enlace |
| --- | --- |
| Demo en vivo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentación | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Únete a la comunidad](https://discord.gg/4WPeGEaSpF) |
| Encuesta | [Comparte tu caso de uso](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Guía de contribución | [Guía de hacking para desarrolladores](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Explora la documentación, cuyo código fuente se encuentra en el directorio `./docs`.
- Si quieres contribuir, empecé a escribir documentación sobre cómo empezar a trabajar en estos paquetes [aquí](https://docs.vad.ricky0123.com/developer-guide/hacking/). Si tienes preguntas, puedes abrir un issue aquí o dejar un mensaje en Discord.

Internamente, estos paquetes ejecutan [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referencias) usando [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node). Muchas gracias a esas personas por hacerlo posible.

Nota sobre el estado de i18n: `i18n/` existe e incluye varios archivos README traducidos. El selector de idioma de arriba también contiene enlaces para traducciones planificadas/de marcador de posición (`README.de.md`, `README.ru.md`) que pueden no estar presentes en esta instantánea del repositorio.

## Resumen General 🧭

Este repositorio es un monorepo con dos paquetes principales publicados:

| Paquete | Propósito |
| --- | --- |
| `@ricky0123/vad-web` | APIs de navegador, incluyendo `MicVAD`, `AudioNodeVAD` y `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper de hook de React (`useMicVAD`) para `vad-web` |

El proyecto está orientado primero al navegador e incluye:

- Callbacks de segmentación de micrófono en tiempo real (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Umbrales de algoritmo y controles de tiempo configurables
- Compatibilidad con modelos Silero legacy y v5
- Apps de demo/pruebas y código fuente del sitio de documentación en este repositorio

## Características ✨

- Pipeline VAD orientado al navegador impulsado por modelos Silero ONNX
- Funciona con script tags, bundlers y React
- Restricciones de stream de micrófono predeterminadas y razonables
- Ciclo de vida de stream sobreescribible (`getStream`, `pauseStream`, `resumeStream`)
- Segmentación de voz no en tiempo real para audio pregrabado mediante `NonRealTimeVAD`
- Carga configurable de modelo/assets mediante `baseAssetPath` y `onnxWASMBasePath`
- Compatibilidad con manejo de estado de modelos legacy y v5 mediante wrappers integrados
- Incluye ejemplos para script tags, bundlers basados en webpack, bundlers de React y Next.js

## Estructura del Proyecto 🗂️

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

- `packages/web/src/real-time-vad.ts`: orquestación de VAD de micrófono/audio-node en tiempo real
- `packages/web/src/non-real-time-vad.ts`: segmentación asíncrona para audio pregrabado
- `packages/web/src/frame-processor.ts`: lógica de umbrales y límites de segmentos de voz
- `packages/react/src/index.ts`: ciclo de vida y wrapper de estado del hook de React `useMicVAD`

## Matriz de Compatibilidad 🧩

| Componente | Entorno |
| --- | --- |
| `@ricky0123/vad-web` | Navegadores modernos con WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Apps React (`react` / `react-dom` >= 16.8.0) |
| Toolchain de docs | Python 3.10 + Poetry (según workflow de CI) |
| Runtime de Node en CI | Node 18 (según workflows del repositorio) |

Nota de suposición: los ejemplos y la documentación son coherentes con las versiones actuales de paquetes en esta instantánea del repositorio (`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`).

## Requisitos Previos ✅

- Uso en navegador: un navegador moderno con `MediaDevices.getUserMedia`
- Desarrollo local: Node.js + npm workspaces
- Desarrollo de documentación: Python + Poetry (para build de MkDocs)

Base local recomendada según la configuración de CI:

- Node.js 18.x
- Python 3.10.x

## Instalación 📦

Instala el paquete de navegador:

```bash
npm i @ricky0123/vad-web
```

Instala el wrapper de React:

```bash
npm i @ricky0123/vad-react
```

Instala las dependencias del monorepo (para contribuidores):

```bash
npm install
```

## Uso 🚀

### Inicio rápido (script tags)

Para usar el VAD con una script tag en el navegador, incluye las siguientes script tags:

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

### Uso del paquete de navegador (import de módulo)

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

- `positiveSpeechThreshold` (valor predeterminado cercano a `0.3` en APIs en tiempo real)
- `negativeSpeechThreshold` (valor predeterminado cercano a `0.25` en APIs en tiempo real)
- `redemptionMs` (valor predeterminado cercano a `1400` en APIs en tiempo real)
- `preSpeechPadMs` (valor predeterminado cercano a `800` en APIs en tiempo real)
- `minSpeechMs` (valor predeterminado cercano a `400` en APIs en tiempo real)

Las APIs en tiempo real (`MicVAD`, `useMicVAD`) también admiten:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` or `"v5"`)
- `baseAssetPath` and `onnxWASMBasePath`
- `workletOptions`

Consulta las tablas completas de API en la documentación: [API reference](https://docs.vad.ricky0123.com/user-guide/api/) y [algorithm guide](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Receta de configuración: alojar por cuenta propia modelo y assets de runtime

Cuando no uses los valores predeterminados de CDN, asegúrate de que tu aplicación sirva:

- `silero_vad_legacy.onnx` y/o `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Archivos de runtime de `onnxruntime-web` (`.wasm`; y `.mjs` para builds de runtime recientes)

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

Comando de ejemplo desde `examples/bundler`:

```bash
npm run build && npm run start
```

La documentación para empaquetar el detector de actividad de voz para el navegador o usarlo en proyectos node o React se puede encontrar en [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Notas de Desarrollo 🛠️

Scripts del workspace raíz:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Qué hace cada uno:

- `npm run build`: compila todos los workspaces
- `npm run test`: ejecuta las pruebas de los workspaces
- `npm run test:coverage`: cobertura para `packages/web`
- `npm run typecheck`: verifica TypeScript en paquetes, test-site y tests
- `npm run format-check`: verifica el formato de TS/TSX en `packages`, `examples`, `test-site`
- `npm run dev`: observa fuentes de paquetes y test-site, recompila y sirve `test-site/dist`

Build de docs (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Notas adicionales:

- `./test-site/build.sh` copia los assets necesarios de VAD/ONNX Runtime en `test-site/dist` y `test-site/dist/subpath`
- `./scripts/dev.sh` usa `nodemon` + `live-server` para bucles locales de recompilar y servir en el puerto `8080`
- `./check_vad_up_to_date.sh` es histórico y hace referencia a `silero_vad.onnx` (mientras que este repo incluye `silero_vad_legacy.onnx` y `silero_vad_v5.onnx`)

## CI y Puertas de Calidad 🧱

Los workflows de GitHub en `.github/workflows/` cubren:

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatting (`format-check.yml`)
- Build/deploy de docs (`docs.yml`)
- Flujo de publicación (`publish.yml`)

Estos workflows son una fuente práctica de verdad sobre las versiones de runtime/herramientas esperadas y las comprobaciones de lanzamiento.

## Solución de Problemas 🩺

| Síntoma | Verificar / Solución |
| --- | --- |
| Permiso de micrófono denegado | Asegúrate de que el navegador tenga permiso de micrófono para tu origen. |
| Fallo al cargar assets (`.onnx`, `.wasm`, `.mjs`, worklet) | Configura correctamente `baseAssetPath` / `onnxWASMBasePath` y verifica que los archivos realmente se estén sirviendo. |
| Problemas con runtimes más recientes de `onnxruntime-web` | Sirve también archivos `.mjs`, no solo `.wasm`. |
| Desarrollo local sobre origen inseguro | Las APIs de micrófono del navegador normalmente requieren contextos seguros (`https` o `localhost`). |
| Problemas de bundler en build | Usa la guía de empaquetado en [browser docs](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problemas de integración con Next.js | Usa los patrones de configuración mostrados en [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) y verifica las rutas de hosting de assets estáticos. |

## Patrocinio ❤️

Contribuye económicamente al proyecto, especialmente si tu producto comercial depende de este paquete. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Actualización importante sobre el soporte de node - Oct 2024 📢

Voy a reducir gradualmente el soporte para `ricky0123/vad-node`, el paquete de detección de actividad de voz para entornos node del lado del servidor. No planeo publicar más actualizaciones para el paquete node a partir de ahora. Tomé esta decisión por las siguientes razones:

- Mi caso de uso original para este proyecto fue la detección de actividad de voz en cliente. Añadí soporte para node porque alguien lo pidió y quise ayudar. Sin embargo, no tengo mucho tiempo para trabajar en este proyecto, y descontinuar `ricky0123/vad-node` me dará más tiempo para centrarme en `ricky0123/vad-web`.
- Es mucho más fácil para desarrolladores individuales crear soluciones personalizadas de detección de actividad de voz del lado del servidor que aprender a trabajar con onnxruntime-web, audio worklets y otras tecnologías para producir una solución del lado del cliente. Por ello, considero que `ricky0123/vad-web` aporta más valor a la comunidad.
- Compartir código entre los paquetes de navegador y node es bastante incómodo porque los entornos son diferentes en aspectos relevantes para ejecutar y usar el modelo de detección de actividad de voz.
- La mayoría de usuarios, según la [encuesta](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), está usando `ricky0123/vad-web` (posiblemente con `ricky0123/vad-react`).

## Hoja de Ruta 🛣️

Dirección actual (basada en el estado del repositorio y la nota del mantenedor anterior):

- Seguir centrando esfuerzos en APIs orientadas al navegador (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Mantener y mejorar docs/ejemplos para bundlers y frameworks
- Mejorar la documentación para contribuidores/desarrolladores y los flujos de `test-site`
- Añadir y mantener README traducidos en `i18n/`

## Contribuir 🤝

- Lee la guía de hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Abre issues o PRs en este repositorio: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Para contexto rápido del proyecto, revisa [`HACKING.md`](HACKING.md)

## Referencias 📚

1. Repositorio de Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Licencia 📄

- Licencia del proyecto: ISC (ver [LICENSE](LICENSE))
