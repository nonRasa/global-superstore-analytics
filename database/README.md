# Database and warehouse design

دیتابیس MySQL فقط منبع اولیه Power BI است. پاک‌سازی، ادغام و ساخت Fact/Dimension مطابق صورت مسئله باید با Power Query انجام شود.

مراحل پیشنهادی:

1. ایجاد دیتابیس اختصاصی و اجرای نسخه محلی `Superstore.sql`
2. اتصال Power BI به شش جدول منبع
3. ساخت staging queryها با حالت `Enable load = Off`
4. اجرای بررسی کیفیت، تبدیل نوع‌ها و حذف/مدیریت خطاها در Power Query
5. ساخت Dimensionها و `FactSales`
6. تعریف رابطه‌های یک‌به‌چند و جهت فیلتر یک‌طرفه
7. بررسی uniqueness کلید Dimensionها و orphan keyها

طرح پیشنهادی در [`design/star-schema.md`](design/star-schema.md) آمده است.

