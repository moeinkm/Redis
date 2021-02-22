# Redis
## a beginner guide to Redis in Persian
<p align="center">
    <img src="https://github.com/AryanAhadinia/web_workshop/blob/redis_article/Redis/public/redis_logo.svg" alt="Redis Logo">
</p>
<div dir="rtl">

## ردیس چیست؟
  redis یا remote dictionary server یک ذخیره کننده ساختمان داده است که بر روی Ram قرار میگیرد به همین دلیل آنرا in-memory Database می نامند. ساختار redis به صورت کلید مقداری key-value است به همین دلیل میتوان آن را یک نوع پایگاه داده NoSQL دانست. همچنین از آن به عنوان کش و سرویس انتقال پیام نیز استفاده میشود.

## چرا ردیس؟

### سرعت بالا
در دنیای امروز سرعت فاکتور بسیار مهمی است و ابزار هایی که سرعت بالاتری دارند مورد توجه کاربران قرار میگیرند در نتیجه مدیران آن ها را مورد توجه قرار می دهند. نقطه قوت ردیس نیز در همینجاست و به دلیل نوشته شدن به زبان C سرعت بسیار بالایی دارد.

### ساختار مانند NoSQL

ردیس ساختاری شبیه به پایگاه داده های NoSQL دارد و به صورت کلید مقداری داده ها را ذخیره میکند همین ویژگی باعث محبوبیت در بین توسعه دهندگان شده است.

### پشتیبانی از زبان های برنامه نویسی مختلف

ردیس از بیشتر زبان های برنامه نویسی مانند سی، سی پلاس پلاس، سی شارپ، پی اچ پی، پایتون، ابجکتیو سی، گو، و... پشتیبانی میکند و نیاز طیف وسیعی از توسعه دهندگان را به خوبی پاسخ میدهد


## راه اندازی

### راه اندازی روی داکر
  به مانند هر دیتابیس دیگری، Redis دارای یک سرور برای ذخیره داده ها در رم و کلاینت ها است که در قبال یک سرور، دستوراتی را اجرا میکند. برای راه اندازی سرور بر روی دستگاه خود، استفاده از Docker را پیشنهاد میکنم؛ زیرا شروع کار با آن بسیار ساده است. اگر Docker daemon را بر روی سیستم خود دارید، این دستور را اجرا کنید:
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

<div dir="rtl">

### راه اندازی روی ویندوز

راه اندازی ردیس روی ویندوز بسیار سرراست است. به این صورت که شما فایل ```.msi``` یا ```.zip``` آن را دانلود کنید([از اینجا میتوانید دانلود کنید](https://redis.io/download)) سپس ```redis-server.exe``` را اجرا کنید، با این کار ردیس روی لوکال(127.0.0.1) روی پورت پیشفرض 6379 در دسترس خواهد بود. یا متوانید همین کار را به صورت زیر انجام دهید.
    
</div>

```
$ wget https://download.redis.io/releases/redis-6.0.10.tar.gz
$ tar xzf redis-6.0.10.tar.gz
$ cd redis-6.0.10
$ make
```

<div dir="rtl">
    که این دستورات ابتدا نسخه 6.0.10 را از منبع دانلود میکند و سپس آن را از حالت فشرده خارج و آن را کامپایل میکند.
    
</div>

<div dir="rtl">
    
### راه اندازی روی Ubuntu
    
    
برای نصب ردیس روی اوبونتو ابتدا ```apt``` را بروزرسانی کنیم سپس```redis-server``` را نصب کنیم. فرض میکنیم تنظیمات فایروال ابتدایی و کاربر بدون دسترسی root است.
    
    
</div>

```
sudo apt update
sudo apt install redis-server
```

<div dir="rtl">

با این دستور ردیس و نیازمندی های آن روی سیستم عامل نصب می شود.

حالا فایل کانفیگ ردییس که به صورت خودکار نصب شده است را باید باز کنیم و فیلد ```supervised``` که به صورت پیش فرض ```no``` است را به ```systemd``` تغییر دهیم. برای این کار فایل کانفیگ ردیس را با هر ویرایشگری متنی که دوست دارید باز کنید.

</div>

```
sudo nano /etc/redis/redis.conf
```
<div dir="rtl">
 در فایل تنظیمات باز شده ```supervised``` را پیدا کنید و مقدار آن را از ```no``` به ```systemd``` تغییر دهید و آن را ذخیره کنید.
    
  حالا باید ردیس را ری استارت کنیم تا تغییرات تنظیمات آن اعمال شود.
    
</div>

```
sudo systemctl restart redis.service
```
<div dir="rtl">
    
حالا فکر خوبیست که بررسی کنیم آیا ردیس به درستی در حا اجرا است.
    
</div>

```
sudo systemctl status redis
```
<div dir="rtl">
    
اگر ردیس بدون خطا درحال اجرا باشد خروجی دستور را به صورت زیر خواهید دید.
    
</div>

```
redis-server.service - Advanced key-value store
   Loaded: loaded (/lib/systemd/system/redis-server.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2018-06-27 18:48:52 UTC; 12s ago
     Docs: http://redis.io/documentation,
           man:redis-server(1)
  Process: 2421 ExecStop=/bin/kill -s TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 2424 ExecStart=/usr/bin/redis-server /etc/redis/redis.conf (code=exited, status=0/SUCCESS)
 Main PID: 2445 (redis-server)
    Tasks: 4 (limit: 4704)
   CGroup: /system.slice/redis-server.service
           └─2445 /usr/bin/redis-server 127.0.0.1:6379
. . .
```

<div dir="rtl">

## تعامل با ردیس 

با این دستور بش ردیس به صورت تعاملی اجرا میشود. با وارد شدن به این محیط با اجرای دستور redis-cli میتوانید دستورات خود را روی ردیس اجرا کنید.

</div>

```
# redis-cli
```

<div dir="rtl">
  
  با این دستور به ردیس رو پورت مربوطه وصل میشویم
  
### String
  
  ساده ترین دستورات ردیس set و get هستند که بقیه دستورات بر پایه اینها اجرا می شوند که set برای یک کلید مقدار set میکند و get مقدار کلید ها را بر میگرداند.
  
  چند تا از دستورات ساده ردیس را در ادامه با هم می بینیم
  
  </div>
  
```
127.0.0.1:6379> PING
PONG
127.0.0.1:6379> PONG hello
"hello"
127.0.0.1:6379> SET me "moein"
OK
127.0.0.1:6379> GET me
"moein"
127.0.0.1:6379> KEYS *
1) "me"
2) 127.0.0.1:6379> MSET country iran city tehran street azadi
OK
127.0.0.1:6379> MGET country city street
1) "iran"
2) "tehran"
3) "azadi"
```

<div dir="rtl">
در دستورات بالا ping صحت اتصال را بررسی میکند، set مقداری برای کلید گفته شده(در اینجا me) ست میکند و get مقدار ست شده برای کلید را برمیگرداند (اگر کلید get شده وجود نداشته باشد nil بازگردانده میشود).  

### Integer

با دستورات زیر میتوانید یک فیلد اینتیجر تعریف و آن را افزایش و کاهش دهید
  
</div>  

```
127.0.0.1:6379> SET score 17
OK
127.0.0.1:6379> INCRBY score 3
(integer) 20
127.0.0.1:6379> DECR score
(integer) 19
127.0.0.1:6379> DECRBY score 9
(integer) 10
127.0.0.1:6379> GET score
"10"
```


<div dir="rtl">

### Lists

در ردیس برا پیاده سازی لیست از linked-list به جای آرایه استفاده شده به همین دلیل اینزرت کردن با اوردر ۱ و بسیار سریع انجام میشود در حالی که پیدا کردن یک عضو با اوردر n انجام میشود به همین دلیل توصیه میشود اگر برنامه شما با فرکانس بیشتری به جستجو نیاز دارد از sorted-set استفاده کنید.

</div>  

```
127.0.0.1:6379> LPUSH mylist 1 asb 2
(integer) 3
127.0.0.1:6379> RPUSH mylist "Shotor" "Boz" 3
(integer) 6
127.0.0.1:6379> LRANGE mylist 0 6
1) "2"
2) "asb"
3) "1"
4) "Shotor"
5) "Boz"
6) "3"
127.0.0.1:6379> LTRIM mylist 0 1
OK
127.0.0.1:6379> LRANGE mylist 0 6
1) "2"
2) "asb"
127.0.0.1:6379> RPOP mylist
"asb"
127.0.0.1:6379> LRANGE mylist 0 6
1) "2"
```
<div dir="rtl">
    
 در دستورات بالا ```LPUSH``` از سمت چپ به لیست اضافه میکند و ```RPUSH```  از سمت راست. ```LRANGE``` در رنج داده شده مقادیر لیست را باز میگرداند و اگر رنج بزرگتر از طول لیست باشد همه مقادیر آن را باز میگرداند. ```LTRIM``` لیست را در بازه داده شده مقادیر را نگه داشته و باقی را دور میریزد و ```RPOP``` آخرین مقدار را از سمت راست برگردانده و از لیست خارج میکند.
 
</div>


<div dir="rtl">
 
### Hashes

هش مپ ها به صورت کلید مقداری

</div>
```
127.0.0.1:6379> HMSET palang id 85 name shima
OK
127.0.0.1:6379> HGET palang id
"85"
127.0.0.1:6379> HGET palang name
"shima"
127.0.0.1:6379> HGETALL palang
1) "id"
2) "85"
3) "name"
4) "shima"
```

<div dir="rtl">
 
### Sets

ست ها مجموعه های بدون ترتیب هستند

</div>

```
127.0.0.1:6379> SADD mySet 2 2 2 4 8 16
(integer) 0
127.0.0.1:6379> SMEMBERS mySet
1) "2"
2) "4"
3) "8"
4) "16"
127.0.0.1:6379> SISMEMBER mySet 2
(integer) 1
```

<div dir="rtl">
 
### Sorted sets

Sorted-set ها ساختار داده ای ما بین هش و ست است.

</div>

```
127.0.0.1:6379> ZADD president 1384 "Ahmadinejad" 1392 "Fereydoon"
(integer) 2
127.0.0.1:6379> ZRANGE president 0 -1
1) "Ahmadinejad"
2) "Fereydoon"
127.0.0.1:6379> ZREVRANGE president 0 -1 
1) "Fereydoon"
2) "Ahmadinejad"
127.0.0.1:6379> ZREVRANGE president 0 -1 withScores
1) "Fereydoon"
2) "1392"
3) "Ahmadinejad"
4) "1384"
127.0.0.1:6379> ZADD president 1376 "Khatami"
(integer) 1
127.0.0.1:6379> ZREVRANGE president 0 -1 withScores  // مقادیر با اسکور هایشان برمیگردند
1) "Fereydoon"
2) "1392"
3) "Ahmadinejad"
4) "1384"
5) "Khatami"
6) "1376"
127.0.0.1:6379> ZADD president 1368 "Hashemi" 1360 "Khamenei" 1358 "Banisadr"  // هر تعداد کلید مقدار به ست president اضافه می شود
(integer) 3
127.0.0.1:6379> ZREMRANGEBYSCORE president 1365 1392
(integer) 4
127.0.0.1:6379> ZRANGE president 0 -1
1) "Banisadr"
2) "Khamenei"
127.0.0.1:6379> ZRANK president Banisadr
(integer) 0
```
<div dir="rtl">

در این دستورات مربوت به Sorted set ```ZADD``` برا اضافه کردن کلید مقدار ها به ست ```ZRANGE``` برای خروجی گرفتن از مقادیر لیست در رنج داده شده (-۱ در انتهای بازه همه مقادیر را برمیگرداند)، ```ZREVRANGE``` مقادیر را با ترتیب برعکس و ```ZREMRANGEBYSCORE``` مقادیر را در بازه کلید ها(score) حذف میکند. 

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
