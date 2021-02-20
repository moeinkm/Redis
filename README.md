# Redis
## a beginner guide to Redis on Docker in Persian

<div dir="rtl">
  redis یا remote dictionary server یک ذخیره کننده ساختمان داده است که بر روی Ram قرار میگیرد به همین دلیل آنرا in-memory Database می نامند. ساختار redis به صورت کلید مقداری key-value است به همین دلیل میتوان آن را یک نوع پایگاه داده No-SQL دانست.
  
  
  به مانند هر دیتابیس دیگری، Redis دارای یک سرور برای ذخیره داده‌ها در رم و کلاینت‌ها است که در قبال یک سرور، دستوراتی را اجرا می‌کند. برای راه‌اندازی سرور بر روی دستگاه خود، استفاده از Docker را پیشنهاد می‌کنم؛ زیرا شروع کار با آن بسیار ساده است. اگر Docker daemon را بر روی سیستم خود دارید، این دستور را اجرا کنید:
</div>
  
  ```
  docker pull redis:<version>
  ```
  
  <div dir="rtl">
  با این دستور تصویر رسمی ردیس رو سیستم شما دانلود می شود. اگر ورژن مورد نظر خود را انتخاب نکنید به صورت دیفالت از برچسب latest استفاده میشود.

</div>

```
> docker pull redis
Using default tag: latest
latest: Pulling from library/redis
```
<div dir="rtl">
  
  برای اجرای این تصویر از دستور زیر استفاده می کنیم
  
</div>

```
docker run -d -p 6379:6379 --name redis-test redis
```

<div dir="rtl">
  
  این دستور از تصویر دانلود شده یک پروسه میسازد به نام redis-test روی پورت دیفالت ردیس 6379. برای دیدن اینکه آیا ردیس به صورت یک پروسه درحال اجرا است یا نه لیست پروسه های در حال اجرای داکر را با دستور زیر میتوانید مشاهده کنید
  
  </div>
  
 ```
 docker ps
 ```
 
 <div dir="rtl">
  
  پروسه ردیس را در لیست پروسه ها به صورت زیر باید مشاهده کنید
  
  </div>
  
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                    NAMES
xxxxxxxxxxxx   redis     "docker-entrypoint.s…"   n minutes ago   Up 8 minutes   0.0.0.0:6379->6379/tcp   redis-test
```

<div dir="rtl">
  همچنین برا مشاهده لاگ های انجین ردیس میتوانید از دستور زیر استفاده کنید
  
  </div>
  
```
docker logs redis-test
```

<div dir="rtl">
  که در آن redis-test نام محفظه ردیس است.
  
  حالا برا وصل شدن به cli ردیس از دستور زیر استفاده میکنیم:
  </div>
  
```
docker exec -it redis-test sh
```

با این دستور بش ردیس به صورت تعاملی اجرا میشود. با وارد شدن به این محیط با اجرای دستور redis-cli میتوانید دستورات خود را روی ردیس اجرا کنید.

</div>

```
# redis-cli
```

<div dir="rtl">
  
  با این دستور به ردیس رو پورت مربوطه وصل میشویم
  
  ساده ترین دستورات ردیس set و get هستند که بقیه دستورات بر پایه اینها اجرا می شوند که set برای یک کلید مقدار set میکند و get مقدار کلید ها را بر میگرداند.
  
  چند تا از دستورات ساده ردیس را در ادامه با هم می بینیم
  
  </div>
  
```
127.0.0.1:6379> ping
PONG
127.0.0.1:6379> ping hello
"hello"
127.0.0.1:6379> set me "moein"
OK
127.0.0.1:6379> get me
"moein"
127.0.0.1:6379> keys *
1) "me"
127.0.0.1:6379> exit
# exit
```

<div dir="rtl">
در دستورات بالا ping صحت اتصال را بررسی میکند، set مقداری برای کلید گفته شده(در اینجا me) ست میکند و get مقدار ست شده برای کلید را برمیگرداند (اگر کلید get شده وجود نداشته باشد nil بازگردانده میشود).  
  
  
</div>  


<div dir="rtl">
 
 برای دیدن لیست کامل دستورات ردیس به [http://redis.io/commands
](http://redis.io/commands
) مراجعه کنید


همچنین لینک های مفید برای عمیق تر شدن در ردیس:

* معرفی انواع داده در ردیس http://redis.io/topics/data-types-intro
* امتحان کردن دستورا ردیس در مرورگر http://try.redis.io
* و داکیومنتیشن رسمی ردیس http://redis.io/documentation

</div>
