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

> Ejecuta callbacks en segmentos de audio con voz del usuario en pocas líneas de código.

Este paquete busca ofrecer un detector de actividad de voz (VAD) preciso y fácil de usar que se ejecute en el navegador. Al usar este paquete, puedes pedir permisos de micrófono, comenzar a grabar audio, enviar segmentos con voz al servidor para procesarlos o mostrar una animación o indicador cuando el usuario esté hablando. Ten en cuenta que he decidido [dar de baja el soporte de Node](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-) para centrarme en el caso de uso del navegador.

| De un vistazo | Detalles |
| --- | --- |
| Paquetes principales | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Entorno de ejecución principal | Navegador (`WebAudio` + `getUserMedia`) |
| Documentación | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Demo en vivo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Tabla de contenidos

- [Enlaces rápidos 🔗](#enlaces-r%C3%A1pidos-)
- [Vista general 🧭](#vista-general-)
- [Características ✨](#caracteristicas-)
- [Estructura del proyecto 🗂️](#estructura-del-proyecto-)
- [Matriz de compatibilidad 🧩](#matriz-de-compatibilidad-)
- [Requisitos previos ✅](#requisitos-previos-)
- [Instalación 📦](#instalacion-)
- [Uso 🚀](#uso-)
- [Configuración ⚙️](#configuracion-)
- [Ejemplos 🧪](#ejemplos-)
- [Notas de desarrollo 🛠️](#notas-de-desarrollo-)
- [CI y puertas de calidad 🧱](#ci-y-puertas-de-calidad-)
- [Resolución de problemas 🩺](#resolucion-de-problemas-)
- [Patrocinio ❤️](#patrocinio-)
- [❤️ Support](#-support)
- [Actualización importante sobre el soporte de Node - Oct 2024 📢](#actualizacion-importante-sobre-el-soporte-de-node---oct-2024-)
- [Hoja de ruta 🛣️](#hoja-de-ruta-)
- [Contribuir 🤝](#contribuir-)
- [Referencias 📚](#referencias-)
- [Licencia 📄](#licencia-)

## Enlaces rápidos 🔗

| Recurso | Enlace |
| --- | --- |
| Demo en vivo | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentación | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Únete a la comunidad](https://discord.gg/4WPeGEaSpF) |
| Encuesta | [Comparte tu caso de uso](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Guía para contribuir | [Guía de desarrollo](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- La fuente de la documentación está en `./docs`.
- La incorporación para contribuidores empieza aquí: [guía de desarrollo](https://docs.vad.ricky0123.com/developer-guide/hacking/). Puedes hacer preguntas en issues o en Discord.

Estos paquetes ejecutan internamente [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#referencias-) usando [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (con referencias históricas a ONNX Runtime Node.js de la etapa anterior con soporte para Node). Gracias a quienes hicieron esto posible.

Nota de estado de i18n: `i18n/` incluye archivos README traducidos para los idiomas enlazados en la parte superior de este archivo.

## Vista general 🧭

Este repositorio es un monorepo con dos paquetes principales publicados:

| Paquete | Propósito |
| --- | --- |
| `@ricky0123/vad-web` | APIs de navegador que incluyen `MicVAD`, `AudioNodeVAD` y `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Envoltorio con hooks de React (`useMicVAD`) para `vad-web` |

El proyecto está orientado al navegador e incluye:

- Callbacks de segmentación de micrófono en tiempo real (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Umbrales y controles de tiempo configurables del algoritmo
- Compatibilidad con modelos Silero legacy y v5
- Aplicaciones de demostración/pruebas y fuentes de la documentación en este repositorio

## Características ✨

- Pipeline VAD orientada al navegador impulsada por modelos Silero ONNX
- Funciona con etiquetas `<script>`, bundlers y React
- Restricciones de stream de micrófono razonables por defecto
- Ciclo de vida del stream reemplazable (`getStream`, `pauseStream`, `resumeStream`)
- Segmentación de voz fuera de tiempo real para audio pregrabado mediante `NonRealTimeVAD`
- Carga configurable de modelo/recursos vía `baseAssetPath` y `onnxWASMBasePath`
- Compatible con la gestión de estado de modelos legacy y v5 mediante wrappers integrados
- Incluye ejemplos para etiquetas `<script>`, webpack-based bundlers, bundlers de React y Next.js

## Estructura del proyecto 🗂️

```text
.
├── README.md
├── docs/                     # Fuentes MkDocs de docs.vad.ricky0123.com
├── examples/                 # ejemplos script-tag, bundler, react-bundler, nextjs
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # herramientas de desarrollo
├── test-site/                # playground interactivo local
├── i18n/                     # archivos README traducidos
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

Rutas más detalladas:

- `packages/web/src/real-time-vad.ts`: orquestación de VAD en tiempo real para micrófono/audio-node
- `packages/web/src/non-real-time-vad.ts`: segmentación asíncrona para audio pregrabado
- `packages/web/src/frame-processor.ts`: lógica de umbrales y límites de los segmentos de voz
- `packages/react/src/index.ts`: ciclo de vida y wrapper de estado del hook de React `useMicVAD`

## Matriz de compatibilidad 🧩

| Componente | Entorno |
| --- | --- |
| `@ricky0123/vad-web` | Navegadores modernos con WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Apps React (`react` / `react-dom` >= 16.8.0) |
| Cadena de herramientas de docs | Python 3.10 + Poetry (según flujo de CI) |
| Runtime de Node en CI | Node 18 (según workflows del repositorio) |

Versiones de paquetes en la instantánea del repositorio (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Requisitos previos ✅

- Uso en navegador: un navegador moderno con `MediaDevices.getUserMedia`
- Desarrollo local: Node.js + npm workspaces
- Desarrollo de documentación: Python + Poetry (para la compilación de MkDocs)

Línea base recomendada localmente según la configuración de CI:

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

Instala las dependencias del monorepo (para colaboradores):

```bash
npm install
```

## Uso 🚀

### Inicio rápido (script tags)

Para usar VAD con una etiqueta script en el navegador, incluye lo siguiente:

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

### Uso de React

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

### Uso fuera de tiempo real (audio por lotes)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuración ⚙️

Opciones comunes en las APIs:

- `positiveSpeechThreshold` (valor predeterminado alrededor de `0.3` en APIs en tiempo real)
- `negativeSpeechThreshold` (valor predeterminado alrededor de `0.25` en APIs en tiempo real)
- `redemptionMs` (valor predeterminado alrededor de `1400` en APIs en tiempo real)
- `preSpeechPadMs` (valor predeterminado alrededor de `800` en APIs en tiempo real)
- `minSpeechMs` (valor predeterminado alrededor de `400` en APIs en tiempo real)

Las APIs en tiempo real (`MicVAD`, `useMicVAD`) también soportan:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` o `"v5"`)
- `baseAssetPath` y `onnxWASMBasePath`
- `workletOptions`

Consulta las tablas completas de la API en la documentación: [Referencia de API](https://docs.vad.ricky0123.com/user-guide/api/) y [guía del algoritmo](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Receta de configuración: autoalojar modelo y recursos de runtime

Cuando no uses los valores predeterminados de CDN, asegúrate de que tu app sirva:

- `silero_vad_legacy.onnx` y/o `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- archivos de runtime de `onnxruntime-web` (`.wasm`; y `.mjs` para builds de runtime más recientes)

Luego configura:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // manejar segmento de audio
  },
})
```

## Ejemplos 🧪

Ejemplos del repositorio:

- `examples/script-tags`: configuración básica con etiqueta script
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: ejemplo de integración con Next.js

Comando de ejemplo de `examples/bundler`:

```bash
npm run build && npm run start
```

La documentación para empaquetar el detector de actividad de voz para navegador o usarlo en proyectos Node o React está en [vad.ricky0123.com](https://www.vad.ricky0123.com).

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

Qué hace cada uno:

- `npm run build`: compila todos los workspaces
- `npm run test`: ejecuta pruebas de los workspaces
- `npm run test:coverage`: cobertura para `packages/web`
- `npm run typecheck`: comprueba TypeScript en paquetes, test-site y tests
- `npm run format-check`: valida formato de TS/TSX en `packages`, `examples`, `test-site`
- `npm run dev`: vigila fuentes de paquetes y de test-site, recompila y sirve `test-site/dist`

Compilación de documentación (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

Notas adicionales:

- `./test-site/build.sh` copia los recursos VAD/ONNX Runtime requeridos en `test-site/dist` y `test-site/dist/subpath`
- `./scripts/dev.sh` usa `nodemon` + `live-server` para bucles locales de rebuild-and-serve en el puerto `8080`
- `./check_vad_up_to_date.sh` es histórico y hace referencia a `silero_vad.onnx` (mientras que este repositorio distribuye `silero_vad_legacy.onnx` y `silero_vad_v5.onnx`)

## CI y puertas de calidad 🧱

Los flujos de GitHub en `.github/workflows/` cubren:

- Pruebas (`test.yml`)
- Chequeo de tipos (`typecheck.yml`)
- Revisión de formato (`format-check.yml`)
- Build y despliegue de docs (`docs.yml`)
- Flujo de publicación (`publish.yml`)

Estos workflows son una fuente práctica de verdad sobre las versiones esperadas de runtime/herramientas y comprobaciones de liberación.

## Resolución de problemas 🩺

| Síntoma | Verificación / Solución |
| --- | --- |
| Permiso del micrófono denegado | Asegúrate de que el navegador tenga permiso de micrófono para tu origen. |
| Error al cargar recursos (`.onnx`, `.wasm`, `.mjs`, worklet) | Configura correctamente `baseAssetPath` / `onnxWASMBasePath` y verifica que los archivos se estén sirviendo realmente. |
| Problemas con runtimes más recientes de `onnxruntime-web` | Sirve también archivos `.mjs`, no solo `.wasm`. |
| Desarrollo local en origen inseguro | Las APIs de micrófono del navegador suelen requerir contextos seguros (`https` o `localhost`). |
| Problemas con bundlers en build | Usa la guía de empaquetado en la [documentación del navegador](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problemas de integración con Next.js | Usa los patrones de configuración mostrados en [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) y verifica las rutas de hosting de recursos estáticos. |

## Patrocinio ❤️

Contribuye económicamente al proyecto, especialmente si tu producto comercial depende de este paquete. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Actualización importante sobre el soporte de Node - Oct 2024 📢

Voy a dar de baja progresivamente el soporte para `ricky0123/vad-node`, el paquete de detección de actividad de voz para entornos de Node del lado del servidor. No planeo publicar más actualizaciones del paquete Node a partir de ahora. Tomé esta decisión por estas razones:

- El caso de uso original de este proyecto fue la detección de actividad de voz en cliente. Agregué soporte de Node porque alguien lo pidió y quería ser útil. Sin embargo, no tengo mucho tiempo para trabajar en este proyecto, y reducir `ricky0123/vad-node` me dará más tiempo para centrarme en `ricky0123/vad-web`.
- Es mucho más fácil para desarrolladores individuales crear soluciones personalizadas de VAD del lado del servidor que aprender a trabajar con onnxruntime-web, audio worklets y otras tecnologías para construir una solución del lado del cliente. Por eso veo que `ricky0123/vad-web` aporta más valor a la comunidad.
- Compartir código entre los paquetes de navegador y de Node es bastante incómodo porque los entornos difieren en aspectos relevantes para ejecutar y usar el modelo de detección de actividad de voz.
- La mayoría de usuarios, según la [encuesta](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), usa `ricky0123/vad-web` (probablemente con `ricky0123/vad-react`).

## Hoja de ruta 🛣️

Dirección actual (basada en el estado del repositorio y la nota anterior del mantenedor):

- Seguir centrando el desarrollo en APIs orientadas al navegador (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Mantener y mejorar docs y ejemplos para bundlers y frameworks
- Mejorar la documentación para colaboradores/desarrolladores y los flujos de `test-site`
- Añadir y mantener README traducidos en `i18n/`

## Contribuir 🤝

- Lee la guía de hacking: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Abre issues o PRs en este repositorio: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Para tener contexto rápido del proyecto, consulta [`HACKING.md`](HACKING.md)

## Referencias 📚

1. Repositorio de Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Licencia 📄

- Licencia del proyecto: ISC (ver [LICENSE](LICENSE))
