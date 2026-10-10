# VideoForge AI — GitHub Pages

واجهة عربية RTL لإدارة أدوات فيديو تعمل داخل المتصفح باستخدام HTML وCSS وJavaScript، دون خادم Python.

## النشر على GitHub Pages

1. ارفع محتويات هذا المجلد إلى جذر مستودع GitHub (بحيث يكون `index.html` في الجذر).
2. افتح **Settings → Pages**.
3. في **Build and deployment** اختر **Deploy from a branch**.
4. اختر الفرع `main` والمجلد `/ (root)` ثم اضغط **Save**.
5. انتظر اكتمال النشر وافتح الرابط الذي يعرضه GitHub Pages.

## إضافة أداة جديدة

1. أنشئ ملف JavaScript جديدًا داخل `assets/js/tools/`، مثل `my-tool.js`.
2. صدّر منه دالة `run`:
   ```js
   export async function run({ file }) {
     if (!file) throw new Error("اختر فيديو أولًا.");
     return { title: "نتيجة أداتي", text: `اسم الملف: ${file.name}` };
   }
   ```
3. أضف عنصرًا إلى `TOOLS` في `assets/js/tools/registry.js`:
   ```js
   {
     id: "my-tool",
     name: "اسم الأداة",
     description: "وصف مختصر",
     icon: "✦",
     module: "./my-tool.js",
     needsVideo: true,
     enabled: true
   }
   ```
4. احفظ التغييرات. اجعل `enabled: false` لإخفاء الأداة مؤقتًا.

## حدود النسخة الحالية

- أداة معلومات الفيديو تعمل داخل المتصفح.
- أدوات استخراج الصوت وحذف الصمت والتفريغ الصوتي مجرد هياكل أولية، وليست مفعّلة.
- الطابور مؤقت داخل الصفحة الحالية، ولا يحتفظ بالمهام بعد إعادة تحميلها.
- معالجة الفيديو الثقيلة في المتصفح قد تكون بطيئة وتستهلك الذاكرة. لا تضع مفاتيح API سرية داخل ملفات الموقع العامة.
- الخط من Google Fonts اختياري؛ يعمل الموقع بخط نظام بديل إذا تعذر تحميله.
