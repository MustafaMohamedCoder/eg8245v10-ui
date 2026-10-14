# Huawei DG8245V-10 — واجهة مطابقة بصريًا للفيديو

هذه المستودع يحتوي على **تعديلات شكلية فقط** لواجهة Huawei DG8245V-10، مستخرجة من نسخة Firmware متداولة للإصدار:

```text
V100R019C10SPC594B011
```

الهدف هو تقريب شكل واجهة فيديوهات DG8245V-10: الشريط العلوي، القائمة الجانبية، صفحة Overview، الجداول، الأزرار، وصفحة تسجيل الدخول.

> **مهم:** هذه الملفات ليست Firmware كاملًا، ولا تصلح للتفليش أو للرفع المباشر عبر Telnet.

## رابط ملف Firmware المستخدم للتحليل

- [تحميل Firmware DG8245V-10 من MediaFire](https://www.mediafire.com/file/8hloe86ja6cxlh1/DG8245V-10_XDSLV100R019C10SPC594B011(1).bin/file)
- اسم الملف: `DG8245V-10_XDSLV100R019C10SPC594B011(1).bin`
- الإصدار: `V100R019C10SPC594B011`
- SHA-256:

  ```text
  f919256bec68b78e379030e0fc8d404f48d2ebe7d51aac4aae832e5a931a7a3f
  ```

> هذا رابط مجتمعي/غير رسمي، وليس رابط تنزيل رسميًا من Huawei. استخدمه للتحليل الساكن فقط، وتحقق من البصمة بعد التنزيل. لا ترفع الملف إلى راوتر Vodafone أو DG8245V-10 قبل التأكد من توافق المنطقة والمزود وإصدار الجهاز.

الصفحة الرسمية للمنتج: [Huawei DG8245V-10 Support](https://support.huawei.com/enterprise/en/access-network/dg8245v-10-pid-22304968) — المنتج مصنف حاليًا كمنتهي الخدمة، وقد لا تتوفر تنزيلات رسمية.

## محتويات المشروع

```text
ui/Cuscss/english/PTVDF/frame.css
ui/Cuscss/english/PTVDF/index.css
ui/Cuscss/english/PTVDF/mainpage.css
ui/Cuscss/english/PTVDF/login.css
ui/login.asp
docs/SHA256SUMS.txt
```

## ما تم تعديله

- لون وتخطيط الشريط العلوي.
- ألوان القائمة الجانبية وحالة المرور بالفأرة.
- ألوان صفحة Overview وبطاقات الحالة.
- ألوان الجداول والأزرار.
- خلفية صفحة تسجيل الدخول وتدرجها.
- الخطوط، المحاذاة، حدود الحقول، وتأثير التركيز.
- إضافة تنسيق مرئي إلى نسخة `login.asp` فقط.

## ما لم يتم تعديله

لم يتم تعديل منطق المصادقة أو الوظائف الخلفية، ومنها:

- `LoginSubmit()`
- `GetRandCnt()`
- `MD5()`
- عداد محاولات الدخول والقفل المؤقت.
- رموز Huawei الخادمية من الشكل `<% ... %>`.
- ملفات JavaScript وXML التنفيذية.
- ملفات `bin/web` و`bin/ssmp` و`bin/cwmp`.

تم التحقق من أن عدد رموز الخادم في `login.asp` بقي كما هو: **48 رمزًا قبل وبعد التعديل**.

## طريقة استخدام الملفات للتحليل المحلي

1. فك نسخة Firmware في بيئة معزولة.
2. احتفظ بالملف الأصلي دون تعديل.
3. خذ نسخة احتياطية من ملفات الواجهة.
4. استبدل ملفات CSS في نسخة العمل فقط:

   ```text
   frame.css
   index.css
   mainpage.css
   login.css
   ```

5. استخدم `login.asp` المعدل للمراجعة أو الاختبار المحلي فقط.
6. قارن الواجهة بصور وفيديوهات المصادر أدناه.
7. لا ترفع الملفات إلى الراوتر قبل التحقق من المسار القابل للكتابة والتوافق الكامل.

## ما لا يجب تنفيذه

لا تستخدم هذه الملفات مع أوامر الفلاش أو أقسام النظام:

```text
mtd write
flash
erase
rm -rf
```

إعادة بناء Firmware قابل للتثبيت تحتاج إلى الحفاظ على الحاوية، التوقيع، CRC، فحص الإصدار، وهوية الجهاز. ملفات CSS وASP وحدها لا تنتج Firmware صالحًا.

## مصادر الفيديو

### واجهة DG8245V-10

- [فيديو واجهة Huawei DG8245V-10](https://www.youtube.com/watch?v=OpyEmUzfObw)
- [صورة مصغرة للفيديو](https://i.ytimg.com/vi/OpyEmUzfObw/hqdefault.jpg)

### واجهات Huawei قريبة للمقارنة

- [واجهة Huawei DN8245V-56 الخاصة بـWE](https://www.youtube.com/watch?v=nvy-lbAZoOU)
- [صورة مصغرة لفيديو DN8245V-56](https://i.ytimg.com/vi/nvy-lbAZoOU/hqdefault.jpg)
- [واجهة Huawei HG8145X6-10](https://www.youtube.com/watch?v=KSQAr6xu4iE)
- [صورة مصغرة لفيديو HG8145X6-10](https://i.ytimg.com/vi/KSQAr6xu4iE/hqdefault.jpg)
- [شرح إعداد Huawei DG8245V](https://www.youtube.com/watch?v=XeGbcQf7-kg)
- [صورة مصغرة لفيديو إعداد DG8245V](https://i.ytimg.com/vi/XeGbcQf7-kg/hqdefault.jpg)

## صور مرجعية

هذه الصور من موضوع عام يعرض استخدام DG8245V-10 كنقطة وصول، وهي مراجع بصرية وإعدادية وليست ملفات Firmware:

- [الصورة المرجعية 1](https://cdn.geekzone.co.nz/imagessubs/c436e1ae5f50f39c59087f52c4a17944.jpg)
- [الصورة المرجعية 2](https://cdn.geekzone.co.nz/imagessubs/703b2c61548ff69dbba65ba0a7537940.jpg)
- [الصورة المرجعية 3](https://cdn.geekzone.co.nz/imagessubs/405e8bc264b543fdf3e04528700c9722.jpg)
- [الصورة المرجعية 4](https://cdn.geekzone.co.nz/imagessubs/90fe2d14475a09d1e8c9ab7cbd54b91a.jpg)
- [موضوع الصور في Geekzone](https://www.geekzone.co.nz/forums.asp?forumid=66&topicid=300542)

## بصمة الملفات

راجع `docs/SHA256SUMS.txt` للتحقق من الملفات المعدلة.
