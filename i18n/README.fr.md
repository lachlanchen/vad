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
[![CI](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/test.yml?branch=main&style=flat-square&label=CI)](https://github.com/ricky0123/vad/actions/workflows/test.yml)
[![Typecheck](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/typecheck.yml?branch=main&style=flat-square&label=Typecheck)](https://github.com/ricky0123/vad/actions/workflows/typecheck.yml)
[![Docs](https://img.shields.io/github/actions/workflow/status/ricky0123/vad/docs.yml?branch=main&style=flat-square&label=Docs)](https://github.com/ricky0123/vad/actions/workflows/docs.yml)
[![GitHub stars](https://img.shields.io/github/stars/ricky0123/vad?style=flat-square&logo=github)](https://github.com/ricky0123/vad)
[![Node.js 18+](https://img.shields.io/badge/Node-18%2B-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)

> Exécute des callbacks sur des segments audio contenant la voix de l’utilisateur en quelques lignes de code.

Ce paquet a pour objectif de fournir un détecteur d’activité vocale (VAD) précis et convivial qui fonctionne directement dans le navigateur. Avec ce paquet, vous pouvez demander la permission du microphone, démarrer l’enregistrement audio, envoyer les segments contenant de la parole à votre serveur pour traitement, ou encore afficher une animation/indicateur lorsque l’utilisateur parle. Notez que j’ai choisi de [désactiver la prise en charge Node](#mise-à-jour-importante-sur-la-prise-en-charge-de-node---oct-2024-) afin de me concentrer sur l’usage navigateur.

| 🧭 En bref | Détails |
| --- | --- |
| 📦 Paquets principaux | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 Runtime principal | Navigateur (`WebAudio` + `getUserMedia`) |
| 📚 Docs | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 Démo en direct | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## Table des matières

- [Liens rapides 🔗](#liens-rapides-)
- [Aperçu 🧭](#aperçu-)
- [Fonctionnalités ✨](#fonctionnalités-)
- [Structure du projet 🗂️](#structure-du-projet-)
- [Matrice de compatibilité 🧩](#matrice-de-compatibilité-)
- [Prérequis ✅](#prérequis-)
- [Installation 📦](#installation-)
- [Utilisation 🚀](#utilisation-)
- [Configuration ⚙️](#configuration-)
- [Exemples 🧪](#exemples-)
- [Notes de développement 🛠️](#notes-de-développement-)
- [CI et contrôles qualité 🧱](#ci-et-contrôles-qualité-)
- [Dépannage 🩺](#dépannage-)
- [Sponsoring ❤️](#sponsoring-)
- [Feuille de route 🛣️](#feuille-de-route-)
- [Contribution 🤝](#contribution-)
- [Références 📚](#références-)
- [❤️ Support](#-support)
- [Mise à jour importante sur la prise en charge de Node - Oct 2024 📢](#mise-à-jour-importante-sur-la-prise-en-charge-de-node---oct-2024-)
- [License 📄](#license-)

## Liens rapides 🔗

| Ressource | Lien |
| --- | --- |
| Démo en direct | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| Documentation | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [Rejoindre la communauté](https://discord.gg/4WPeGEaSpF) |
| Sondage | [Partager votre cas d’usage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| Guide contributeur | [Guide de hacking développeur](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- La source de documentation se trouve dans `./docs`.
- L’onboarding des contributeurs commence ici : [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). Les questions sont les bienvenues via les issues ou Discord.

En interne, ces paquets utilisent [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#références-) via [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (avec des références historiques à ONNX Runtime Node.js depuis le support Node initial). Merci beaucoup à ces équipes pour avoir rendu cela possible.

Note sur l’i18n : le dossier `i18n/` inclut les README traduits pour les langues listées en haut de ce fichier.

## Aperçu 🧭

Ce dépôt est un monorepo avec deux paquets principaux publiés :

| Paquet | Objectif |
| --- | --- |
| `@ricky0123/vad-web` | API navigateur incluant `MicVAD`, `AudioNodeVAD` et `NonRealTimeVAD` |
| `@ricky0123/vad-react` | Wrapper React (`useMicVAD`) pour `vad-web` |

Le projet est orienté navigateur et inclut :

- Callbacks de segmentation de micro en temps réel (`onSpeechStart`, `onSpeechEnd`, `onVADMisfire`, etc.)
- Seuils algorithmiques et contrôles temporels configurables
- Support des modèles Silero legacy et v5
- Applications de démo/test et source de la documentation dans ce dépôt

## Fonctionnalités ✨

- Pipeline VAD first-browser basé sur les modèles Silero ONNX
- Compatible avec les balises script, bundlers et React
- Contraintes de flux micro par défaut raisonnables
- Cycle de vie du flux surchargeable (`getStream`, `pauseStream`, `resumeStream`)
- Segmentation asynchrone de la parole pour audio pré-enregistré via `NonRealTimeVAD`
- Chargement configurable des modèles/ressources via `baseAssetPath` et `onnxWASMBasePath`
- Prise en charge des états de modèle legacy et v5 via wrappers intégrés
- Exemples pour balises script, webpack bundlers, bundlers React et Next.js

## Structure du projet 🗂️

```text
.
├── README.md
├── docs/                     # Source MkDocs pour docs.vad.ricky0123.com
├── examples/                 # examples script-tag, bundler, react-bundler, nextjs
├── packages/
│   ├── web/                  # @ricky0123/vad-web
│   └── react/                # @ricky0123/vad-react
├── scripts/                  # outils dev
├── test-site/                # bac à sable interactif local
├── i18n/                     # fichiers README traduits
├── silero_vad_legacy.onnx
└── silero_vad_v5.onnx
```

Chemins détaillés :

- `packages/web/src/real-time-vad.ts` : orchestration VAD temps réel du microphone/audio-node
- `packages/web/src/non-real-time-vad.ts` : segmentation asynchrone de l’audio pré-enregistré
- `packages/web/src/frame-processor.ts` : logique de seuillage et détection des frontières de segments vocaux
- `packages/react/src/index.ts` : cycle de vie du hook React `useMicVAD` et wrapper d’état

## Matrice de compatibilité 🧩

| Composant | Environnement |
| --- | --- |
| `@ricky0123/vad-web` | Navigateurs modernes avec WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | Applications React (`react` / `react-dom` >= 16.8.0) |
| Outils de docs | Python 3.10 + Poetry (selon les workflows CI) |
| Runtime Node CI | Node 18 (selon les workflows du dépôt) |

Versions de snapshot des paquets (`packages/*/package.json`) :

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## Prérequis ✅

- Usage navigateur : un navigateur moderne avec `MediaDevices.getUserMedia`
- Développement local : Node.js + npm workspaces
- Développement docs : Python + Poetry (pour la génération MkDocs)

Environnement local recommandé selon la configuration CI :

- Node.js 18.x
- Python 3.10.x

## Installation 📦

Installer le paquet navigateur :

```bash
npm i @ricky0123/vad-web
```

Installer le wrapper React :

```bash
npm i @ricky0123/vad-react
```

Installer les dépendances du monorepo (pour les contributeurs) :

```bash
npm install
```

## Utilisation 🚀

### Démarrage rapide (balises script)

Pour utiliser le VAD via une balise script dans le navigateur, ajoutez les balises suivantes :

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

### Utilisation du paquet navigateur (import de module)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### Utilisation React

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

### Utilisation non temps réel (audio par lot)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## Configuration ⚙️

Les options communes à toutes les API incluent :

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

Consultez les tableaux API complets dans la documentation : [Référence API](https://docs.vad.ricky0123.com/user-guide/api/) et [guide de l’algorithme](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### Recette de configuration : auto-hébergement du modèle et des assets runtime

Quand vous n’utilisez pas les valeurs CDN par défaut, assurez-vous que votre application serve :

- `silero_vad_legacy.onnx` et/ou `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- les fichiers runtime `onnxruntime-web` (`.wasm`; et `.mjs` pour les builds runtime plus récents)

Puis configurez :

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

- `examples/script-tags` : configuration de base via balises script
- `examples/bundler` : webpack + `@ricky0123/vad-web`
- `examples/react-bundler` : webpack + `@ricky0123/vad-react`
- `examples/nextjs` : exemple d’intégration Next.js

Commande d’exemple depuis `examples/bundler` :

```bash
npm run build && npm run start
```

La documentation pour empaqueter le détecteur d’activité vocale pour navigateur ou l’utiliser dans des projets Node ou React se trouve sur [vad.ricky0123.com](https://www.vad.ricky0123.com).

## Notes de développement 🛠️

Scripts de la racine du workspace :

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

Ce qu’ils font :

- `npm run build` : compile tous les workspaces
- `npm run test` : exécute les tests des workspaces
- `npm run test:coverage` : couverture pour `packages/web`
- `npm run typecheck` : vérifie TypeScript dans packages, test-site et tests
- `npm run format-check` : vérifie le formatage TS/TSX dans `packages`, `examples`, `test-site`
- `npm run dev` : surveille les sources de package et de test-site, reconstruit et sert `test-site/dist`

Build de la documentation (MkDocs + Poetry) :

```bash
poetry install
poetry run mkdocs serve
```

Notes supplémentaires :

- `./test-site/build.sh` copie les assets VAD/ONNX Runtime nécessaires dans `test-site/dist` et `test-site/dist/subpath`
- `./scripts/dev.sh` utilise `nodemon` + `live-server` pour des boucles locales rebuild-and-serve sur le port `8080`
- `./check_vad_up_to_date.sh` est historique et fait référence à `silero_vad.onnx` (alors que ce dépôt inclut `silero_vad_legacy.onnx` et `silero_vad_v5.onnx`)

## CI et contrôles qualité 🧱

Les workflows GitHub dans `.github/workflows/` couvrent :

- Test (`test.yml`)
- Vérification de type (`typecheck.yml`)
- Formatage (`format-check.yml`)
- Build/déploiement de docs (`docs.yml`)
- Workflow de publication (`publish.yml`)

Ces workflows sont une source pratique de vérité sur les versions runtime/outil attendues et les contrôles de release.

## Dépannage 🩺

| Symptom | Vérification / Correctif |
| --- | --- |
| Permission micro refusée | Assurez-vous que le navigateur a bien l’autorisation micro pour votre origine. |
| Échec du chargement des assets (`.onnx`, `.wasm`, `.mjs`, worklet) | Réglez correctement `baseAssetPath` / `onnxWASMBasePath` et vérifiez que les fichiers sont vraiment servis. |
| Problèmes sur les versions plus récentes de `onnxruntime-web` | Servez aussi les fichiers `.mjs`, pas uniquement les `.wasm`. |
| Dév local sur origine non sécurisée | Les APIs micro du navigateur nécessitent généralement un contexte sécurisé (`https` ou `localhost`). |
| Problèmes de build du bundler | Utilisez les recommandations de bundling dans la [documentation navigateur](https://docs.vad.ricky0123.com/user-guide/browser/). |
| Problèmes d’intégration Next.js | Utilisez les patterns de configuration montrés dans [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) et vérifiez les chemins d’hébergement des assets statiques. |

## Sponsoring ❤️

Merci de contribuer financièrement au projet — surtout si votre produit commercial repose sur ce paquet. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## Mise à jour importante sur la prise en charge de Node - Oct 2024 📢

Je vais progressivement arrêter la prise en charge de `ricky0123/vad-node`, le paquet de détection d’activité vocale pour les environnements Node côté serveur. Je ne prévois pas de publier de nouvelles mises à jour du paquet Node à partir de maintenant. Cette décision est fondée sur les raisons suivantes :

- Mon cas d’usage initial pour ce projet était la détection d’activité vocale côté client. J’ai ajouté la prise en charge Node parce qu’on me l’a demandée et que je voulais être utile. Cependant, je n’ai pas beaucoup de temps à consacrer à ce projet, et interrompre `ricky0123/vad-node` me laisse davantage de temps pour me concentrer sur `ricky0123/vad-web`.
- Il est beaucoup plus simple pour un développeur de créer sa propre solution de détection d’activité vocale côté serveur que d’apprendre à utiliser onnxruntime-web, les audio worklets et d’autres technologies pour produire une solution côté client. Je considère donc `ricky0123/vad-web` comme plus utile pour la communauté.
- Le partage de code entre les paquets navigateur et Node reste assez pénible car les environnements diffèrent sur des points importants pour l’exécution et l’usage du modèle VAD.
- Selon le [sondage](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv), la plupart des utilisateurs utilisent `ricky0123/vad-web` (potentiellement avec `ricky0123/vad-react`).

## Feuille de route 🛣️

Direction actuelle (selon l’état du dépôt et la note du mainteneur ci-dessus) :

- Continuer à se concentrer sur des API orientées navigateur (`@ricky0123/vad-web`, `@ricky0123/vad-react`)
- Maintenir et améliorer docs/exemples pour bundlers et frameworks
- Améliorer la documentation pour contributeurs/développeurs et les flux de travail du test-site
- Ajouter et maintenir les README traduits dans `i18n/`

## Contribution 🤝

- Consultez le guide de hacking : [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- Ouvrez des issues ou PRs dans ce dépôt : [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- Pour un contexte rapide du projet, voyez [`HACKING.md`](HACKING.md)

## Références 📚

1. Dépôt Silero VAD : [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## License 📄

- Licence du projet : ISC (voir [LICENSE](LICENSE))
