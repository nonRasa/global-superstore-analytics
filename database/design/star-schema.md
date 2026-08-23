# Proposed star schema

## Grain

هر سطر `FactSales` نشان‌دهنده فروش یک محصول در یک سفارش است و از `order_detail[Row ID]` مشتق می‌شود.

## FactSales

| ستون | نقش |
|---|---|
| `SalesKey` | کلید یکتای fact؛ مبتنی بر `Row ID` |
| `OrderID` | Degenerate dimension برای drill-through سفارش |
| `ProductKey` | ارتباط با `DimProduct` |
| `CustomerKey` | ارتباط با `DimCustomer` |
| `OrderDateKey` | ارتباط role-playing با `DimDate` |
| `ShipDateKey` | ارتباط role-playing با `DimDate` |
| `GeographyKey` | ارتباط با `DimGeography` |
| `ShipModeKey` | ارتباط با `DimShipMode` |
| `MarketKey` | ارتباط با `DimMarket` |
| `PriorityKey` | ارتباط با `DimOrderPriority` |
| `Sales` | مبلغ فروش |
| `Quantity` | تعداد |
| `Discount` | نرخ تخفیف |
| `Profit` | سود |
| `ShippingCost` | هزینه ارسال |
| `ShippingDays` | اختلاف روز ارسال و سفارش |
| `IsReturned` | پرچم مرجوعی |

## Dimensions

- `DimProduct`: محصول، دسته و زیردسته
- `DimCustomer`: مشتری و Segment
- `DimDate`: تاریخ، سال، فصل، ماه، نام ماه، هفته، روز هفته، روز کاری/تعطیل
- `DimGeography`: شهر، استان، کشور، Region و در صورت امکان Latitude/Longitude
- `DimShipMode`: روش ارسال و رتبه سرعت/سطح سرویس
- `DimMarket`: بازار و گروه‌بندی جغرافیایی پیشنهادی
- `DimOrderPriority`: اولویت سفارش و رتبه آن

## Relationships

تمام رابطه‌ها از Dimension به Fact، یک‌به‌چند و با جهت فیلتر یک‌طرفه باشند. برای دو نقش تاریخ، یک رابطه فعال و Measureهای نقش دوم با `USERELATIONSHIP` یا دو نسخه role-playing از `DimDate` استفاده شود.

## Power Query quality checks

- یکتایی کلیدهای اصلی و نبود `null` در آن‌ها
- تطابق `Order ID` و `Product ID` در جدول جزئیات با جدول‌های مرجع
- بررسی مقادیر منفی یا غیرمنطقی در Sales، Quantity و Shipping Cost
- بررسی بازه Discount و مقادیر پرت Profit
- بررسی `Ship Date >= Order Date`
- استانداردسازی متن Country، State، City، Region و Ship Mode
- ثبت تعداد ردیف قبل و بعد از هر حذف یا deduplication

