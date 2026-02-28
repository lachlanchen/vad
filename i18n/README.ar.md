[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# 🎙️ كشف النشاط الصوتي في JavaScript

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

> نفّذ دوالّ ردّ الاتصال على مقاطع صوتية تحتوي على كلام المستخدم في بضع أسطر من الكود.

تهدف هذه الحزمة إلى تقديم كاشف نشاط صوتي (VAD) دقيق وسهل الاستخدام يعمل في المتصفح. باستخدام هذه الحزمة، يمكنك طلب إذن الميكروفون من المستخدم، وبدء تسجيل الصوت، وإرسال مقاطع الصوت التي تحتوي على كلام إلى خادمك للمعالجة، أو عرض رسوم متحركة أو مؤشر معيّن عندما يتحدث المستخدم. لاحظ أنني قرّرت [إيقاف دعم Node](#تحديث-مهم-حول-دعم-node---أكتوبر-2024-) للتركيز على حالة استخدام المتصفح.

| 🧭 لمحة سريعة | التفاصيل |
| --- | --- |
| 📦 الحزم الأساسية | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| 🧪 البيئة الأساسية | المتصفح (`WebAudio` + `getUserMedia`) |
| 📚 التوثيق | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| 🌐 عرض مباشر | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## جدول المحتويات

- [روابط سريعة 🔗](#روابط-سريعة-)
- [نظرة عامة 🧭](#نظرة-عامة-)
- [المميزات ✨](#المميزات-)
- [هيكل المشروع 🗂️](#هيكل-المشروع-)
- [مصفوفة التوافق 🧩](#مصفوفة-التوافق-)
- [المتطلبات المسبقة ✅](#المتطلبات-المسبقة-)
- [التثبيت 📦](#التثبيت-)
- [الاستخدام 🚀](#الاستخدام-)
- [الإعدادات ⚙️](#الإعدادات-)
- [أمثلة 🧪](#أمثلة-)
- [ملاحظات التطوير 🛠️](#ملاحظات-التطوير-)
- [بوابات الجودة & CI 🧱](#ci--quality-gates-)
- [استكشاف الأخطاء وإصلاحها 🩺](#استكشاف-الأخطاء-وإصلاحها-)
- [الرعاية المالية ❤️](#الرعاية-المالية-)
- [❤️ Support](#-support)
- [تحديث مهم حول دعم node - أكتوبر 2024 📢](#تحديث-مهم-حول-دعم-node---أكتوبر-2024-)
- [خطة الطريق 🛣️](#خطة-الطريق-)
- [المساهمة 🤝](#المساهمة-)
- [المراجع 📚](#المراجع-)
- [الترخيص 📄](#الترخيص-)

## روابط سريعة 🔗

| المورد | الرابط |
| --- | --- |
| العرض المباشر | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| التوثيق | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [انضم إلى المجتمع](https://discord.gg/4WPeGEaSpF) |
| الاستبيان | [شارك حالة استخدامك](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| دليل المساهمة | [مرشد المطورين](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- توجد مصادر التوثيق في `./docs`.
- يبدأ اندماج المساهمين من هنا: [developer hacking guide](https://docs.vad.ricky0123.com/developer-guide/hacking/). الأسئلة مرحّب بها عبر القضايا (issues) أو Discord.

تعمل هذه الحزم باستخدام [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#المراجع-) عبر [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (مع مراجع تاريخية لـ ONNX Runtime Node.js من فترة دعم Node السابقة). شكرًا كبيرًا لكل من جعل ذلك ممكنًا.

ملاحظة عن حالة i18n: يحتوي `i18n/` على ملفات README مترجمة للغات المذكورة في أعلى هذا الملف.

## نظرة عامة 🧭

هذا المستودع هو مستودع متعدد الحزم (monorepo) يضم حزمتين منشورتين رئيسيتين:

| الحزمة | الهدف |
| --- | --- |
| `@ricky0123/vad-web` | واجهات برمجة للمستخدم في المتصفح تشمل `MicVAD` و`AudioNodeVAD` و`NonRealTimeVAD` |
| `@ricky0123/vad-react` | غلاف React (`useMicVAD`) لحزمة `vad-web` |

المشروع مصمم للمتصفح أولاً، ويشمل:

- دوال استدعاء لقطع صوتية لحظية للميكروفون (`onSpeechStart`، `onSpeechEnd`، `onVADMisfire`، وغيرها)
- عتبات خوارزمية وعناصر توقيت قابلة للتخصيص
- دعم نماذج Silero القديمة وV5
- تطبيقات عرض/اختبار ومصادر موقع التوثيق داخل هذا المستودع

## المميزات ✨

- مسار VAD موجه للمتصفح يعتمد على نماذج Silero ONNX
- يعمل مع وسوم `<script>` وأدوات التجميع وReact
- قيود تدفق الميكروفون الافتراضية منطقية
- دورة حياة تدفق قابلة للتجاوز (`getStream`, `pauseStream`, `resumeStream`)
- تجزئة كلام غير زمنية واقعية لملف صوت مسبق التسجيل عبر `NonRealTimeVAD`
- تحميل النموذج والأصول بشكل قابل للتكوين عبر `baseAssetPath` و`onnxWASMBasePath`
- يدعم معالجة حالة نموذج legacy وV5 عبر wrappers مدمجة
- يتضمن أمثلة لوسوم `<script>`، و bundlers مبنية على webpack، وReact bundlers، وNext.js

## هيكل المشروع 🗂️

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

مسارات أكثر تفصيلاً:

- `packages/web/src/real-time-vad.ts`: تنسيق VAD في الزمن الحقيقي للميكروفون/audio-node
- `packages/web/src/non-real-time-vad.ts`: تجزئة غير متزامنة للصوت المسبق التسجيل
- `packages/web/src/frame-processor.ts`: منطق العتبات وتحديد حدود مقاطع الكلام
- `packages/react/src/index.ts`: دورة حياة وwrapper حالة Hook React `useMicVAD`

## مصفوفة التوافق 🧩

| المكوّن | البيئة |
| --- | --- |
| `@ricky0123/vad-web` | المتصفحات الحديثة مع WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | تطبيقات React (`react` / `react-dom` >= 16.8.0) |
| سلسلة أدوات التوثيق | Python 3.10 + Poetry (بحسب سير عمل CI) |
| Node runtime في CI | Node 18 (بحسب سير العمل في المستودع) |

إصدارات الحزم الحالية في (`packages/*/package.json`):

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## المتطلبات المسبقة ✅

- استخدام المتصفح: متصفح حديث مع `MediaDevices.getUserMedia`
- التطوير المحلي: Node.js + npm workspaces
- تطوير التوثيق: Python + Poetry (لبناء MkDocs)

النسخة المحلية الموصى بها وفق إعدادات CI:

- Node.js 18.x
- Python 3.10.x

## التثبيت 📦

تثبيت حزمة المتصفح:

```bash
npm i @ricky0123/vad-web
```

تثبيت غلاف React:

```bash
npm i @ricky0123/vad-react
```

تثبيت تبعيات المونوربو (للمساهمين):

```bash
npm install
```

## الاستخدام 🚀

### البدء السريع (وسوم `<script>`)

لاستخدام VAD عبر وسم `<script>` في المتصفح، أضف الوسوم التالية:

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

### استخدام حزمة المتصفح (استيراد وحدة)

```ts
import { MicVAD } from "@ricky0123/vad-web"

const myvad = await MicVAD.new({
  onSpeechEnd: (audio) => {
    console.log("Speech segment length:", audio.length)
  },
})

myvad.start()
```

### استخدام React

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

### استخدام غير لحظي (دفعات صوت)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## الإعدادات ⚙️

تتضمن الخيارات المشتركة بين واجهات البرمجة:

- `positiveSpeechThreshold` (تقريبًا `0.3` افتراضيًا في واجهات الزمن الحقيقي)
- `negativeSpeechThreshold` (تقريبًا `0.25` افتراضيًا في واجهات الزمن الحقيقي)
- `redemptionMs` (تقريبًا `1400` افتراضيًا في واجهات الزمن الحقيقي)
- `preSpeechPadMs` (تقريبًا `800` افتراضيًا في واجهات الزمن الحقيقي)
- `minSpeechMs` (تقريبًا `400` افتراضيًا في واجهات الزمن الحقيقي)

تدعم واجهات الزمن الحقيقي (`MicVAD`، `useMicVAD`) أيضًا:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` أو `"v5"`)
- `baseAssetPath` و`onnxWASMBasePath`
- `workletOptions`

راجع جداول API الكاملة في التوثيق: [مرجع API](https://docs.vad.ricky0123.com/user-guide/api/) و[مرشد الخوارزمية](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### وصفة الإعداد: استضافة النموذج وأصول وقت التشغيل بنفسك

عند عدم استخدام إعدادات CDN الافتراضية، تأكد من أن تطبيقك يخدم:

- `silero_vad_legacy.onnx` و/أو `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- ملفات تنفيذ `onnxruntime-web` (`.wasm`؛ و`.mjs` لبنى تشغيل أحدث)

ثم اضبط التكوين:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## أمثلة 🧪

أمثلة المتجر:

- `examples/script-tags`: إعداد أساسي لوسوم `script`
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: مثال تكامل Next.js

أمر تشغيل المثال من `examples/bundler`:

```bash
npm run build && npm run start
```

يوجد توثيق لتجميع كاشف النشاط الصوتي للمتصفح أو استخدامه في مشاريع Node/React في [vad.ricky0123.com](https://www.vad.ricky0123.com).

## ملاحظات التطوير 🛠️

سكربتات مساحة العمل الجذرية:

```bash
npm run build
npm run test
npm run test:coverage
npm run typecheck
npm run format-check
npm run dev
```

ماذا تفعل:

- `npm run build`: يبني جميع workspaces
- `npm run test`: يشغّل اختبارات الـ workspace
- `npm run test:coverage`: يغطي الاختبارات في `packages/web`
- `npm run typecheck`: يتحقق من TypeScript في الحزم و`test-site` والاختبارات
- `npm run format-check`: يتحقق من تنسيق TS/TSX تحت `packages` و`examples` و`test-site`
- `npm run dev`: يراقب مصادر الحزم و`test-site` ويُعيد البناء ويخدم `test-site/dist`

بناء التوثيق (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

ملاحظات إضافية:

- `./test-site/build.sh` ينسخ أصول VAD/ONNX Runtime المطلوبة إلى `test-site/dist` و`test-site/dist/subpath`
- `./scripts/dev.sh` يستخدم `nodemon` + `live-server` لعملية rebuild-and-serve محلية على المنفذ `8080`
- `./check_vad_up_to_date.sh` مرجعي تاريخي ويشير إلى `silero_vad.onnx` (بينما هذا المستودع يوزع `silero_vad_legacy.onnx` و`silero_vad_v5.onnx`)

## بوابات الجودة & CI 🧱

عمليات GitHub في `.github/workflows/` تغطي:

- الاختبار (`test.yml`)
- فحص الأنواع (`typecheck.yml`)
- فحص التنسيق (`format-check.yml`)
- بناء ونشر التوثيق (`docs.yml`)
- سير نشر الحزم (`publish.yml`)

تُعد هذه سيرات العمل مصدرًا عمليًا للقيود المتوقعة لأدوات/نسخ التشغيل وفحوصات الإصدار.

## استكشاف الأخطاء وإصلاحها 🩺

| العرض | الفحص / الإصلاح |
| --- | --- |
| رفض إذن الميكروفون | تأكد أن المتصفح يمتلك إذن الميكروفون لمصدر Origin الخاص بك. |
| فشل تحميل الأصول (`.onnx`, `.wasm`, `.mjs`, worklet) | عيّن `baseAssetPath` / `onnxWASMBasePath` بشكل صحيح وتأكد من أن الملفات مخدمة فعلاً. |
| مشاكل في إصدارات `onnxruntime-web` الأحدث | تأكد من تقديم ملفات `.mjs` أيضًا، وليس فقط `.wasm`. |
| تطوير محلي عبر أصل غير آمن | تتطلب واجهات ميكروفون المتصفح عادةً سياقًا آمنًا (`https` أو `localhost`). |
| مشاكل bundler وقت البناء | استخدم إرشادات التجميع في [توثيق المتصفح](https://docs.vad.ricky0123.com/user-guide/browser/). |
| مشاكل تكامل Next.js | استخدم أنماط الإعداد الموجودة في [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) وتأكد من مسارات استضافة الأصول الثابتة. |

## الرعاية المالية ❤️

يرجى دعم المشروع ماديًا — خصوصًا إذا كان منتجك التجاري يعتمد على هذه الحزمة. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## تحديث مهم حول دعم node - أكتوبر 2024 📢

أنوي تقليل دعم `ricky0123/vad-node`، حزمة كشف نشاط الصوت لبيئات Node.js من جهة الخادم. لا أنوي نشر أي تحديثات جديدة لحزمة Node من هذه النقطة فصاعدًا. اتخذت هذا القرار للأسباب التالية:

- كان استخدامي الأصلي لهذا المشروع هو كشف نشاط الصوت على جانب العميل. أضفت دعم Node لأن شخصًا طلب ذلك وكنت أريد المساعدة. لكن ليس لدي الكثير من الوقت للعمل على هذا المشروع، وسيمنحني إيقاف دعم `ricky0123/vad-node` المزيد من الوقت للتركيز على `ricky0123/vad-web`.
- من الأسهل على المطورين الفرديين بناء حلول مخصصة للكشف عن النشاط الصوتي على جانب الخادم من تعلم كيفية العمل مع onnxruntime-web وaudio worklets وتقنيات أخرى لإنتاج حل على جانب المتصفح. لذلك أرى أن `ricky0123/vad-web` يوفر قيمة أكبر للمجتمع.
- مشاركة الكود بين حزم المتصفح وNode غير مريحة لأن البيئات تختلف في أمور جوهرية تتعلق بتشغيل واستخدام نموذج كشف النشاط الصوتي.
- حسب [الاستبيان](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)، أغلب المستخدمين يستخدمون `ricky0123/vad-web` (على الأرجح مع `ricky0123/vad-react`).

## خطة الطريق 🛣️

الاتجاه الحالي (استنادًا إلى حالة المستودع وملاحظة الصيانة المذكورة أعلاه):

- مواصلة التركيز على واجهات برمجة للمتصفح أولاً (`@ricky0123/vad-web`، `@ricky0123/vad-react`)
- صيانة وتحسين التوثيق/الأمثلة الخاصة بـ bundlers والأُطُر
- تحسين توثيق المساهمين والمطورين وسير عمل test-site
- إضافة وصيانة README مترجمة ضمن `i18n/`

## المساهمة 🤝

- اقرأ دليل التطوير: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- افتح قضايا أو طلبات دمج في هذا المستودع: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- لفهم سريع لسياق المشروع، انظر إلى [`HACKING.md`](HACKING.md)

## المراجع 📚

1. مستودع Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## الترخيص 📄

- ترخيص المشروع: ISC (انظر [LICENSE](LICENSE))


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
