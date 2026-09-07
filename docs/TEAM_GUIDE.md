<div dir="rtl" align="right">

# راهنمای ساده کار تیمی با Git

هر نفر روی branch خودش کار می‌کند و تغییرها بعد از بررسی با Pull Request وارد `main` می‌شوند.

## دریافت پروژه برای اولین بار

ابتدا دعوت GitHub را قبول کنید و سپس:

```bash
git clone https://github.com/yasaman1994/eigenfaces-from-scratch.git
cd eigenfaces-from-scratch
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

فایل `eigenfaces_from_scratch.ipynb` را باز کنید و یک بار Run All بزنید.

## شروع یک کار

ابتدا آخرین نسخه `main` را بگیرید:

```bash
git switch main
git pull --ff-only origin main
```

بعد یک branch با نام روشن بسازید:

```bash
git switch -c shakib/review-pca-math
```

نمونه‌های دیگر:

```text
amin/review-reconstruction-error
saba/compare-distances
```

قبل از ویرایش نوت‌بوک در گروه بگویید روی کدام بخش کار می‌کنید. بهتر است دو نفر هم‌زمان همان فایل نوت‌بوک را تغییر ندهند، چون حل conflict فایل‌های Jupyter سخت است.

## بررسی و commit

بعد از تغییر، نوت‌بوک را از ابتدا اجرا کنید و وضعیت Git را ببینید:

```bash
git status
git diff
```

فقط فایل مربوط به کار خود را اضافه کنید:

```bash
git add eigenfaces_from_scratch.ipynb
git status
git commit -m "Review PCA eigenvalue calculations"
```

پیام commit باید کوتاه و مشخص باشد. نمونه‌های مناسب:

```text
Add face reconstruction and MSE
Compare Euclidean and cosine similarity
Update final results
```

## push و Pull Request

```bash
git branch --show-current
git push -u origin نام-branch
```

در GitHub روی `Compare & pull request` بزنید و کنترل کنید:

- `base` برابر `main` باشد.
- `compare` همان branch شما باشد.
- عنوان بگوید چه چیزی تغییر کرده است.
- در توضیح بنویسید چه چیزی را تغییر دادید و چطور آن را آزمایش کردید.

اگر reviewer ایرادی پیدا کرد، روی همان branch اصلاح، commit و push کنید. Pull Request خودکار به‌روز می‌شود.

بعد از merge:

```bash
git switch main
git pull --ff-only origin main
```

## هر عضو چه بخشی را مرور کند؟

| عضو | بخش اصلی |
|---|---|
| یاسمن | ترتیب کل نوت‌بوک، مستندات، split و data leakage |
| شکیب | Gram matrix، eigenvalue، eigenface و SVD |
| امین | projection، reconstruction و MSE |
| صبا | 1-NN، Euclidean، Cosine و accuracy |

همه اعضا باید مسیر کلی PCA را بفهمند. اگر کسی در بخش خودش ایرادی پیدا کرد، آن را در یک branch کوچک اصلاح می‌کند؛ لازم نیست فقط برای ایجاد commit تغییری غیرضروری انجام دهد.

## قبل از ساخت Pull Request

- [ ] روی branch شخصی هستم.
- [ ] فقط فایل‌های لازم تغییر کرده‌اند.
- [ ] کدی را که تغییر داده‌ام می‌فهمم.
- [ ] نوت‌بوک از ابتدا بدون خطا اجرا می‌شود.
- [ ] داده test وارد mean یا ساخت eigenfaces نشده است.
- [ ] از PCA یا nearest neighbor آماده استفاده نشده است.
- [ ] یک هم‌تیمی تغییر را بررسی می‌کند.

## اگر conflict دیدید

فایل را overwrite نکنید و از `git reset --hard` استفاده نکنید. خروجی `git status`، نام branch و نام فایل را در گروه بفرستید تا با هم حلش کنیم.

## لینک‌های مرتبط

- [معرفی پروژه](../README.md)
- [برنامه و تقسیم کار](PROJECT_PLAN.md)
- [راهنمای آموزشی](LEARNING_GUIDE.md)
- [راهنمای Pull Request در GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

</div>
