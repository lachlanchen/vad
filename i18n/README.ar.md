[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

# اكتشاف نشاط الصوت لجافاسكربت

[![npm vad-web](https://img.shields.io/npm/v/@ricky0123/vad-web?color=0b69d7&label=%40ricky0123%2Fvad-web&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-web)
[![npm vad-react](https://img.shields.io/npm/v/@ricky0123/vad-react?color=0b69d7&label=%40ricky0123%2Fvad-react&style=flat-square)](https://www.npmjs.com/package/@ricky0123/vad-react)
[![Docs](https://img.shields.io/badge/docs-vad.ricky0123.com-0a7f5a?style=flat-square)](https://docs.vad.ricky0123.com/)
[![Demo](https://img.shields.io/badge/demo-live-ff8c00?style=flat-square)](https://www.vad.ricky0123.com)
[![Monorepo](https://img.shields.io/badge/repo-monorepo-111827?style=flat-square)](https://github.com/ricky0123/vad)
[![Discord](https://img.shields.io/badge/discord-community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/4WPeGEaSpF)
[![License: ISC](https://img.shields.io/badge/license-ISC-2ea44f?style=flat-square)](LICENSE)

> شغّل دوال رد النداء على مقاطع الصوت التي تحتوي كلام المستخدم في بضع أسطر من الشيفرة.

تهدف هذه الحزمة إلى توفير كاشف نشاط صوتي (VAD) دقيق وسهل الاستخدام يعمل داخل المتصفح. باستخدام هذه الحزمة، يمكنك طلب إذن استخدام الميكروفون من المستخدم، وبدء تسجيل الصوت، وإرسال المقاطع التي تحتوي كلامًا إلى الخادم لمعالجتها، أو عرض مؤشر/رسوم متحركة معيّنة عندما يتحدث المستخدم. لاحظ أنني قررت [إيقاف دعم node](#تحديث-مهم-حول-دعم-node---أكتوبر-2024-) للتركيز على حالة الاستخدام في المتصفح.

| لمحة سريعة | التفاصيل |
| --- | --- |
| الحزم الأساسية | `@ricky0123/vad-web`, `@ricky0123/vad-react` |
| بيئة التشغيل الأساسية | المتصفح (`WebAudio` + `getUserMedia`) |
| الوثائق | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| العرض المباشر | [vad.ricky0123.com](https://www.vad.ricky0123.com) |

## جدول المحتويات

- [الروابط السريعة 🔗](#الروابط-السريعة-)
- [نظرة عامة 🧭](#نظرة-عامة-)
- [المزايا ✨](#المزايا-)
- [هيكل المشروع 🗂️](#هيكل-المشروع-️)
- [مصفوفة التوافق 🧩](#مصفوفة-التوافق-)
- [المتطلبات المسبقة ✅](#المتطلبات-المسبقة-)
- [التثبيت 📦](#التثبيت-)
- [الاستخدام 🚀](#الاستخدام-)
- [الإعداد ⚙️](#الإعداد-️)
- [الأمثلة 🧪](#الأمثلة-)
- [ملاحظات التطوير 🛠️](#ملاحظات-التطوير-️)
- [بوابات الجودة وCI 🧱](#ci-وبوابات-الجودة-)
- [استكشاف الأخطاء وإصلاحها 🩺](#استكشاف-الأخطاء-وإصلاحها-)
- [الدعم المالي ❤️](#الدعم-المالي-️)
- [❤️ Support](#-support)
- [تحديث مهم حول دعم node - أكتوبر 2024 📢](#تحديث-مهم-حول-دعم-node---أكتوبر-2024-)
- [خريطة الطريق 🛣️](#خريطة-الطريق-)
- [المساهمة 🤝](#المساهمة-)
- [المراجع 📚](#المراجع-)
- [الترخيص 📄](#الترخيص-)

## الروابط السريعة 🔗

| المورد | الرابط |
| --- | --- |
| العرض المباشر | [vad.ricky0123.com](https://www.vad.ricky0123.com) |
| التوثيق | [docs.vad.ricky0123.com](https://docs.vad.ricky0123.com/) |
| Discord | [انضم إلى المجتمع](https://discord.gg/4WPeGEaSpF) |
| الاستبيان | [شارك حالة استخدامك](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv) |
| دليل المساهمة | [دليل التوجيه للمطورين](https://docs.vad.ricky0123.com/developer-guide/hacking/) |

- توجد ملفات التوثيق في `./docs`.
- ابدأ هنا لأي مساهمة: [دليل المساعدة التقنية](https://docs.vad.ricky0123.com/developer-guide/hacking/). الأسئلة مرحب بها عبر issues أو Discord.

تعمل هذه الحزم خلف الكواليس على [Silero VAD](https://github.com/snakers4/silero-vad) [[1]](#المراجع) باستخدام [ONNX Runtime Web](https://github.com/microsoft/onnxruntime/tree/main/js/web) (مع مراجع تاريخية إلى ONNX Runtime Node.js من الدعم القديم في Node). شكرًا كبيرًا للفريقين الذين جعلوا هذا ممكنًا.

ملاحظة حول حالة i18n: يحتوي المجلد `i18n/` على ملفات README مترجمة للغات المرتبطة أعلاه.

## نظرة عامة 🧭

هذا المستودع هو monorepo يضم حزمتين منشورتين رئيسيتين:

| الحزمة | الغرض |
| --- | --- |
| `@ricky0123/vad-web` | واجهات برمجة المتصفح بما فيها `MicVAD` و`AudioNodeVAD` و`NonRealTimeVAD` |
| `@ricky0123/vad-react` | غلاف React hook (`useMicVAD`) لحزمة `vad-web` |

المشروع مُصمّم أولًا للمتصفح ويشمل:

- ردود اتصال تقسيم الميكروفون في الزمن الحقيقي (`onSpeechStart`، `onSpeechEnd`، `onVADMisfire`، وغيرها)
- عتبات خوارزمية قابلة للتهيئة وتحكمات زمنية
- دعم نموذج Silero القديم و v5
- تطبيقات demo/tests ومصادر موقع التوثيق ضمن هذا المستودع

## المزايا ✨

- خط أنابيب VAD للمتحسب (المتصفح) مدعوم بنماذج Silero ONNX
- يعمل مع وسوم `script` و أنظمة التجميع وReact
- قيود افتراضية معقولة لبث الميكروفون
- يمكن تجاوز دورة حياة البث (`getStream`، `pauseStream`، `resumeStream`)
- تقسيم الكلام خارج الزمن الحقيقي للصوت المسجّل مسبقًا عبر `NonRealTimeVAD`
- تحميل قابل للتهيئة للنموذج/الأصول عبر `baseAssetPath` و`onnxWASMBasePath`
- يدعم التعامل مع حالة النموذجين legacy و v5 عبر wrappers مدمجة
- يتضمن أمثلة لوسوم `script`، وحزم webpack، وحزم React، وNext.js

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

- `packages/web/src/real-time-vad.ts`: تنسيق VAD للتعامل مع الميكروفون/عقدة الصوت في الزمن الحقيقي
- `packages/web/src/non-real-time-vad.ts`: تقسيم غير متزامن للصوت المسجل مسبقًا
- `packages/web/src/frame-processor.ts`: منطق العتبات وحدود مقاطع الكلام
- `packages/react/src/index.ts`: دورة حياة غلاف `useMicVAD` وحالته

## مصفوفة التوافق 🧩

| المكوّن | البيئة |
| --- | --- |
| `@ricky0123/vad-web` | متصفحات حديثة تدعم WebAudio + `MediaDevices.getUserMedia` |
| `@ricky0123/vad-react` | تطبيقات React (`react` / `react-dom` >= 16.8.0) |
| سلسلة أدوات التوثيق | Python 3.10 + Poetry (حسب سير عمل CI) |
| Node المستخدم في CI | Node 18 (حسب سير عمل المستودع) |

إصدارات لحظية للحزم كما في `packages/*/package.json`:

- `@ricky0123/vad-web@0.0.27`
- `@ricky0123/vad-react@0.0.33`

## المتطلبات المسبقة ✅

- استخدام المتصفح: متصفح حديث يدعم `MediaDevices.getUserMedia`
- التطوير المحلي: Node.js + npm workspaces
- تطوير التوثيق: Python + Poetry (لبناء MkDocs)

الحد الأدنى المقترح محليًا بناءً على إعداد CI:

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

تثبيت تبعيات monorepo (للمساهمين):

```bash
npm install
```

## الاستخدام 🚀

### بداية سريعة (وسوم script)

لاستخدام VAD عبر وسم script داخل المتصفح، أدرج وسوم الـ script التالية:

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

### الاستخدام خارج الزمن الحقيقي (batch audio)

```ts
import { NonRealTimeVAD } from "@ricky0123/vad-web"

const myvad = await NonRealTimeVAD.new()
for await (const { audio, start, end } of myvad.run(audioData, sampleRate)) {
  console.log({ start, end, samples: audio.length })
}
```

## الإعداد ⚙️

تشمل الخيارات المشتركة بين واجهات API:

- `positiveSpeechThreshold` (افتراضيًا حول `0.3` في واجهات الزمن الحقيقي)
- `negativeSpeechThreshold` (افتراضيًا حول `0.25` في واجهات الزمن الحقيقي)
- `redemptionMs` (افتراضيًا حول `1400` في واجهات الزمن الحقيقي)
- `preSpeechPadMs` (افتراضيًا حول `800` في واجهات الزمن الحقيقي)
- `minSpeechMs` (افتراضيًا حول `400` في واجهات الزمن الحقيقي)

واجهات الزمن الحقيقي (`MicVAD`, `useMicVAD`) تدعم أيضًا:

- `getStream`, `pauseStream`, `resumeStream`
- `onFrameProcessed`, `onSpeechStart`, `onSpeechRealStart`, `onSpeechEnd`, `onVADMisfire`
- `submitUserSpeechOnPause`
- `model` (`"legacy"` أو `"v5"`)
- `baseAssetPath` و `onnxWASMBasePath`
- `workletOptions`

راجع جداول API الكاملة في التوثيق: [مرجع API](https://docs.vad.ricky0123.com/user-guide/api/) و[دليل الخوارزمية](https://docs.vad.ricky0123.com/user-guide/algorithm/).

### وصفة الإعداد: استضافة النموذج والأصول الخاصة بك

عند عدم استخدام إعدادات CDN الافتراضية، تأكد من أن تطبيقك يقدم:

- `silero_vad_legacy.onnx` و/أو `silero_vad_v5.onnx`
- `vad.worklet.bundle.min.js`
- ملفات تشغيل `onnxruntime-web` (`.wasm`، و`.mjs` لبناءات runtime الأحدث)

ثم اضبط الإعدادات:

```ts
const vad = await MicVAD.new({
  baseAssetPath: "/assets/vad/",
  onnxWASMBasePath: "/assets/onnxruntime/",
  onSpeechEnd: (audio) => {
    // handle audio segment
  },
})
```

## الأمثلة 🧪

أمثلة المستودع:

- `examples/script-tags`: إعداد أساسي باستخدام وسوم script
- `examples/bundler`: webpack + `@ricky0123/vad-web`
- `examples/react-bundler`: webpack + `@ricky0123/vad-react`
- `examples/nextjs`: مثال تكامل Next.js

أمر مثال من `examples/bundler`:

```bash
npm run build && npm run start
```

يوجد توثيق للتجميع bundling لكاشف النشاط الصوتي للمتصفح أو استخدامه في مشاريع node أو React على [vad.ricky0123.com](https://www.vad.ricky0123.com).

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

ما يفعله كل أمر:

- `npm run build`: يبني جميع workspaces
- `npm run test`: يشغّل اختبارات workspaces
- `npm run test:coverage`: التغطية لحزمة `packages/web`
- `npm run typecheck`: يفحص TypeScript في الحزم و`test-site` والاختبارات
- `npm run format-check`: يفحص التنسيق لـ TS/TSX داخل `packages` و`examples` و`test-site`
- `npm run dev`: يراقب مصادر الحزم و`test-site`، ويعيد البناء ويخدم `test-site/dist`

بناء التوثيق (MkDocs + Poetry):

```bash
poetry install
poetry run mkdocs serve
```

ملاحظات إضافية:

- `./test-site/build.sh` ينسخ أصول VAD/ONNX Runtime المطلوبة إلى `test-site/dist` و`test-site/dist/subpath`
- `./scripts/dev.sh` يستخدم `nodemon` + `live-server` لمشاريع إعادة البناء والتشغيل المحلي على المنفذ `8080`
- `./check_vad_up_to_date.sh` هو ملف تاريخي ويشير إلى `silero_vad.onnx` (بينما هذا المستودع يوفّر `silero_vad_legacy.onnx` و`silero_vad_v5.onnx`)

## CI وبوابات الجودة 🧱

سير عمل GitHub في `.github/workflows/` يغطي:

- الاختبارات (`test.yml`)
- فحص الأنواع (`typecheck.yml`)
- فحص التنسيق (`format-check.yml`)
- بناء/نشر التوثيق (`docs.yml`)
- سير نشر الحزم (`publish.yml`)

تُعد هذه السير عمل مصادر مرجعية عملية للإصدارات المتوقعة لبيئات التشغيل والأدوات وفحوصات الإصدار.

## استكشاف الأخطاء وإصلاحها 🩺

| العرض | الفحص / الحل |
| --- | --- |
| رفض إذن الميكروفون | تأكد من أن المتصفح يملك إذن الميكروفون لنطاقك (`origin`) |
| فشل تحميل الأصول (`.onnx`, `.wasm`, `.mjs`, worklet) | تأكد من ضبط `baseAssetPath` / `onnxWASMBasePath` بشكل صحيح وتحقق من أن الملفات تُخدَّم فعليًا |
| مشاكل مع إصدارات أحدث من `onnxruntime-web` | يجب أيضًا تقديم ملفات `.mjs`، وليس ملفات `.wasm` فقط |
| التطوير المحلي عبر أصل غير آمن | تتطلب واجهات ميكروفون المتصفح عادة سياقات آمنة (`https` أو `localhost`) |
| مشاكل bundler أثناء البناء | استخدم إرشادات التجميع الموجودة في [توثيق المتصفح](https://docs.vad.ricky0123.com/user-guide/browser/) |
| مشاكل تكامل Next.js | استخدم أنماط الإعداد الموضحة في [`examples/nextjs/next.config.js`](examples/nextjs/next.config.js) وتحقق من مسارات استضافة الأصول الثابتة |

## الدعم المالي ❤️

يرجى دعم المشروع ماليًا، خاصة إذا كان منتجك التجاري يعتمد على هذه الحزمة. [![Become a Sponsor](https://img.shields.io/static/v1?label=Become%20a%20Sponsor&message=%E2%9D%A4&logo=GitHub&style=flat&color=d42f2d)](https://github.com/sponsors/ricky0123)

## ❤️ Support

| Donate | PayPal | Stripe |
|---|---|---|
| [![Donate](https://img.shields.io/badge/Donate-LazyingArt-0EA5E9?style=for-the-badge&logo=ko-fi&logoColor=white)](https://chat.lazying.art/donate) | [![PayPal](https://img.shields.io/badge/PayPal-RongzhouChen-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/RongzhouChen) | [![Stripe](https://img.shields.io/badge/Stripe-Donate-635BFF?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## تحديث مهم حول دعم node - أكتوبر 2024 📢

سأبدأ في إنهاء دعم `ricky0123/vad-node`، وهي حزمة اكتشاف النشاط الصوتي لبيئات Node على الخادم. لا أنوي نشر أي تحديثات إضافية لحزمة Node من الآن فصاعدًا. اتخذت هذا القرار للأسباب التالية:

- كان استخدامي الأصلي لهذا المشروع هو كشف نشاط الصوت من جهة العميل. أضفت دعم Node لأن أحدهم طلبه وأردت المساعدة. لكنّ الوقت المتاح لدي للعمل على المشروع محدود، وإنهاء `ricky0123/vad-node` سيمنحني وقتًا أكبر للتركيز على `ricky0123/vad-web`.
- من الأسهل كثيرًا للمطورين الفرديين إنشاء حلول كشف نشاط صوتي مخصصة في جهة الخادم بدلًا من تعلم استخدام onnxruntime-web، وـaudio worklets، وتقنيات أخرى لبناء حل من جهة العميل. لذلك أرى أن `ricky0123/vad-web` يقدّم قيمة أكبر للمجتمع.
- مشاركة الشيفرة بين حزم المتصفح وNode صعبة إلى حد كبير لأن البيئتين تختلفان بطرق مهمة عند تشغيل واستخدام نموذج كشف النشاط الصوتي.
- وفقًا لــ [الاستطلاع](https://uaux2a2ppfv.typeform.com/to/iJG2gCQv)، يستخدم أغلب المستخدمين `ricky0123/vad-web` (ربما مع `ricky0123/vad-react`).

## خريطة الطريق 🛣️

الاتجاه الحالي (بناءً على حالة المستودع وملاحظة الصيانة أعلاه):

- الاستمرار بالتركيز على واجهات API الموجّهة للمتصفح (`@ricky0123/vad-web`، `@ricky0123/vad-react`)
- الحفاظ على وتطوير التوثيق/الأمثلة الخاصة بحزم التجميع والأُطر
- تحسين توثيق المساهمين/المطورين وسير عمل test-site
- إضافة وصيانة ملفات README مترجمة ضمن `i18n/`

## المساهمة 🤝

- اقرأ دليل التطوير: [docs.vad.ricky0123.com/developer-guide/hacking](https://docs.vad.ricky0123.com/developer-guide/hacking/)
- افتح issue أو PR في هذا المستودع: [github.com/ricky0123/vad/issues](https://github.com/ricky0123/vad/issues)
- لمرجع سريع على سياق المشروع، راجع [`HACKING.md`](HACKING.md)

## المراجع 📚

1. مستودع Silero VAD: [github.com/snakers4/silero-vad](https://github.com/snakers4/silero-vad)

## الترخيص 📄

- ترخيص المشروع: ISC (راجع [LICENSE](LICENSE))
