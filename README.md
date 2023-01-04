
<div dir="rtl" align="center">

# DynamoDB

</div>

<div dir="rtl" align="right">

یک پایگاه داده کاملاً مدیریت شده و NOSQL که توسط AWS ارائه شده است




## ویژگی های اساسی:




🔸 پشتیبانی از دو ساختار:


> * key - value
> 
> * wide column 


🔸 مقیاس پذیری (Scale) بدون کاهش عملکرد


>مهم نیست دیتای شما یک مگابایت باشه، ده گیگابایت یا حتی ده گیگابایت، دیتای شما در چند میلی ثانیه آماده میشه.

🔸 مدل هایی بر پایه http 

>مثل یک api به این دیتابیس وصل بشید و با دیتابیس و دیتاهاتون کار کنید.



🔸 پنل های قیمتی منعطف 

>۲۵ گیگ فضای رایگان!



🔸 رهگیری تغییرات با قابلیت Stream 

>این ویژگی به شما این امکان رو میده که دیتابیس بتونه با شما ارتباط داشته باشه و تغییرات دیتا (Add-Edit-Delete) رو به اطلاع شما برسونه.



🔸 پشتیبانی از IAM






## کی باید از DynamoDB استفاده کرد؟

🔸 وقتی کاربر های خیلی خیلی زیاد دارید و نیاز به scale زیادی دارید.


🔸 وقتی میخواید با ابزار هایی مثل AWS AppSync و یا AWS Lambda کار کنید. (سازگاری بالا با این ابزار ها)


🔸 وقتی ساختار دیتابیستون ساده است!

🔸 وقتی نیاز به کش کردن اطلاعات دارید! (نه به خوبیه redis ولی اگه نمیخواین ردیس راه اندازی کنید تا حد زیادی کارتون رو راه میندازه)

🔸 وقتی میخواید اپی با ساختار OLTP بسازید!



>معمولا برنامه نویس ها بخاطر تجربه و ذهنیتی که نسبت به دیتابیس های رابطه ای دارن در برابر مهاجرت به DynamoDB مقاومت میکنن ولی دو برتری که DynamoDB در مقایسه با دیتابیس های رابطه ای داره یکی قابلیت اسکیل پذیری عالی اونه و مورد بعد پشتیبانی خیلی خوب از سرویس های ServerLess هست.




##  انواع Primary Key 

🔸 کلید اصلی ساده یا Simple Primary Key

>مشابه Key در هش تیبل!

🔸 کلید اضلی ترکیبی یا Composite Primary Key
 
>مشابه Simple Primary Key ولی با دو Key. به Key اول Partition Key و به Key دوم Sort Key گفته میشه.
> 
>برای مثال Key ما در مرحله اول اسم بازیگر و در مرحله دوم فیلم های بازیگر هست.
> 
>بطور مشخص یک بازیگر میتونه چندین فیلم داشته باشه ولی مجموع همه ابجکت های مربوط به اون بازیگر یک Item Collection هستن.
> 
>پ.ن: یکی از کاربرد های Item Collection برای پیاده سازی مفهوم Relation هست.




## مفاهیم مهم در DynamoDB 

🔸 تیبل یا Tabel: مشابه Tabel دیتابیس های رابطه ای، یک تیبل شامل یک سری دیتا با محوریت مشخص هست.

🔸 آیتم یا Item: مشابه row در دیتابیس های رابطه ای (با این تفاوت که شامل بخش Key هم هست)

🔸 کلید اصلی یا Primary Key: کلید پیدا کردن یک ابجکت (مشابه Key در هش تیبل)

🔸 ویژگی ها یا Attributes: در واقع همون ستون ها در جداول رابطه ای با این تفاوت که هر Item میتونه Attributes های مختلفی داشته باشه


🔸 قابلیت Streams

>همونطور که قبلا گفته شد این ویژگی به شما این امکان رو میده که دیتابیس بتونه با شما ارتباط داشته باشه و تغییرات دیتا (Add-Edit-Delete) رو به اطلاع شما برسونه.

>این قابلیت خیلی در میکروسرویس ها، لاگ گیری و آنالیز کردن دیتا و Aggregations کاربردی هست.


🔸 طول عمر یا TTL (Time To Live)

>این ویژگی به شما امکان تنظیم تاریخ انقضا به ابجکت رو میده.


🔸 پارتیشن یا Partition 

> دیتای شما میتونه در چند فضای مختلف ذخیره سازی بشه که به اون فضا ها Partition گفته میشه.
>
> بزارید با یک یک مثال بهتر کاربردشون رو متوجه بشیم ... وقتی ما سه پارتیشن داریم و یک دیتای جدید قصد داریم ثبت کنیم دیتابیس سعی میکنه با اون Key یک هش بسازه و بفهمه که دیتای ما باید توی کدوم پارتیشن ثبت بشه و دیتارو در اون بخش ثبت میکنه.
>همونطور که گفتیم اسکیل پذیری جزء ويژگی های اصلی این دیتابیسه و یکی از روش های اسکیل این دیتابیس، افزایش تعداد پارتیشن هاست.
>هر لحظه که دیتابیس حجم دیتاش زیاد بشه، تعداد پارتیشن ها بیشتر میشن :) به همین راحتی


🔸 ثبات اطلاعات یا Consistency 

>این دیتابیس از دیتای هر پارتیشن شما دو کپی میگیره تا بتونه دسترسی پذیری و ثبات بیشتری داشته باشه.

>بدین صورت که وقتی دیتایی ثبت یا تغییر میدین. اون دیتا بصورت Async به نود بعدی منتقل میشه و اون نود وقتی دیتارو گرفت بصورت Async اون دیتارو به نود بعدی منتقل میکنه و اینطوری ما سه تا نسخه یکسان از یک دیتا داریم.

>پ.ن: بطور پیش فرض دیتابیس سعی میکنه **در پایان عملیات ها** دیتای هر سه نود یکسان باشه یعنی دیتابیس روی حالت (Eventual consistency) هست و این مساله ممکنه باعث بشه در چند میلی ثانیه بعد از درخواست تغییر، دیتایی که خونده میشه، دیتای به روزی نباشه. اگه میخواید قطعا دیتاتون دیتای درستی باشه، باید دیتابیس‌تون رو روی حالت Strong consistency بزارین!





##  محدودیت های DynamoDB

🔸 حداکثر سایز هر آیتم میتونه 400KB باشه!

>گفته میشه آمازون سعی داشته روند خوندن رو با این مساله سریعتر بکنه و شمارو ترغیب کنه:
> 
>* دیتارو به بخش های کوچیک تر بشکنین 
>* از آیتم کالکشن استفاده کنین 
>* از S3 برای ذخیره‌سازی فایل ها و عکس هاتون استفاده کنین!!

🔸 حداکثر حجم درخواست های Query و Scan میتونه 1MB باشه!

🔸 توان عملیاتی هر پارتیشن. 3000 خواندن در ثانیه و یا 1000 عملیات ثبت ویا ویرایش در ثانیه


🔸 هر Item Collection میتونه نهایتا 10GB دیتا داشته باشه!





</div>

