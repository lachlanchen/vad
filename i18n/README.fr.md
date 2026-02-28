[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


# Détection d'activité vocale pour JavaScript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Exécutez des callbacks sur des segments audio contenant de la parole utilisateur en quelques lignes de code.

Ce package vise à fournir un détecteur d'activité vocale (VAD) précis et facile à utiliser, exécuté dans le navigateur. En utilisant ce package, vous pouvez demander les autorisations microphone à l'utilisateur, démarrer l'enregistrement audio, envoyer à votre serveur des segments audio contenant de la parole pour traitement, ou afficher une animation/indicateur quand l'utilisateur parle. Notez que j'ai décidé d'[arrêter le support de Node](#mise-a-jour-importante-sur-le-support-node---oct-2024-) afin de me concentrer sur le cas d'usage navigateur.

## Table des matières

- [Liens rapides 🔗](#liens-rapides-)
- [Vue d'ensemble 🧭](#vue-densemble-)
- [Fonctionnalités ✨](#fonctionnalites-)
- [Structure du projet 🗂️](#structure-du-projet-)
- [Matrice de compatibilité 🧩](#matrice-de-compatibilite-)
- [Prérequis ✅](#prerequis-)
- [Installation 📦](#installation-)
- [Utilisation 🚀](#utilisation-)
- [Configuration ⚙️](#configuration-)
- [Exemples 🧪](#exemples-)
- [Notes de développement 🛠️](#notes-de-developpement-)
- [CI et portes de qualité 🧱](#ci-et-portes-de-qualite-)
- [Dépannage 🩺](#depannage-)
- [Sponsoring ❤️](#sponsoring-)
- [Mise à jour importante sur le support de Node - oct 2024 📢](#mise-a-jour-importante-sur-le-support-node---oct-2024-)
- [Feuille de route 🛣️](#feuille-de-route-)
- [Contribution 🤝](#contribution-)
- [Références 📚](#references-)
- [Licence 📄](#licence-)

## Liens rapides 🔗

| Ressource | Lien |
| --- | --- |
| Démo en direct | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Rejoindre la communauté](https://discord.gg/4WPeGEaSpF) |
| Enquête | [Partagez votre cas d'usage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Guide de contribution | [Guide de hacking développeur](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- Parcourez la documentation, dont le code source se trouve dans le répertoire `./docs`.
- Si vous souhaitez contribuer, j'ai commencé à rédiger de la documentation sur la façon de démarrer le hacking de ces packages [ici](https://docs.vad.ricky0123.com/developer-guide/hacking/). Si vous avez des questions, vous pouvez ouvrir une issue ici ou laisser un message sur Discord.

Sous le capot, ces packages exécutent [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references) avec [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) / [ONNX Runtime Node.js](https://github.com/microsoft/onnxruntime/tree/main/js/node). Un grand merci à ces équipes d'avoir rendu cela possible.

Note sur l'état de l'i18n : `i18n/` existe et inclut plusieurs fichiers README traduits. Le sélecteur de langue ci-dessus contient également des liens vers des traductions prévues/de substitution (`README.de.md`, `README.ru.md`) qui peuvent ne pas être présentes dans cet instantané du dépôt.

## Vue d'ensemble 🧭

Ce dépôt est un monorepo avec deux packages publiés principaux :

| Package | Objectif |
| --- | --- |
| `@ricky0123/vad-web` | API navigateur incluant `MicVAD`, `AudioNodeVAD` et `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper de hook React (`useMicVAD`) pour `vad-web` |

Le projet est orienté navigateur en priorité et inclut :

- Callbacks de segmentation micro en temps réel (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Seuils algorithmiques configurables et contrôles de timing
- Support des modèles Silero legacy et v5
- Applications de démo/test et sources du site de documentation dans ce dépôt

## Fonctionnalités ✨

- Pipeline VAD orienté navigateur, propulsé par les modèles ONNX de Silero
- Fonctionne avec les balises `script`, les bundlers et React
- Contraintes de flux microphone par défaut raisonnables
- Cycle de vie du flux surchargeable (`getStream`, `pauseStream`, `resumeStream`)
- Segmentation de parole hors temps réel pour audio préenregistré via `NonRealTimeVAD`
- Chargement configurable des modèles/assets via `baseAssetPath` et `onnxWASMBasePath`
- Prend en charge la gestion d'état des modèles legacy et v5 via des wrappers intégrés
- Inclut des exemples pour balises `script`, bundlers basés sur webpack, bundlers React et Next.js

## Structure du projet 🗂️

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

Chemins plus détaillés :

- `packages/web/src/real-time-vad.ts` : orchestration VAD en temps réel pour microphone/audio-node
- `packages/web/src/non-real-time-vad.ts` : segmentation asynchrone pour audio préenregistré
- `packages/web/src/frame-processor.ts` : logique de seuils et de frontières de segments de parole
- `packages/react/src/index.ts` : cycle de vie et wrapper d'état du hook React `useMicVAD`

## Matrice de compatibilité 🧩

| Composant | Environnement |
| --- | --- |
| `@ricky0123/vad-web` | Navigateurs modernes avec WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Applications React (`react` / `react-dom` >= 16.8.0) |
| Toolchain docs | Python 3.10 + Poetry (selon le workflow CI) |
| Runtime Node CI | Node 18 (selon les workflows du dépôt) |

Note d'hypothèse : les exemples et la documentation sont cohérents avec les versions de package actuelles dans cet instantané du dépôt (`@ricky0123/vad-web@0.0.27`, `@ricky0123/vad-react@0.0.33`).

## Prérequis ✅

- Utilisation navigateur : un navigateur moderne avec `MediaDevices.getUserMedia`
- Développement local : Node.js + npm workspaces
- Développement de la documentation : Python + Poetry (pour le build MkDocs)

Base locale recommandée selon la configuration CI :

- Node.js 18.x
- Python 3.10.x

## Installation 📦

Installez le package navigateur :

```bash
npm i @ricky0123/vad-web
```

Installez le wrapper React :

```bash
npm i @ricky0123/vad-react
```

Installez les dépendances du monorepo (pour les contributeurs) :

```bash
npm install
```

## Utilisation 🚀

### Démarrage rapide (balises script)

Pour utiliser le VAD via une balise script dans le navigateur, incluez les balises script suivantes :

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

### Utilisation du package navigateur (import de module)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### Utilisation avec React

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

### Utilisation hors temps réel (audio par lot)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuration ⚙️

Les options communes entre les API incluent :

- `positiveSpeechThreshold` (par défaut autour de `0.3` dans les API temps réel)
- `negativeSpeechThreshold` (par défaut autour de `0.25` dans les API temps réel)
- `redemptionMs` (par défaut autour de `1400` dans les API temps réel)
- `preSpeechPadMs` (par défaut autour de `800` dans les API temps réel)
- `minSpeechMs` (par défaut autour de `400` dans les API temps réel)

Les API temps réel (`MicVAD`, `useMicVAD`) prennent aussi en charge :

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` ou `"v5"`)
- `baseAssetPath` et `onnxWASMBasePath`
- `workletOptions`

Consultez les tables API complètes dans la documentation : [Référence API](https://docs.vad.ricky0123.com/user-guide/api/) et [guide de l'algorithme](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Recette de configuration : auto-hébergement du modèle et des assets runtime

Lorsque vous n'utilisez pas les valeurs CDN par défaut, assurez-vous que votre application sert :

- `silero_vad_legacy.onnx` et/ou `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Fichiers runtime `onnxruntime-web` (`.wasm` et `.mjs` pour les builds runtime plus récents)

Configurez ensuite :

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## Exemples 🧪

Exemples du dépôt :

- `examples/script-tags` : configuration de base avec balises script
- `examples/bundler` : webpack + `@ricky0123/vad-web`
- `examples/react-bundler` : webpack + `@ricky0123/vad-react`
- `examples/nextjs` : exemple d'intégration Next.js

Exemple de commande depuis `examples/bundler` :

```bash
npm run build && npm run start
```

La documentation pour bundler le détecteur d'activité vocale pour le navigateur, ou l'utiliser dans des projets node ou React, est disponible sur [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Notes de développement 🛠️

Scripts du workspace racine :

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Ce qu'ils font :

- `npm run build` : build tous les workspaces
- `npm run test` : lance les tests des workspaces
- `npm run test:coverage` : couverture pour `packages/web`
- `npm run typecheck` : vérifie TypeScript dans les packages, test-site et tests
- `npm run format-check` : vérifie le formatage TS/TSX sous `packages`, `examples`, `test-site`
- `npm run dev` : surveille les sources des packages et de test-site, rebuild et sert `test-site/dist`

Build de la documentation (MkDocs + Poetry) :

```bash
poetry install
poetry run mkdocs serve
```

Notes supplémentaires :

- `./test-site/build.sh` copie les assets VAD/ONNX Runtime requis dans `test-site/dist` et `test-site/dist/subpath`
- `./scripts/dev.sh` utilise `nodemon` + `live-server` pour les boucles locales rebuild-and-serve sur le port `8080`
- `./check_vad_up_to_date.sh` est historique et référence `silero_vad.onnx` (alors que ce dépôt inclut `silero_vad_legacy.onnx` et `silero_vad_v5.onnx`)

## CI et portes de qualité 🧱

Les workflows GitHub dans `.github/workflows/` couvrent :

- Test (`test.yml`)
- Typecheck (`typecheck.yml`)
- Formatage (`format-check.yml`)
- Build/déploiement de la doc (`docs.yml`)
- Flux de publication (`publish.yml`)

Ces workflows constituent une source de vérité pratique pour les versions runtime/outils attendues et les vérifications de release.

## Dépannage 🩺

| Symptôme | Vérification / Correctif |
| --- | --- |
| Permission micro refusée | Vérifiez que le navigateur a la permission microphone pour votre origine. |
| Échec de chargement des assets (`.onnx`, `.wasm`, `.mjs`, worklet) | Définissez correctement `baseAssetPath` / `onnxWASMBasePath` et vérifiez que les fichiers sont bien servis. |
| Problèmes avec une version plus récente de `onnxruntime-web` | Servez aussi les fichiers `.mjs`, pas seulement `.wasm`. |
| Développement local sur une origine non sécurisée | Les API micro du navigateur exigent généralement des contextes sécurisés (`https` ou `localhost`). |
| Problèmes de bundler au build | Utilisez les recommandations de bundling dans la [documentation navigateur](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problèmes d'intégration Next.js | Utilisez les patterns de configuration montrés dans [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) et vérifiez les chemins d'hébergement des assets statiques. |

## Sponsoring ❤️

Merci de contribuer financièrement au projet, en particulier si votre produit commercial dépend de ce package. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Mise à jour importante sur le support de Node - oct 2024 📢

Je vais réduire progressivement le support de `ricky0123/vad-node`, le package de détection d'activité vocale pour les environnements node côté serveur. Je ne prévois pas de publier de nouvelles mises à jour pour le package node à partir de maintenant. J'ai pris cette décision pour les raisons suivantes :

- Mon cas d'usage d'origine pour ce projet était la détection d'activité vocale côté client. J'ai ajouté le support node parce que quelqu'un l'a demandé et que je voulais aider. Cependant, j'ai peu de temps pour travailler sur ce projet, et la dépréciation de `ricky0123/vad-node` me donnera plus de temps pour me concentrer sur `ricky0123/vad-web`.
- Il est beaucoup plus facile pour des développeurs individuels de créer des solutions serveur personnalisées de détection d'activité vocale qu'il ne l'est pour les développeurs d'apprendre à travailler avec onnxruntime-web, les audio worklets et d'autres technologies afin de produire une solution côté client. Je considère donc que `ricky0123/vad-web` apporte davantage de valeur à la communauté.
- Le partage de code entre les packages navigateur et node est assez maladroit, car les environnements sont différents de manière importante pour exécuter et utiliser le modèle de détection d'activité vocale.
- D'après l'[enquête](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), la plupart des utilisateurs utilisent `ricky0123/vad-web` (éventuellement avec `ricky0123/vad-react`).

## Feuille de route 🛣️

Direction actuelle (d'après l'état du dépôt et la note du mainteneur ci-dessus) :

- Continuer à se concentrer sur les API orientées navigateur (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Maintenir et améliorer la documentation/les exemples pour les bundlers et frameworks
- Améliorer la documentation contributeur/développeur et les workflows test-site
- Ajouter et maintenir des README traduits sous `i18n/`

## Contribution 🤝

- Lisez le guide de hacking : [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Ouvrez des issues ou des PR sur ce dépôt : [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Pour un contexte projet rapide, consultez [`HACKING.md`](HACKING.md)

## Références 📚

1. Dépôt Silero VAD : [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Licence 📄

- Licence du projet : ISC (voir [LICENSE](LICENSE))
