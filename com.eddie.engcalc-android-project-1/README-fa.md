# ماشین‌حساب مهندسی — راهنمای ساخت APK

## ۱) پوش کردن پروژه به گیت‌هاب
یه ریپوی خالی بساز، بعد:
```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin <لینک ریپو>
git push -u origin main
```
یا از اپلیکیشن GitHub موبایل یا Working Copy هم می‌تونی آپلود کنی.

## ۲) گرفتن APK دیباگ
بعد از پوش، برو به تب **Actions** همون ریپو. ورک‌فلوی Build APK خودکار اجرا می‌شه.
وقتی تموم شد، پایین صفحه‌ی اجرا، دو فایل **app-debug-apk** و **app-release-apk** هست — دانلودشون کن (zip هستن، داخلشون APK واقعیه).
نسخه‌ی دیباگ همیشه قابل نصبه، فقط برای توزیع عمومی امضای رسمی نداره.

## ۳) ساخت نسخه‌ی امضاشده (release) واقعی
یه keystore بساز:
```
keytool -genkey -v -keystore release.keystore -alias engcalc -keyalg RSA -keysize 2048 -validity 10000
```
بعد توی تنظیمات ریپو > Settings > Secrets and variables > Actions این‌ها رو اضافه کن:
- `KEYSTORE_BASE64` → خروجی `base64 -w0 release.keystore`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

دفعه‌ی بعد که پوش کنی، APK نسخه‌ی release واقعاً امضاشده می‌شه.

## محدودیت‌های فعلی
- آیکون فقط در ۵ دانسیتی استاندارد ساخته شده (بدون آیکون تطبیقی/Adaptive).
- پروژه به فونت گوگل از اینترنت وصل می‌شه؛ دسترسی اینترنت روشن نگه داشته شده.
- کامپایل واقعی فقط روی سرور GitHub Actions انجام می‌شه.
