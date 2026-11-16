# مهمة Claude Code: نشر zuhairhd.com

## السياق
- صفحة ثابتة شخصية في `site/`. لا يوجد build — الملفات تُنسخ كما هي.
- الخادم: `165.245.220.86`، Ubuntu + Nginx، **يستضيف مواقع إنتاج أخرى**:
  futuresmartsupport.com، portal/admin/api.futuresmartsupport.com، vpn.zuhairhd.com.
- DNS (GoDaddy) مُحدّث: `A @ → 165.245.220.86`، و`www` CNAME → zuhairhd.com.

## قواعد لا تُكسر
1. لا تعدّل أي ملف Nginx موجود. أضف `zuhairhd.com` فقط.
2. لا تجعل الموقع `default_server`.
3. شغّل `sudo nginx -t` قبل كل reload. إن فشل: توقف، أبلغ، لا تُعِد التحميل.
4. certbot للنطاقين `zuhairhd.com` و`www.zuhairhd.com` فقط. لا تُعِد إصدار شهادات أخرى.
5. لا ترفع إلى المستودع أي بيانات خاصة (تقارير Instagram، أرقام داخلية، مفاتيح، `.env`).
6. توقف واسألني قبل أي خطوة غير مذكورة هنا أو قبل حذف أي شيء على الخادم.

## الخطوات
1. **فحص مسبق (قراءة فقط):**
   - `dig +short zuhairhd.com` يجب أن يعطي `165.245.220.86`.
   - على الخادم: `ls /etc/nginx/sites-enabled/` و`sudo nginx -t` وسجّل الحالة الحالية.
   - سجّل رمز الاستجابة الحالي لكل من: futuresmartsupport.com، portal.، admin.، api.، vpn.zuhairhd.com.
2. **GitHub:** أنشئ مستودعاً عاماً `zuhairhd.com` باسم حسابي، وارفع محتوى هذا المجلد (commit أولي).
3. **النشر:**
   - `sudo mkdir -p /var/www/zuhairhd.com` ثم انسخ محتوى `site/` إليه (rsync أو git clone + rsync).
   - `sudo chown -R www-data:www-data /var/www/zuhairhd.com`
   - انسخ `deploy/nginx/zuhairhd.com.conf` إلى `/etc/nginx/sites-available/zuhairhd.com` وأنشئ symlink في `sites-enabled`.
   - `sudo nginx -t && sudo systemctl reload nginx`
4. **HTTPS:** `sudo certbot --nginx -d zuhairhd.com -d www.zuhairhd.com --redirect`
5. **التحقق:**
   - `curl -I https://zuhairhd.com` → 200، و`http://` → 301 إلى https.
   - `https://www.zuhairhd.com` يعمل، و`/غير-موجود` يعرض 404.html.
   - أعد فحص المواقع الخمسة الأخرى وقارن بالخطوة 1: يجب ألا يتغير شيء.
6. **التقرير:** أنشئ `DEPLOY_REPORT.md` في هذا المجلد يضم: ما نُفّذ، الأوامر، نتائج الفحص قبل وبعد، رابط المستودع، تاريخ انتهاء الشهادة، وأي مشكلة. لا تضع فيه أسراراً.

## تحديثات لاحقة
تعديل في `site/` ← commit ← rsync إلى `/var/www/zuhairhd.com` (لا حاجة لإعادة تحميل Nginx).
