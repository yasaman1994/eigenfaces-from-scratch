<div dir="rtl" align="right">

# راهنمای همکاری تیمی

این فایل می‌گوید هر عضو تیم از لحظه دریافت دعوت GitHub تا تحویل Pull Request دقیقاً چه کاری انجام دهد. هدف ما یک روش ساده، قابل‌آموزش و کم‌خطر برای همکاری روی یک نوت‌بوک مشترک است.

## اعضا و مسئولیت‌ها

| عضو | حساب GitHub | مسئولیت اصلی |
|---|---|---|
| یاسمن | [@yasaman1994](https://github.com/yasaman1994) | هماهنگی، مستندات، کنترل data leakage، ادغام تغییرها و اجرای نهایی |
| شکیب | [@Shakib1380](https://github.com/Shakib1380) | بازبینی ریاضی PCA، covariance، eigendecomposition و مقایسه با SVD |
| امین | [@Aminbyt](https://github.com/Aminbyt) | projection، reconstruction، خطای بازسازی و نمودارها |
| صبا | [@SabaHesaraki](https://github.com/SabaHesaraki) | nearest neighbor، معیارهای Euclidean و Cosine و accuracy |

تقسیم کار به معنی جداشدن دانش نیست. همه اعضا باید مسیر کامل پروژه را بفهمند و بتوانند در ارائه توضیح دهند. شکیب بازبین اصلی ریاضیات است، نه تنها فرد مسئول یادگیری ریاضیات.

## قانون‌های اصلی تیم

1. هیچ‌کس مستقیماً روی `main` کد جدید push نمی‌کند.
2. هر branch فقط برای یک کار مشخص ساخته می‌شود.
3. پیش از ساخت branch جدید، آخرین نسخه `main` دریافت می‌شود.
4. هر تغییر با Pull Request بررسی می‌شود و بعد وارد `main` می‌شود.
5. در هر لحظه فقط یک نفر نسخه نهایی نوت‌بوک را ویرایش می‌کند.
6. قبل از ویرایش نوت‌بوک، عضو تیم در گروه نام branch و بخش موردنظر را اعلام می‌کند.
7. از PCA و nearest neighbor آماده استفاده نمی‌کنیم.
8. داده test در محاسبه mean، eigenfaces یا انتخاب پارامترهای مدل وارد نمی‌شود.
9. رمز عبور، token، فایل محیط مجازی و تنظیمات شخصی IDE نباید commit شوند.
10. هر عضو باید کدی را که تحویل می‌دهد، خط‌به‌خط بفهمد.

## مرحله صفر: قبول‌کردن دعوت

یاسمن ابتدا اعضا را از صفحه تنظیمات repository دعوت می‌کند. هر عضو باید دعوت را از ایمیل یا اعلان GitHub قبول کند. چون repository خصوصی است، clone پیش از قبول دعوت ممکن نیست.

## مرحله یک: دریافت پروژه برای اولین بار

هر عضو فقط یک بار این دستورها را در Terminal اجرا می‌کند:

```bash
git clone https://github.com/yasaman1994/eigenfaces-from-scratch.git
cd eigenfaces-from-scratch
```

سپس محیط مجازی و کتابخانه‌ها ساخته می‌شوند:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

بعد فایل `eigenfaces_from_scratch.ipynb` را در PyCharm یا Jupyter باز کنید. یک بار همه سلول‌ها را از ابتدا اجرا کنید تا مطمئن شوید نسخه اولیه روی سیستم شما کار می‌کند.

## مرحله دو: شروع یک کار جدید

ابتدا به `main` بروید و آن را به‌روز کنید:

```bash
git switch main
git pull origin main
```

حالا branch مخصوص کار خود را بسازید. نام branch باید شامل نام شخص و موضوع کار باشد.

نمونه برای شکیب:

```bash
git switch -c shakib/review-pca-math
```

نمونه برای امین:

```bash
git switch -c amin/add-reconstruction
```

نمونه برای صبا:

```bash
git switch -c saba/compare-distances
```

پس از این دستور، تغییرها فقط در branch شما قرار می‌گیرند و `main` دست‌نخورده باقی می‌ماند.

## مرحله سه: انجام و بررسی تغییر

کار را در بخش تعیین‌شده انجام دهید. سپس نوت‌بوک را از ابتدا اجرا کنید و این دو دستور را ببینید:

```bash
git status
git diff
```

پیش از commit بررسی کنید:

- فقط فایل‌های مربوط به همان کار تغییر کرده باشند.
- سلول‌ها به ترتیب اجرا شوند.
- خروجی شکل‌ها و متغیرها منطقی باشد.
- کد آماده PCA یا nearest neighbor اضافه نشده باشد.
- توضیح کوتاه و قابل‌فهم برای تصمیم مهم وجود داشته باشد.

نکته: نمایش تغییرهای فایل Jupyter در Terminal همیشه خوانا نیست. در این حالت `git status` را بررسی کنید و نوت‌بوک را داخل PyCharm یا Jupyter مرور کنید.

## مرحله چهار: commit

فقط فایل موردنظر را stage کنید. برای مثال:

```bash
git add eigenfaces_from_scratch.ipynb
git status
```

اگر فهرست فایل‌ها درست بود، commit بسازید:

```bash
git commit -m "Add SVD comparison"
```

نمونه پیام‌های خوب:

```text
Review PCA eigenvalue calculations
Add face reconstruction and MSE
Compare Euclidean and cosine similarity
Update final results and documentation
```

پیام‌هایی مانند `change`، `final` یا `fix` مشخص نمی‌کنند چه کاری انجام شده است.

## مرحله پنج: push کردن branch

نام branch فعلی را با این دستور ببینید:

```bash
git branch --show-current
```

سپس همان branch را push کنید. مثال:

```bash
git push -u origin shakib/review-pca-math
```

در pushهای بعدی همان branch، دستور کوتاه زیر کافی است:

```bash
git push
```

## مرحله شش: ساخت Pull Request

1. صفحه repository را در GitHub باز کنید.
2. روی `Compare & pull request` کلیک کنید.
3. مطمئن شوید مقصد یا `base` برابر `main` است.
4. مطمئن شوید مبدأ یا `compare` همان branch شماست.
5. عنوان روشن و توضیح کوتاه بنویسید.
6. Pull Request را بسازید و از یک هم‌تیمی review بخواهید.

قالب پیشنهادی توضیح Pull Request:

```text
What did I change?
- ...

How did I test it?
- Restarted the kernel and ran the notebook
- Checked ...

What should the reviewer check?
- ...
```

یاسمن پس از review و رفع اشکال، Pull Request را در `main` merge می‌کند. اگر reviewer ایرادی پیدا کرد، صاحب branch اصلاح را روی همان branch commit و push می‌کند؛ Pull Request به‌صورت خودکار به‌روز می‌شود.

## مرحله هفت: بعد از merge

پس از اعلام merge، عضو تیم نسخه محلی خود را به‌روز می‌کند:

```bash
git switch main
git pull origin main
```

اگر branch دیگر لازم نیست، حذف محلی آن اختیاری است:

```bash
git branch -d shakib/review-pca-math
```

فقط نام branch خودتان را جایگزین کنید. branch ادغام‌نشده را با `-D` حذف نکنید.

## ترتیب پیشنهادی کار روی نوت‌بوک

فایل Jupyter یک فایل JSON بزرگ است و ادغام تغییر هم‌زمان چند نفر روی آن دشوار می‌شود. بنابراین نسخه نهایی نوت‌بوک را با این ترتیب جلو می‌بریم:

1. شکیب بخش ریاضی فعلی، Gram matrix، eigendecomposition و مقایسه SVD را بازبینی می‌کند.
2. Pull Request شکیب review و merge می‌شود.
3. امین آخرین `main` را دریافت و projection، reconstruction و error را اضافه می‌کند.
4. Pull Request امین review و merge می‌شود.
5. صبا آخرین `main` را دریافت و nearest neighbor و مقایسه معیارها را اضافه می‌کند.
6. Pull Request صبا review و merge می‌شود.
7. یاسمن کل پروژه را یکپارچه، مستند و از ابتدا اجرا می‌کند.

اعضا می‌توانند مطالعه، محاسبه روی کاغذ یا آزمایش در فایل موقت را هم‌زمان انجام دهند؛ اما تغییر نهایی نوت‌بوک طبق ترتیب بالا انجام می‌شود. فایل موقت فقط در صورت نیاز و با توافق تیم وارد repository شود.

## خروجی مورد انتظار هر مسئولیت

### شکیب: بازبینی ریاضی

- بررسی شکل تمام ماتریس‌ها
- بررسی متقارن‌بودن Gram matrix
- مرتب‌سازی eigenvalueها به‌صورت نزولی
- حذف مؤلفه‌های صفر یا بسیار کوچک
- نرمال و تقریباً متعامدبودن eigenfaceها
- توضیح ارتباط SVD با eigenvalueها
- مقایسه subspace یا reconstruction به‌جای مقایسه علامت خام eigenvectorها

علامت یک eigenvector می‌تواند برعکس شود و همچنان همان پاسخ ریاضی باشد؛ پس برابری علامت شرط درستی نیست.

### امین: فشرده‌سازی و بازسازی

- projection با ضرب ماتریسی NumPy
- reconstruction برای `k = 10, 50, 150`
- نمایش تصویر اصلی و تصاویر بازسازی‌شده
- محاسبه MSE برای چند مقدار `k`
- بررسی اینکه خطای بازسازی با افزایش `k` بیشتر نشود
- نمودار cumulative explained variance و error

### صبا: تشخیص هویت

- پیاده‌سازی nearest neighbor بدون مدل آماده
- فاصله Euclidean با انتخاب کمترین مقدار
- شباهت Cosine با انتخاب بیشترین مقدار
- جلوگیری از تقسیم بر صفر در Cosine
- محاسبه accuracy فقط روی test
- نمایش نمونه موفق، نمونه شکست و موارد اختلاف دو معیار

### یاسمن: یکپارچه‌سازی

- بررسی اینکه split پیش از یادگیری پارامترها انجام شده باشد
- بررسی اینکه mean و eigenfaces فقط از train آمده باشند
- هماهنگ‌کردن متن‌ها، نام متغیرها و نمودارها
- اجرای `Restart Kernel and Run All`
- کنترل فایل‌های خروجی و آماده‌سازی ارائه و ZIP نهایی

## اگر conflict رخ داد

1. ادامه ندهید و فایل را کورکورانه overwrite نکنید.
2. خروجی `git status` را در گروه بفرستید.
3. نام branch و فایل دارای conflict را اعلام کنید.
4. با یاسمن و صاحب آخرین تغییر هماهنگ کنید.
5. از دستورهای مخرب مانند `git reset --hard` استفاده نکنید.

پیشگیری از conflict بسیار ساده‌تر از حل conflict نوت‌بوک است؛ به همین دلیل ترتیب کار بالا مهم است.

## چک‌لیست Pull Request

- [ ] کار فقط در branch شخصی انجام شده است.
- [ ] `main` پیش از ساخت branch به‌روز بوده است.
- [ ] فقط فایل‌های لازم تغییر کرده‌اند.
- [ ] نویسنده تمام کد اضافه‌شده را می‌فهمد.
- [ ] نوت‌بوک بدون خطا از ابتدا اجرا شده است.
- [ ] shapeها و نتیجه‌های مهم بررسی شده‌اند.
- [ ] هیچ داده test وارد مرحله آموزش نشده است.
- [ ] عنوان و توضیح Pull Request روشن است.
- [ ] حداقل یک هم‌تیمی تغییر را review کرده است.

## اولین پیام پیشنهادی در گروه

```text
من روی بخش ... کار می‌کنم.
نام branch من ... است.
فایل نوت‌بوک از الان تا زمان ساخت Pull Request در اختیار من است.
وقتی کار تمام شد در گروه خبر می‌دهم.
```

## منابع داخل پروژه

- [معرفی و اجرای پروژه](../README.md)
- [برنامه سه‌روزه و معیارهای تحویل](PROJECT_PLAN.md)
- [دلیل تصمیم‌ها و آموزش ریاضی](LEARNING_GUIDE.md)

## منابع رسمی GitHub

- [راهنمای clone کردن repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
- [راهنمای مدیریت branchها](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository)
- [راهنمای ساخت Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

</div>
