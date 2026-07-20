# openFDA CRL Resolution Intelligence

<div dir="rtl">

## نظرة عامة

مشروع مفتوح لتحليل **خطابات الاستجابة الكاملة** (Complete Response Letters — CRLs) الصادرة عن إدارة الغذاء والدواء الأمريكية (FDA)، انطلاقًا من بيانات **openFDA CRL Transparency**.

يحوّل المشروع نصوص الخطابات الطويلة وغير المتجانسة إلى قاعدة فرز تنظيمية قابلة للتتبع، مع الفصل بين:

- مرشحي العيوب المؤثرة في قابلية الموافقة.
- الإجراءات العلاجية المطلوبة.
- التعليقات غير المانعة للموافقة.
- اللغة والقوالب الروتينية.
- المقاطع غير القابلة للحكم بسبب الحجب أو OCR أو التجزئة.

الهدف الحالي ليس إعلان قائمة نهائية لأسباب الرفض أو بناء نموذج تنبؤ بالموافقة، بل إنشاء أساس قابل للتدقيق والتحكيم البشري وبناء **Issue Graph** يتابع العيب والإجراء والنتيجة عبر دورات المراجعة.

## النتائج الأساسية في الإصدار الحالي

| المؤشر | القيمة |
|---|---:|
| سجلات المصدر الخام | 455 |
| خطابات COMPLETE RESPONSE | 442 |
| الخطابات الفريدة المحللة | 441 |
| فروع الطلبات بعد التطبيع | 333 |
| الفروع متعددة الدورات | 79 |
| مرشحو العيوب المؤثرة في قابلية الموافقة | 950 |
| الرسائل التي تحتوي مرشح A واحدًا على الأقل | 402 |
| الروابط الزمنية المرشحة | 209 |

> **تنبيه منهجي:** الأعداد أعلاه تصف مخرجات نظام الفرز الحالي، وليست تقديرًا نهائيًا لعدد العيوب الذرية أو انتشارها.

## منهجية الترميز A–E

| الفئة | المعنى |
|---|---|
| A | مرشح عيب مؤثر في قابلية الموافقة |
| B | إجراء مطلوب دون مشكلة أم واضحة |
| C | تعليق غير مانع للموافقة |
| D | لغة روتينية أو قالب متكرر |
| E | نص غير قابل للحكم ويحتاج مراجعة |

## الملفات الرئيسية

- [`data/CRL_analysis.xlsx`](data/CRL_analysis.xlsx): ملف التحليل متعدد الأوراق، ويشمل الرسائل، والطبقات A–E، والروابط الزمنية، والتصنيف، وقوائم المراجعة.
- [`docs/CRL_Arabic_Methodology.docx`](docs/CRL_Arabic_Methodology.docx): الوثيقة العربية الكاملة للمنهجية وعقد الترميز والنتائج والقيود.
- [`docs/DATA_DICTIONARY_AR.md`](docs/DATA_DICTIONARY_AR.md): قاموس مختصر للحقول والكيانات.
- [`docs/VALIDATION_PLAN_AR.md`](docs/VALIDATION_PLAN_AR.md): خطة التحكيم البشري وقياس الجودة.

## المبادئ المنهجية

1. الاحتفاظ بالنص المصدري وإمكانية التتبع إلى الخطاب الأصلي.
2. عدم مساواة المقطع المستخرج بالعيب الذري النهائي.
3. استخدام أعلام جودة وصفية بدل نسب ثقة غير معايرة.
4. الحفاظ على الفروع التنظيمية للطلبات مثل Original وSupplement.
5. عدم إنشاء رابط زمني إلا إذا كانت الدورة السابقة أقدم من الدورة الحالية.
6. التمييز بين **استمرار العيب** و**استمرار اعتماد الموافقة على المجال نفسه**.
7. عدم استخدام المرشحين لتقدير الانتشار أو التنبؤ قبل التحكيم البشري.

## القيد الزمني للروابط

```text
same_normalized_application
AND prior_review_cycle < current_review_cycle
```

هذا الشرط يمنع المطابقة داخل الدورة نفسها، لكنه لا يثبت وحده أن العيب استمر؛ إذ تحتاج العلاقة إلى تحكيم دلالي.

## الاستخدام المقصود

هذا الإصدار مناسب لـ:

- التدقيق والاستكشاف التنظيمي.
- تحديد أولويات المراجعة البشرية.
- تطوير دليل ترميز ومعيار ذهبي.
- دراسة العلاقات بين العيوب والإجراءات عبر الدورات.
- تطوير أدوات ذكاء تنظيمي مستقبلية.

ولا ينبغي استخدامه حاليًا لـ:

- حساب انتشار نهائي لأنواع العيوب.
- التنبؤ باحتمال موافقة FDA.
- إصدار قرارات تنظيمية أو طبية دون مراجعة خبير.

## مصدر البيانات

المصدر الأساسي: [openFDA CRL Transparency](https://open.fda.gov/data/crl/)

آخر تحديث للمصدر المستخدم في التحليل: **13 يوليو 2026**.

## حالة المشروع

**Research / audit prototype** — قاعدة فرز منهجية قابلة للتتبع، وليست مجموعة بيانات محكّمة نهائية.

</div>

---

## English summary

This repository contains an auditable, rule-based regulatory NLP reanalysis of FDA Complete Response Letters published through openFDA. It separates approvability-deficiency candidates, remediation actions, non-approvability comments, boilerplate language, and unassessable text. Cross-cycle links are generated only under an explicit chronological constraint and remain candidates pending human adjudication.

## Citation

Please cite the repository using the metadata in [`CITATION.cff`](CITATION.cff).

## License

Project-authored documentation and analysis outputs are released under the [Creative Commons Attribution 4.0 International License](LICENSE). FDA/openFDA source material remains subject to its original terms, notices, and public-domain status where applicable.
