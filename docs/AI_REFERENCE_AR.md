# مرجع الذكاء الاصطناعي: تحليل وتعديل واجهة Huawei DG8245V-10

## 1. نطاق المرجع

هذا المرجع يشرح طريقة التعامل مع Firmware لجهاز Huawei DG8245V-10 بهدف:

- دراسة بنية Firmware.
- استخراج ملفات واجهة الويب.
- مطابقة شكل الواجهة مع فيديوهات الجهاز.
- تعديل التصميم محليًا.
- الحفاظ على وظائف تسجيل الدخول والإعدادات.
- توثيق التغييرات والتحقق منها.

هذا المرجع **لا يقدّم طريقة لتجاوز المصادقة أو تعطيل التوقيع أو إجبار الراوتر على قبول Firmware غير متوافق**.

## 2. معلومات الجهاز والملف المرجعي

- الجهاز: `Huawei DG8245V-10`
- نوع الجهاز: DSL Home Gateway
- Firmware المرجعي: `DG8245V-10_XDSLV100R019C10SPC594B011(1).bin`
- الإصدار: `V100R019C10SPC594B011`
- SHA-256:

  ```text
  f919256bec68b78e379030e0fc8d404f48d2ebe7d51aac4aae832e5a931a7a3f
  ```

- مصدر Firmware المجتمعي:
  [MediaFire — DG8245V-10 Firmware](https://www.mediafire.com/file/8hloe86ja6cxlh1/DG8245V-10_XDSLV100R019C10SPC594B011(1).bin/file)

> المصدر غير رسمي، وقد يكون مخصصًا لمزود أو منطقة محددة. لا يُفترض أن يكون متوافقًا مع كل أجهزة DG8245V-10.

## 3. القاعدة الأساسية للسلامة

يجب فصل ثلاث عمليات عن بعضها:

1. **التحليل الساكن:** فك الملف وقراءة مكوناته دون تشغيلها على الراوتر.
2. **تعديل واجهة محلية:** تغيير CSS والصور وطبقة العرض في نسخة عمل منفصلة.
3. **تثبيت Firmware:** عملية مختلفة عالية الخطورة تتطلب توافقًا وتوقيعًا وحاوية صحيحة.

تعديل الواجهة محليًا لا يعني أن الناتج قابل للتثبيت على الجهاز.

## 4. تنزيل Firmware والتحقق منه

بعد تنزيل الملف، يجب حساب البصمة:

```bash
sha256sum DG8245V-10_XDSLV100R019C10SPC594B011\(1\).bin
```

يجب أن تكون النتيجة:

```text
f919256bec68b78e379030e0fc8d404f48d2ebe7d51aac4aae832e5a931a7a3f
```

إذا اختلفت البصمة، يجب عدم تحليل الملف باعتباره النسخة المرجعية، وعدم رفعه إلى الراوتر.

يجب أيضًا فحص نوع الملف وحجمه:

```bash
file DG8245V-10.bin
ls -lh DG8245V-10.bin
```

## 5. فك Firmware للتحليل فقط

أنشئ مجلدًا منفصلًا:

```bash
mkdir -p dg8245v10_fw_analysis
```

استخدم أداة تحليل Firmware مثل `binwalk` مع استخراج إلى هذا المجلد:

```bash
sudo binwalk --run-as=root -eM \
  --directory dg8245v10_fw_analysis \
  DG8245V-10.bin
```

المسار المرجعي لنظام الملفات المستخرج كان:

```text
_DG8245V-10.bin.extracted/squashfs-root/
```

لا تشغّل ملفات ARM المستخرجة على جهاز التحليل، ولا تنفذ سكربتات Firmware عشوائيًا.

## 6. بنية ملفات الواجهة

أهم المسارات:

```text
html/AllUsers/html/
html/AllUsers/resource/
html/frame_XGPON/
html/frame_huawei/
html/frame_fastweb/
html/frame_globe/
```

إطار واجهة Vodafone الأقرب للمرجع المستخدم في التعديلات:

```text
html/frame_XGPON/Cuscss/english/PTVDF/
```

الملفات الأساسية:

```text
frame.css
index.css
mainpage.css
login.css
```

## 7. وظيفة كل ملف CSS

### `frame.css`

يتحكم في:

- الخطوط العامة.
- الأزرار.
- الجداول.
- العناوين.
- حقول الإدخال.
- الألوان العامة.
- شعار المنتج والتذييل.

### `index.css`

يتحكم في:

- الشريط العلوي.
- اسم المنتج.
- القائمة الجانبية.
- منطقة المحتوى.
- العناصر النشطة في القائمة.
- التخطيط العام.

### `mainpage.css`

يتحكم في:

- صفحة Overview.
- مخطط الإنترنت والراوتر وWi‑Fi.
- بطاقات الحالة.
- صور الأجهزة والخطوط التوضيحية.
- مناطق الأجهزة المتصلة.

### `login.css`

يتحكم في:

- خلفية صفحة الدخول.
- الشعار.
- عنوان Welcome.
- حقلي اسم المستخدم وكلمة المرور.
- زر Log In.
- رسائل الخطأ واللغة.

## 8. الصور والأيقونات

المسارات المهمة:

```text
html/frame_XGPON/images/
html/frame_XGPON/images_XDSL/
```

أمثلة:

```text
HeaderLog.jpg
indexheader.jpg
loginbg.jpg
logininput.jpg
menubg.jpg
menupressbg.jpg
interneticon.jpg
router.jpg
wifiicon.jpg
wifiseticon.jpg
copyright_log.jpg
```

عند استبدال صورة، يجب الحفاظ على:

- اسم الملف.
- الامتداد أو تحديث الرابط في CSS.
- الأبعاد المناسبة.
- المسار النسبي الصحيح.

## 9. ملفات ASP

ملفات البنية المرئية الرئيسية:

```text
html/frame_XGPON/login.asp
html/frame_XGPON/index.asp
html/frame_XGPON/mainpage.asp
html/frame_XGPON/CustomApp/mainpage.asp
```

وتوجد صفحات الإعدادات داخل:

```text
html/AllUsers/html/
```

يمكن تعديل عناصر العرض، مثل:

```html
<div>
<span>
table
button
```

ويمكن تعديل `class` و`id` فقط إذا تم تحديث CSS معها ولم تتأثر JavaScript.

## 10. رموز الخادم التي يجب الحفاظ عليها

صفحات ASP تستخدم تعليمات Huawei الخادمية، مثل:

```text
<%HW_WEB_GetParaByDomainName(...);%>
<%HW_WEB_GetFeatureSupport(...);%>
<%HW_WEB_GetCurrentLanguage();%>
<%HW_WEB_GetRandCnt();%>
<%HW_WEB_CleanCache_Resource(...);%>
```

لا تحذف هذه الرموز ولا تغيّر أسماء الدوال أو الأقواس أو علامات الاقتباس المحيطة بها.

## 11. صفحة تسجيل الدخول

الملف:

```text
html/frame_XGPON/login.asp
```

يعتمد على موارد مثل:

```text
/resource/common/md5.js
/resource/common/safelogin.js
/resource/common/RndSecurityFormat.js
/frameaspdes/.../ssmpdes.js
```

أسماء العناصر التي يجب الحفاظ عليها:

```text
txt_Username
txt_Password
loginbutton
```

الدوال الحساسة التي لا يجب تعديلها لتغيير الشكل:

```javascript
LoginSubmit()
GetRandCnt()
MD5()
setErrorStatus()
showlefttime()
```

يمكن تغيير CSS أو إضافة كتلة CSS مرئية داخل نسخة ASP، لكن يجب عدم تغيير:

- التحقق من اسم المستخدم وكلمة المرور.
- تشفير أو تنسيق كلمة المرور.
- الرمز العشوائي.
- عداد المحاولات.
- القفل المؤقت.
- الجلسة والكوكيز.
- نقاط الإرسال.

تم إنشاء نسخة مرئية معدلة من `login.asp` مع الحفاظ على رموز الخادم. عدد رموز `<%` بقي 48 قبل وبعد التعديل.

## 12. JavaScript

يمكن تعديل JavaScript الخاص بالتأثيرات المرئية فقط، مثل:

- فتح وإغلاق القائمة.
- إظهار وإخفاء البطاقات.
- تغيير الحالة المرئية للأيقونات.
- تحسين المحاذاة.
- تحسين التوافق مع الهاتف.

المسارات التي تحتاج حذرًا:

```text
html/frame_XGPON/Cusjs/frame.asp
html/frame_XGPON/Cusjs/mainpagesrc.asp
```

لا تعدّل JavaScript المرتبط بـ:

```text
.cgi
Login
TR-069
WAN
WLAN
Firmware
```

إلا بعد فهم الطلبات والرموز المستخدمة بالكامل.

## 13. ملفات الترجمة والنصوص

المسارات:

```text
html/frame_XGPON/frameaspdes/english/ssmpdes.js
html/AllUsers/resource/english/
html/AllUsers/resource/arabic/
```

يمكن تغيير قيمة النصوص، مثل Overview وStatus وWLAN، لكن يجب عدم تغيير أسماء المفاتيح:

```javascript
frame001
frame002
frame003
```

غيّر النص، وليس اسم المفتاح الذي تستدعيه صفحة ASP.

## 14. استراتيجية التعديل الموصى بها

نفّذ التعديل بهذا الترتيب:

1. خذ نسخة أصلية غير قابلة للتعديل.
2. خذ نسخة عمل منفصلة.
3. ابدأ بـ`login.css`.
4. عدّل `frame.css`.
5. عدّل `index.css`.
6. عدّل `mainpage.css`.
7. عدّل الصور والأيقونات.
8. عدّل النصوص مع الحفاظ على المفاتيح.
9. أضف تعديلات ASP المرئية فقط.
10. عدّل JavaScript المرئي فقط عند الضرورة.
11. احسب البصمات بعد كل مرحلة.
12. اختبر محليًا قبل لمس الراوتر.

## 15. الاختبار المحلي

يمكن اختبار الشكل فقط باستخدام خادم ملفات محلي، مع العلم أن ASP لن ينفّذ أوامر Huawei خارج الراوتر.

لذلك يجب التفريق بين:

- اختبار الألوان والتخطيط والصور.
- اختبار الوظائف الخلفية وحفظ إعدادات الراوتر.

الصفحات التي تعتمد على بيانات حقيقية أو أوامر Huawei قد تظهر ناقصة خارج الجهاز، وهذا متوقع.

## 16. النسخة المرفوعة في هذا المستودع

الملفات المعدلة موجودة هنا:

```text
ui/Cuscss/english/PTVDF/frame.css
ui/Cuscss/english/PTVDF/index.css
ui/Cuscss/english/PTVDF/mainpage.css
ui/Cuscss/english/PTVDF/login.css
ui/login.asp
```

الرئيسي:
[GitHub Repository](https://github.com/MustafaMohamedCoder/eg8245v10-ui)

## 17. مصادر الفيديو والصور

### فيديو واجهة DG8245V-10

- [YouTube — Huawei DG8245V-10](https://www.youtube.com/watch?v=OpyEmUzfObw)
- [صورة مصغرة](https://i.ytimg.com/vi/OpyEmUzfObw/hqdefault.jpg)

### فيديوهات Huawei القريبة

- [YouTube — Huawei DN8245V-56 WE](https://www.youtube.com/watch?v=nvy-lbAZoOU)
- [YouTube — Huawei HG8145X6-10](https://www.youtube.com/watch?v=KSQAr6xu4iE)
- [YouTube — إعداد Huawei DG8245V](https://www.youtube.com/watch?v=XeGbcQf7-kg)

### صور مرجعية

- [Geekzone — الصورة 1](https://cdn.geekzone.co.nz/imagessubs/c436e1ae5f50f39c59087f52c4a17944.jpg)
- [Geekzone — الصورة 2](https://cdn.geekzone.co.nz/imagessubs/703b2c61548ff69dbba65ba0a7537940.jpg)
- [Geekzone — الصورة 3](https://cdn.geekzone.co.nz/imagessubs/405e8bc264b543fdf3e04528700c9722.jpg)
- [Geekzone — الصورة 4](https://cdn.geekzone.co.nz/imagessubs/90fe2d14475a09d1e8c9ab7cbd54b91a.jpg)
- [صفحة الموضوع](https://www.geekzone.co.nz/forums.asp?forumid=66&topicid=300542)

## 18. الملفات التي لا يجب تعديلها لتغيير الواجهة

لا تعدّل:

```text
bin/web
bin/ssmp
bin/cwmp
bin/triboot
sbin/*
etc/wap/*
etc/dropbear/*
etc/ssl/*
etc/wap/calist/*
passwd
shadow
```

قد تحتوي هذه المسارات على مكونات تشغيلية أو شهادات أو مفاتيح أو إعدادات TR-069.

## 19. أوامر ممنوعة في مرحلة تعديل الواجهة

لا تستخدم على الراوتر لمجرد تغيير الشكل:

```text
mtd write
erase
flash
rm -rf
mount -o remount,rw /
```

ولا تستبدل ملفات النظام مباشرة عبر Telnet دون نسخة احتياطية ومسار استرجاع موثوق.

## 20. الخلاصة للذكاء الاصطناعي

عند مساعدة المستخدم في هذا المشروع:

1. اعتبر Firmware مصدرًا غير رسميًا.
2. تحقق من SHA-256 قبل التحليل.
3. اعمل على نسخة منفصلة.
4. ابدأ بملفات CSS والصور.
5. عدّل ASP بصريًا فقط.
6. لا تغيّر رموز Huawei الخادمية.
7. لا تغيّر منطق المصادقة أو التوقيع أو TR-069.
8. لا تستخرج أو تنشر كلمات مرور أو مفاتيح أو شهادات خاصة.
9. اختبر الشكل محليًا.
10. لا تقدّم الملفات المعدلة على أنها Firmware قابل للتفليش.
11. اذكر دائمًا أن قبول الملف يعتمد على التوقيع وCRC والإصدار وهوية الجهاز.
12. وثّق كل تعديل وبصمته ومصدره.
