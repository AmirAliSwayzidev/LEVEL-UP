# پخته شدن — اپ اندروید + GitHub Actions

نسخه اندروید پروژه «پخته شدن» با workflow ساخت APK روی GitHub.

---

## ساخت APK با GitHub Actions (بدون نصب Android Studio)

### ۱. ساخت ریپازیتوری

1. در GitHub یک Repository جدید بساز (مثلاً `pakhteh-shodan`)
2. محتویات پوشه `Pakhteh-Android` را Push کن:

```bash
cd Pakhteh-Android
git init
git add .
git commit -m "پخته شدن - نسخه اندروید"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/pakhteh-shodan.git
git push -u origin main
```

### ۲. اجرای Workflow

- برو به تب **Actions** در ریپازیتوری
- workflow به نام **Build Android APK** را انتخاب کن
- یا روی **Run workflow** بزن (دستی)

### ۳. دانلود APK

بعد از اتمام سبز شدن job:

1. روی همان run کلیک کن
2. پایین صفحه بخش **Artifacts**
3. فایل **pakhteh-shodan-debug** را دانلود کن
4. از حالت zip خارج کن → `app-debug.apk`
5. روی گوشی نصب کن (منبع ناشناس را موقتاً فعال کن)

---

## ساخت محلی با Android Studio

1. پوشه را در Android Studio باز کن
2. Gradle Sync
3. **Build → Build APK(s)**

---

## Android SDK مورد نیاز (برای ساخت محلی)

| مورد | نسخه |
|------|------|
| JDK | 17 |
| compileSdk | 35 |
| minSdk | 26 |
| targetSdk | 35 |
| Build Tools | 35.0.0 |
| Gradle | 8.7 |

اگر SDK نداری، از Android Studio → SDK Manager این پکیج‌ها را نصب کن.

---

## ساختار مهم

```
Pakhteh-Android/
├── .github/workflows/android.yml   ← ساخت خودکار APK
├── app/src/main/assets/index.html  ← کل اپ (همان پروژه وب)
├── app/src/main/java/.../MainActivity.kt
├── gradlew
└── README.md
```

---

## امضای Release (اختیاری)

در GitHub → Settings → Secrets and variables → Actions این‌ها را اضافه کن:

- `KEYSTORE_BASE64` (فایل jks به صورت base64)
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

و متغیر `ENABLE_SIGNED_RELEASE=true` را در Variables بگذار.

---

پکیج: `com.pakhteshodan.app`  
نام اپ: **پخته شدن**
