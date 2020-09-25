# Dùng Scrapy-splash với Lua script để crawl các trang web sử dụng Javascript
## Cài đặt, chạy
* Cài docker để chạy splash
```bash
sudo docker run -p 8050:8050 scrapinghub/splash
```
* Cài thư viện 
```bash
pip install scrapy scrapy-splash
```
* scrip lua mô phỏng hành động nhấp chuột chuyển trang
```bash
script = """
        function main(splash)
            local url = splash.args.url
            assert(splash:go(url))
            assert(splash:wait(0.5))
            assert(splash:runjs("$('.next')[0].click();"))
            return {
                html = splash:html(),
                url = splash:url(),
            }
        end
        """
```

* run crawl_web_js
```bash
scrapy crawl wss
```
