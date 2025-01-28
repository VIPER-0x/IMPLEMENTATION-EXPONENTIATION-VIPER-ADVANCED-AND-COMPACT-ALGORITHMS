پیاده‌سازی الگوریتم‌های پیشرفته و فشرده VIPER برای نمایی‌سازی (Exponentiation)
این کد یک اسکریپت Pine Script است که در پلتفرم TradingView برای تحلیل داده‌های مالی استفاده می‌شود. هدف اصلی این کد پیاده‌سازی الگوریتم‌های پیشرفته و فشرده برای محاسبه تعداد ارقام اعشاری (Decimals) در مقادیر ورودی است. همچنین، این کد شامل نمایش داده‌های مختلف در قالب جدول‌های گرافیکی برای مقایسه خروجی الگوریتم‌ها است.

توضیح بخش‌های مختلف کد:
1. تنظیمات اولیه
pinescript
//@version=6  
indicator(title = 'IMPLEMENTATION EXPONENTIATION VIPER ADVANCED AND COMPACT ALGORITHMS', shorttitle = 'IMPLEMENTATION EXPONENTIATION ', overlay = false)  
src = close * math.pow(10, 9)  
نسخه اسکریپت 6 است.
عنوان اندیکاتور و تنظیمات اولیه مشخص شده است.
مقدار src برابر با قیمت بسته شدن (Close) ضربدر توان 10 به توان 9 محاسبه شده است.
2. الگوریتم پیشرفته (Extended Algorithm)
pinescript
VIPER_ADVANCED_DECIMAL_ALGORITHM_EXTENDED(_value) =>   
    decimals = int(na)  
    to5tring = str.tostring(_value)  
    validate = not na(str.tonumber(to5tring))  
    if not validate  
        decimals := int(na)  
        decimals  
    else if validate  
        getRadix = str.pos(to5tring, '.')  
        if na(getRadix)  
            decimals := 0  
            decimals  
        else  
            toSubstr = str.substring(to5tring, getRadix + 1)  
            decimals := str.length(toSubstr)  
            decimals  
این الگوریتم تعداد ارقام اعشاری یک مقدار ورودی (که می‌تواند عدد صحیح، اعشاری یا رشته باشد) را محاسبه می‌کند.
ابتدا مقدار ورودی به رشته تبدیل می‌شود.
بررسی می‌شود که آیا مقدار معتبر است یا خیر.
اگر مقدار معتبر باشد، موقعیت نقطه اعشار (.) شناسایی شده و تعداد ارقام بعد از آن محاسبه می‌شود.
3. الگوریتم فشرده (Compact Algorithm)
pinescript
VIPER_ADVANCED_DECIMAL_ALGORITHM_COMPACT(_in) =>  
    n = int(na)  
    s = str.tostring(_in)  
    p = str.pos(s, '.')  
    n := na(str.tonumber(s)) ? int(na) : na(p) ? 0 : str.length(str.substring(s, p + 1))  
    n  
نسخه فشرده الگوریتم بالا است که با خطوط کمتری نوشته شده است.
عملکرد مشابهی دارد و تعداد ارقام اعشاری را محاسبه می‌کند.
4. مقادیر نمونه (Example Values)
pinescript
float cnt0 = float(0.12345678901234567890)  
var int cnt1 = int(123456789012345678901)  
string cnt2 = '0.12345678901234567890'  
string cnt3 = '123456789012345678901'  
مقادیر نمونه‌ای از انواع مختلف داده (اعشاری، صحیح و رشته) تعریف شده‌اند.
این مقادیر برای تست الگوریتم‌ها استفاده می‌شوند.
5. خروجی به صورت جدول
pinescript
if barstate.islast  
    var VIPER_PANEL = table.new(position.top_center, 8, 18, bgcolor = color.rgb(0, 0, 255), border_color = #ffffff, border_width = -4, frame_color = #ffffff, frame_width = 2)  

    ROWS(VIPER_PANEL, 0, 'PINE BULT-IN FUNCTIONS', 'LOADED VALUE', 'LOADED DECIMALS', 'RETURNS', 'VIPER_ADVANCED_DECIMAL_ALGORITHM_EXTENDED[VIPER]', 'VIPER_ADVANCED_DECIMAL_ALGORITHM_COMPACT[]')  
در این بخش از کد، یک جدول گرافیکی (Table) ایجاد می‌شود که نتایج الگوریتم‌ها را به همراه مقادیر ورودی نمایش می‌دهد.
ستون‌ها شامل اطلاعاتی نظیر نوع داده، مقدار ورودی، تعداد ارقام اعشاری، و خروجی الگوری
