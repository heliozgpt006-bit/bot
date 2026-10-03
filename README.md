# OussaWeb Bot — الترسانة الرقمية الجزائرية على تيليغرام

## ⚠️ أولًا: أعد توليد التوكن!
التوكن الذي أُرسل هنا أصبح مكشوفًا (ظهر في محادثة). أي شخص يملكه يتحكم بالبوت:
1. افتح @BotFather في تيليغرام
2. أرسل `/revoke` ← اختر بوتك ← سيعطيك توكنًا جديدًا فورًا
3. استعمل الجديد في الخطوات أدناه والقَديم ميت نهائيًا

## التشغيل المحلي (دقيقتان)
```bash
pip install -r requirements.txt
export BOT_TOKEN="توكنك_الجديد"     # ويندوز: set BOT_TOKEN=توكنك
python bot.py
```

## تفعيل الوضع المضمّن (بحث فوري داخل أي محادثة)
@BotFather ← `/setinline` ← اختر بوتك ← أرسل اسم مستخدم البوت أو نصًا مثل `oussaweb`

## الاستضافة المجانية المُوصى بها: Render (الأسهل)
1. أنشئ حسابًا على github.com ← أنشئ مستودعًا جديدًا ← ارفع الملفات الثلاثة
   (يمكن من المتصفح: Add file → Upload files)
2. على render.com سجّل بحساب GitHub ← New ← Web Service ← اختر المستودع
3. الإعدادات: Runtime=Python 3، Build Command:
   `pip install -r requirements.txt`
   Start Command:
   `python bot.py`
4. Environment Variables ← أضف: Key=`BOT_TOKEN` Value=توكنك الجديد ← Deploy
5. بعد دقيقتين البوت يعمل ✅ الرابط `xxx.onrender.com` يعمل أيضًا للفحص

⚠️ الخطة المجانية تنام بعد 15 دقيقة خمول — الحل المجاني:
- افتح cron-job.org ← Create job ← الرابط: `https://اسم-خدمتك.onrender.com`
  (فعّل ping كل 10 دقائق — Render يوقظ الخدمة فورًا)
- ملاحظة أمان: أضف في bot.py سطر استجابة بسيطًا، أو استخدم مسار `/` يعيد 200 —
  الحل الأبسط: استبدل `app.run_polling` بنمط webhook إن أردت؛ لكن للبوتات، polling + ping كافٍ تمامًا.
- تيليغرام يحتفظ بالرسائل 24 ساعة، فعند الاستيقاع يستلم البوت كل ما فاته.

## بديل مجاني دائم التشغيل: Hugging Face Spaces
1. huggingface.co ← New Space ← SDK: Docker
2. ارفع الملفات + أضف `Dockerfile`:
   ```
   FROM python:3.12-slim
   WORKDIR /app
   COPY . .
   RUN pip install -r requirements.txt
   CMD ["python","bot.py"]
   ```
3. Settings ← Secrets ← `BOT_TOKEN`
المساحات تنام عند الخمول أيضًا — أضف ping من cron-job.org نفسه.

## الأوامر
`/search /guide /rates /convert /prayer /check /fav /setkey /ai /cancel`
أو ببساطة: اكتب أي كلمة (باسبور، الشومي، بريدي نت…) — وفي أي محادثة: `@اسم_بوتك باسبور`

## الأمان
- التوكن في متغير بيئة فقط — لا تضعه داخل الكود أبدًا
- مفاتيح AI تُحفظ لكل مستخدم في SQLite محلي على السيرفر
- قاعدة البيانات `oussaweb.db` — خذ نسخة منها دوريًا (فهي ذاكرة المفضلة والإنجازات)
