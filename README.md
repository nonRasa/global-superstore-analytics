# Global Superstore Analytics

یک پروژه تحلیلی سرتاسری برای داده‌های Global Superstore، شامل انبار داده، آمار، یادگیری ماشین و داشبورد Power BI.

## هدف پروژه

این ریپو چهار خروجی اصلی را پوشش می‌دهد:

1. ورود داده خام به MySQL و ساخت مدل ستاره‌ای در Power BI/Power Query
2. آزمون آماری اثر تخفیف بر تعداد کالای فروخته‌شده
3. پیش‌بینی `Profit` (رگرسیون) و `Ship Mode` (طبقه‌بندی)
4. ساخت داشبورد مدیریتی و ارائه پیشنهادهای اجرایی

> طبق صورت مسئله، عملیات پاک‌سازی، آماده‌سازی و ساخت جداول Fact/Dimension باید در Power BI انجام شود. پایتون فقط برای فاز آمار و یادگیری ماشین استفاده می‌شود.

## شروع سریع

```powershell
git clone <repository-url>
cd <repository-name>
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
```

سپس داده اولیه را از [لینک صورت مسئله](https://drive.google.com/file/d/1KBzL7U2Bt1jEPAENuPw_zIWKcmj9QGnu/view?usp=sharing) دریافت کنید. فایل‌های خام عمداً وارد Git نمی‌شوند؛ توضیحات در [`data/README.md`](data/README.md) آمده است.

## ساختار پروژه

```text
.
├── .github/                 # قالب Issue و Pull Request
├── data/                    # راهنمای داده خام و خروجی‌های پردازش‌شده
├── database/                # مستندات دیتابیس و طراحی مدل ستاره‌ای
├── docs/                    # برنامه، تصمیم‌ها و مستندات پروژه
├── models/                  # مدل‌های آموزش‌دیده (در Git ذخیره نمی‌شوند)
├── notebooks/               # نوت‌بوک‌های آمار و یادگیری ماشین
├── powerbi/                 # فایل PBIX، Power Query و DAX
├── reports/                 # شکل‌ها، معیارها و خروجی‌های ارائه
├── src/superstore/          # کد قابل استفاده مجدد پایتون
└── tests/                   # تست‌های کد پایتون
```

جزئیات مدل پیشنهادی در [`database/design/star-schema.md`](database/design/star-schema.md) و گردش‌کار تیم در [`CONTRIBUTING.md`](CONTRIBUTING.md) ثبت شده است.

## ترتیب اجرای کار

- `01`: بررسی کیفیت داده و طراحی مدل در Power BI
- `02`: آزمون فرض اثر تخفیف بر Quantity
- `03`: مدل رگرسیون Profit
- `04`: مدل طبقه‌بندی Ship Mode
- `05`: ادغام خروجی‌ها با Power BI و ساخت داشبورد
- `06`: مرور نهایی، ثبت یافته‌ها و آماده‌سازی ارائه

## وضعیت فعلی

- [x] دریافت فایل خام و شناسایی شش جدول منبع
- [x] طراحی ساختار اولیه ریپو
- [ ] ساخت و اعتبارسنجی مدل ستاره‌ای در Power BI
- [ ] تحلیل آماری
- [ ] مدل‌های یادگیری ماشین
- [ ] داشبورد و ارائه نهایی
