# zuhairhd.com

الصفحة الشخصية لـ **زهير درويش** — تحليل سياسي واقتصادي. صفحة روابط ثابتة تحل محل Linktree في Instagram (@zuhairhd).

## البنية
```
site/                 الملفات المنشورة على الخادم
  index.html          الصفحة الرئيسية (عربية، RTL، بلا مكتبات)
  404.html            صفحة الخطأ
  robots.txt, sitemap.xml
  assets/             avatar.jpg، og-image.png، favicon.svg، apple-touch-icon.png
deploy/nginx/         إعداد Nginx للنطاق
CLAUDE.md             تعليمات النشر لـ Claude Code
```

## تعديل الروابط
كل رابط بلوك `<a class="item">` في `site/index.html`. انسخ بلوكاً وعدّل الرابط والعنوان.

## النشر
الخادم: 165.245.220.86 (Nginx). المسار: `/var/www/zuhairhd.com`. التفاصيل في `CLAUDE.md`.
