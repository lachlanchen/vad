[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ Détection d'activité vocale pour JavaScript

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> Déclenchez des callbacks sur des segments audio contenant la parole de l’utilisateur en quelques lignes de code.

Ce package a pour objectif de fournir un détecteur d'activité vocale (VAD) précis et simple d'emploi, fonctionnant dans le navigateur. Grâce à ce package, vous pouvez demander la permission d'accès au micro à l'utilisateur, démarrer l'enregistrement audio, envoyer des segments audio contenant de la voix à votre serveur pour traitement, ou afficher une animation / un indicateur quand l'utilisateur parle. Notez que j'ai décidé de [suspendre le support Node](#mise-a-jour-importante-sur-le-support-de-node---oct-2024-) pour me concentrer sur le cas d’usage navigateur.

| En un coup d'œil | Détails |
| --- | --- |
| Packages principaux | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| Runtime principal | Navigateur (`WebAudio` + `getUserMedia`) |
| Docs | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Démo live | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

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
- [CI & contrôle qualité 🧱](#ci--controle-qualite-)
- [Dépannage 🩺](#depannage-)
- [Parrainage ❤️](#parrainage-)
- [❤️ Support](#-support)
- [Mise à jour importante sur le support de Node - Oct 2024 📢](#mise-a-jour-importante-sur-le-support-de-node---oct-2024-)
- [Feuille de route 🛣️](#feuille-de-route-)
- [Contribuer 🤝](#contribuer-)
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

- La documentation principale vit dans `./docs`.
- L'intégration des contributeurs commence ici : [guide de hacking développeur](https://docs.vad.ricky0123.com/developer-guide/hacking/). Les questions sont les bienvenues via les issues ou Discord.

En interne, ces packages exécutent [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#references) via [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (avec références historiques à ONNX Runtime Node.js depuis le support Node précédent). Merci à toute l’équipe pour l’avoir rendu possible.

Note sur l'état i18n : `i18n/` contient les versions traduites du README pour les langues listées en haut de ce fichier.

## Vue d'ensemble 🧭

Ce dépôt est un monorepo avec deux packages publiés principaux :

| Package | Objectif |
| --- | --- |
| `@ricky0123/vad-web` | API navigateur incluant `MicVAD`, `AudioNodeVAD` et `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper de hook React (`useMicVAD`) pour `vad-web` |

Le projet est conçu d'abord pour le navigateur et comprend :

- Callbacks de segmentation en temps réel depuis le micro (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Seuils d'algorithme configurables et contrôles temporels
- Support des modèles Silero legacy et v5
- Démo, tests et sources de docs dans ce dépôt

## Fonctionnalités ✨

- Pipeline VAD orienté navigateur, basé sur les modèles ONNX de Silero
- Fonctionne avec des balises `script`, des bundlers et React
- Contraintes de flux micro par défaut cohérentes
- Cycle de vie du flux personnalisable (`getStream`, `pauseStream`, `resumeStream`)
- Segmentation de la voix hors temps réel pour l'audio préenregistré via `NonRealTimeVAD`
- Chargement des assets/modèles configurable via `baseAssetPath` et `onnxWASMBasePath`
- Gestion de l'état de modèle legacy et v5 via les wrappers intégrés
- Exemples pour balises `script`, bundlers basés sur webpack, bundlers React et Next.js

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

- `packages/web/src/real-time-vad.ts` : orchestration VAD micro/audio-node en temps réel
- `packages/web/src/non-real-time-vad.ts` : segmentation asynchrone pour l'audio préenregistré
- `packages/web/src/frame-processor.ts` : logique de seuil et détection des limites de segments de parole
- `packages/react/src/index.ts` : cycle de vie du hook React et wrapper d'état de `useMicVAD`

## Matrice de compatibilité 🧩

| Composant | Environnement |
| --- | --- |
| `@ricky0123/vad-web` | Navigateurs modernes avec WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Applications React (`react` / `react-dom` >= 16.8.0) |
| Chaîne d'outils docs | Python 3.10 + Poetry (selon le workflow CI) |
| Runtime Node CI | Node 18 (selon les workflows du dépôt) |

Versions du snapshot du dépôt (`packages/*/package.json`) :

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prérequis ✅

- Usage navigateur : un navigateur moderne avec `MediaDevices.getUserMedia`
- Développement local : Node.js + npm workspaces
- Développement des docs : Python + Poetry (pour la génération MkDocs)

Référentiel recommandé en local selon la configuration CI :

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

Pour utiliser le VAD via une balise script dans le navigateur, incluez les balises suivantes :

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

### Utilisation hors temps réel (audio en lot)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuration ⚙️

Les options courantes entre les API incluent :

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

Voir les tableaux d'API complets dans la documentation : [Référence API](https://docs.vad.ricky0123.com/user-guide/api/) et [guide de l'algorithme](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Recette de configuration : auto-hébergement du modèle et des assets runtime

Si vous n'utilisez pas les valeurs CDN par défaut, assurez-vous que votre application sert :

- `silero_vad_legacy.onnx` et/ou `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- Les fichiers runtime `onnxruntime-web` (`.wasm`) et `.mjs` pour les builds runtime plus récents

Ensuite, configurez :

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

Commande d'exemple depuis `examples/bundler` :

```bash
npm run build && npm run start
```

La documentation pour empaqueter le détecteur d'activité vocale pour le navigateur ou l'utiliser dans des projets Node ou React est disponible sur [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Notes de développement 🛠️

Scripts de l'espace de travail racine :

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Ce qu'ils font :

- `npm run build` : compile tous les workspaces
- `npm run test` : exécute les tests des workspaces
- `npm run test:coverage` : couverture pour `packages/web`
- `npm run typecheck` : vérifie TypeScript dans les packages, test-site et tests
- `npm run format-check` : vérifie le formatage TS/TSX dans `packages`, `examples`, `test-site`
- `npm run dev` : surveille les sources des packages et du test-site, reconstruit et sert `test-site/dist`

Build de la documentation (MkDocs + Poetry) :

```bash
poetry install
poetry run mkdocs serve
```

Notes complémentaires :

- `./test-site/build.sh` copie les assets VAD/ONNX Runtime requis dans `test-site/dist` et `test-site/dist/subpath`
- `./scripts/dev.sh` utilise `nodemon` + `live-server` pour des cycles locaux de rebuild et serve sur le port `8080`
- `./check_vad_up_to_date.sh` est historique et référence `silero_vad.onnx` (alors que ce dépôt fournit `silero_vad_legacy.onnx` et `silero_vad_v5.onnx`)

## CI & contrôle qualité 🧱

Les workflows GitHub dans `.github/workflows/` couvrent :

- Test (`test.yml`)
- Vérification de type (`typecheck.yml`)
- Contrôle de format (`format-check.yml`)
- Build/déploiement docs (`docs.yml`)
- Flux de publication (`publish.yml`)

Ces workflows sont une source de vérité pratique pour les versions runtime/outils attendues et les contrôles de release.

## Dépannage 🩺

| Symptôme | Vérification / Correctif |
| --- | --- |
| Permission micro refusée | Vérifiez que le navigateur a la permission micro pour votre origine. |
| Échec de chargement des assets (`.onnx`, `.wasm`, `.mjs`, worklet) | Configurez correctement `baseAssetPath` / `onnxWASMBasePath` et vérifiez que les fichiers sont effectivement servis. |
| Problèmes avec des versions récentes de `onnxruntime-web` | Servez aussi les fichiers `.mjs`, pas seulement les `.wasm`. |
| Développement local en contexte non sécurisé | Les API micro du navigateur exigent généralement un contexte sécurisé (`https` ou `localhost`). |
| Problème de build avec le bundler | Utilisez les recommandations de bundling dans la [documentation navigateur](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problèmes d'intégration Next.js | Utilisez les patterns de configuration montrés dans [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) et vérifiez les chemins d'hébergement des assets statiques. |

## Parrainage ❤️

Contribuez financièrement au projet — surtout si votre produit commercial repose sur ce package. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Mise à jour importante sur le support de Node - Oct 2024 📢

Je vais progressivement arrêter le support de `ricky0123/vad-node`, le package de détection d'activité vocale pour les environnements Node côté serveur. Je ne prévois pas de publier de nouvelles mises à jour pour le package Node à l'avenir. J'ai pris cette décision pour les raisons suivantes :

- Mon cas d'usage initial pour ce projet était la détection d'activité vocale côté client. J'ai ajouté le support Node parce que quelqu'un l'a demandé et que je voulais être utile. Cependant, je n'ai pas beaucoup de temps pour travailler sur ce projet, et l'arrêt de `ricky0123/vad-node` me donnera plus de temps pour me concentrer sur `ricky0123/vad-web`.
- Il est beaucoup plus simple pour des développeurs individuels de créer des solutions de détection d'activité vocale côté serveur que pour d'autres développeurs d'apprendre à travailler avec onnxruntime-web, les audio worklets et autres technologies afin de produire une solution côté client. C'est pourquoi je pense que `ricky0123/vad-web` apporte plus de valeur à la communauté.
- Partager du code entre les packages navigateur et Node est assez contraignant, car les environnements diffèrent sur des aspects importants pour l'exécution et l'utilisation du modèle de détection d'activité vocale.
- Selon l'[enquête](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), la plupart des utilisateurs utilisent `ricky0123/vad-web` (éventuellement avec `ricky0123/vad-react`).

## Feuille de route 🛣️

Orientation actuelle (basée sur l'état du dépôt et la note de maintenance ci-dessus) :

- Continuer à privilégier les API navigateur (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Maintenir et améliorer les docs/exemples pour bundlers et frameworks
- Améliorer la documentation contributeur/développeur et les workflows du test-site
- Ajouter et maintenir des READMEs traduits sous `i18n/`

## Contribuer 🤝

- Lisez le guide de hacking : [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Ouvrez des issues ou des PR dans ce dépôt : [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Pour un contexte rapide sur le projet, consultez [`HACKING.md`](HACKING.md)

## Références 📚

1. Dépôt Silero VAD : [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## Licence 📄

- Licence du projet : ISC (voir [LICENSE](LICENSE))
