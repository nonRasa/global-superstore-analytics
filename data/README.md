# Data

## منبع

داده اولیه از [لینک ارائه‌شده در صورت مسئله](https://drive.google.com/file/d/1KBzL7U2Bt1jEPAENuPw_zIWKcmj9QGnu/view?usp=sharing) دریافت می‌شود.

فایل `Superstore.sql` شامل شش جدول است:

| جدول | سطح داده | کلید اصلی |
|---|---|---|
| `product` | هر محصول | `Product ID` |
| `customer` | هر مشتری | `Customer ID` |
| `order` | هر سفارش | `Order ID` |
| `order_detail` | هر ردیف محصول در سفارش | `Row ID` |
| `returned` | سفارش‌های مرجوع‌شده | `Order ID` |
| `shipping` | اطلاعات ارسال هر سفارش | `Shipping ID` |

## قواعد پوشه‌ها

- `raw/`: فایل‌های اصلی بدون تغییر؛ در Git ذخیره نمی‌شوند.
- `processed/`: خروجی‌های لازم برای آمار، ML یا ورود مجدد به Power BI؛ در Git ذخیره نمی‌شوند.

هیچ فایل خامی را overwrite نکنید. در صورت نیاز، checksum یا تاریخ دریافت را در گزارش تحلیل ثبت کنید.

