<div dir="rtl" align="right">

# تشخیص هویت چهره با Eigenfaces و پیاده‌سازی PCA از صفر

پروژه ریاضی دوره مهندسی یادگیری ماشین رهنماکالج - تیم ۴

## معرفی پروژه

در این پروژه می‌خواهیم بررسی کنیم آیا می‌توان یک تصویر چهره `64×64` را به‌جای ۴۰۹۶ مقدار پیکسل، با تعداد بسیار کمتری عدد نمایش داد و همچنان اطلاعات لازم برای بازسازی تصویر و تشخیص هویت را حفظ کرد.

برای رسیدن به این هدف، تحلیل مؤلفه‌های اصلی را مرحله‌به‌مرحله و با فرمول‌های ریاضی پیاده‌سازی می‌کنیم. ابزار محاسباتی ما نام‌پای است و از پیاده‌سازی آماده تحلیل مؤلفه‌های اصلی استفاده نمی‌کنیم.

| اصطلاح فارسی | نام فنی |
|---|---|
| تحلیل مؤلفه‌های اصلی | `Principal Component Analysis (PCA)` |
| نام‌پای | `NumPy` |
| چهره ویژه | `Eigenface` |

## سؤال اصلی

چند مؤلفه اصلی برای ساختن یک نمایش فشرده و قابل‌استفاده از چهره‌ها کافی است؟

## سؤال اختصاصی تیم ۴: تعریف شباهت

آیا انتخاب معیار شباهت در فضای مؤلفه‌های اصلی باعث تغییر نزدیک‌ترین همسایه و دقت تشخیص هویت می‌شود؟

در آزمایش اختصاصی تیم، دو معیار زیر را مقایسه می‌کنیم:

- فاصله اقلیدسی: `Euclidean distance`
- شباهت کسینوسی: `Cosine similarity`

### فرضیه اولیه

شباهت کسینوسی ممکن است نسبت به تفاوت اندازه بردارهای فشرده، مانند برخی تغییرات روشنایی و شدت، حساسیت کمتری داشته باشد. از طرف دیگر، فاصله اقلیدسی اطلاعات مربوط به اندازه اختلاف را نیز حفظ می‌کند و ممکن است برای بعضی چهره‌ها بهتر عمل کند. نتیجه نهایی فقط بر اساس دقت، همسایه‌های انتخاب‌شده و نمونه‌های شکست گزارش خواهد شد.

## دیتاست

از دیتاست Olivetti Faces استفاده می‌کنیم:

- ۴۰۰ تصویر خاکستری
- ۴۰ هویت متفاوت
- ۱۰ تصویر برای هر هویت
- ابعاد هر تصویر: `64×64`
- تعداد ویژگی‌های هر تصویر پس از flatten: `4096`

دیتاست فقط با `sklearn.datasets.fetch_olivetti_faces` دریافت می‌شود. برای PCA یا nearest neighbor از پیاده‌سازی آماده scikit-learn استفاده نمی‌کنیم.

## روش جداسازی داده

برای هر هویت:

- ۸ تصویر برای train
- ۲ تصویر برای test

انتخاب تصاویر به‌صورت تصادفی و stratified با `random seed` ثابت انجام می‌شود تا اجرای پروژه تکرارپذیر باشد. تمام پارامترهای یادگرفتنی، از جمله mean face و eigenfaces، فقط از داده train محاسبه می‌شوند.

## مسیر اجرای پروژه

1. دریافت و بررسی دیتاست
2. جداسازی train و test پیش از یادگیری هر پارامتر
3. تبدیل تصویرهای `64×64` به بردارهای ۴۰۹۶بعدی
4. محاسبه mean face فقط از داده train
5. مرکزسازی train و test با همان train mean
6. ساخت covariance matrix یا Gram matrix
7. محاسبه eigenvalues و eigenvectors با `numpy.linalg.eigh`
8. مرتب‌سازی مؤلفه‌ها بر اساس eigenvalue نزولی
9. تبدیل بردارهای ویژه به eigenfaces
10. projection تصویرها به فضای `k`بعدی
11. reconstruction برای `k = 10, 50, 150`
12. محاسبه reconstruction error
13. پیاده‌سازی nearest neighbor از صفر
14. محاسبه accuracy فقط روی test
15. مقایسه حداقلی با مسیر `numpy.linalg.svd`
16. مقایسه Euclidean distance و Cosine similarity برای تیم ۴
17. تحلیل نمونه‌های موفق، شکست‌ها و محدودیت‌ها

## محدودیت‌های پیاده‌سازی

### مجاز

- NumPy برای محاسبات عددی
- Matplotlib برای نمودار و نمایش تصویر
- scikit-learn فقط برای دریافت دیتاست
- `numpy.linalg.eigh`
- `numpy.linalg.svd`

### غیرمجاز

- `sklearn.decomposition.PCA`
- پیاده‌سازی آماده nearest neighbor
- استفاده از داده test برای محاسبه mean، مؤلفه‌ها یا انتخاب پارامترهای مدل

## خروجی‌های مورد انتظار

- نمونه‌هایی از داده و نمایش شکل ماتریس‌ها
- mean face
- مجموعه‌ای از eigenfaceها
- نمودار cumulative explained variance
- تصویر اصلی و reconstruction برای `k = 10, 50, 150`
- نمودار reconstruction error برحسب `k`
- accuracy تشخیص روی test
- حداقل یک تشخیص موفق و یک تشخیص ناموفق
- مقایسه مختصر eigendecomposition و SVD
- دقت Euclidean و Cosine
- نمونه‌هایی که دو معیار همسایه‌های متفاوتی انتخاب کرده‌اند
- یک نتیجه قابل‌دفاع و یک محدودیت واقعی

## ساختار پروژه

```text
eigenfaces-from-scratch/
├── README.md
├── requirements.txt
├── .gitignore
├── eigenfaces_from_scratch.ipynb
├── docs/
│   ├── PROJECT_PLAN.md
│   ├── LEARNING_GUIDE.md
│   └── TEAM_GUIDE.md
└── outputs/
    └── figures/
```

نوت‌بوک اصلی باید از ابتدا تا انتها با Run All و بدون مرحله دستی پنهان اجرا شود. تصاویر نهایی مورد استفاده در گزارش یا ارائه در `outputs/figures/` ذخیره می‌شوند.

## نصب و اجرا

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

سپس فایل `eigenfaces_from_scratch.ipynb` را باز و Run All کنید.

## اعضای تیم

| عضو | GitHub username | مسئولیت پیشنهادی |
|---|---|---|
| یاسمن | [@yasaman1994](https://github.com/yasaman1994) | یکپارچه‌سازی، مستندسازی، کنترل data leakage و اجرای نهایی |
| شکیب | [@Shakib1380](https://github.com/Shakib1380) | بازبینی ریاضی PCA، covariance، eigendecomposition و مقایسه با SVD |
| امین | [@Aminbyt](https://github.com/Aminbyt) | projection، reconstruction، خطای بازسازی و نمودارها |
| صبا | [@SabaHesaraki](https://github.com/SabaHesaraki) | nearest neighbor و مقایسه Euclidean/Cosine |

این تقسیم کار پیشنهادی است. همه اعضا باید مسیر کامل پروژه را درک کنند و Pull Request یکدیگر را مرور کنند.

## روش همکاری تیمی

- شاخه `main` همیشه باید قابل‌اجرا باقی بماند.
- هر کار در یک branch جدا انجام می‌شود.
- نام branch روشن و مرتبط با کار انتخاب می‌شود؛ مانند `amin/pca-math`.
- commitها کوچک و دارای پیام مشخص هستند.
- تغییرها با Pull Request بررسی و سپس وارد `main` می‌شوند.
- پیش از شروع کار جدید، آخرین نسخه `main` دریافت می‌شود.
- برای کاهش conflict، دو نفر هم‌زمان یک بخش از نوت‌بوک را ویرایش نمی‌کنند.

دستورهای دقیق clone، branch، commit، push و Pull Request در [راهنمای همکاری تیم](docs/TEAM_GUIDE.md) آمده است. جزئیات برنامه و Definition of Done در [برنامه پروژه](docs/PROJECT_PLAN.md) نوشته شده است. دلیل تصمیم‌ها، فرمول‌ها، روش راستی‌آزمایی و ممیزی نوت‌بوک نیز در [راهنمای آموزشی](docs/LEARNING_GUIDE.md) قرار دارد.

## وضعیت فعلی

- [x] دریافت و بررسی دیتاست
- [x] flatten تصاویر
- [x] جداسازی تصادفی و متوازن train و test با seed ثابت
- [x] mean face و مرکزسازی
- [x] واریانس و کوواریانس
- [x] Gram matrix و eigendecomposition
- [x] نمایش اولیه eigenfaces
- [ ] projection و reconstruction
- [ ] reconstruction error
- [ ] nearest neighbor و accuracy
- [ ] مقایسه SVD
- [ ] آزمایش اختصاصی Euclidean/Cosine
- [ ] تحلیل موفقیت‌ها و شکست‌ها
- [ ] اجرای نهایی و آماده‌سازی ارائه

## وضعیت پروژه

این پروژه آموزشی و در حال توسعه است.

</div>
