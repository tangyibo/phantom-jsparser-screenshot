# JS解析与页面截图服务组件

```
Author: tang
Date : 2017-09-10
Email: inrgihc@126.com
```

## 一、服务启动

### 1、查看phantomjs的版本信息

```
 ./phantomjs -v
  2.1.1
```

### 2、启动组件

```
 cd phantomjs-fetcher
 ./phantomjs crawler_fetcher.js 12345
```

## 二、使用说明

### 1、接口调用

```
 curl -XPOST "http://127.0.0.1:12345" -d
'{"url":"http://www.xupu.gov.cn/","load_images":true,"make_screen":true,"headers":{"User-Agent":"Mozilla/5.0
(Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko)
Chrome/58.0.3029.110 Safari/537.36"},"timeout":120}'
```

此时会返回页面抓取的HTML及header等信息，并在当前目录的snapshots目录下生成网页截图图片

### 2、请求参数说明

```
--------------------------------------------------------------------------
| 参数名称     | 说明                          |     示例                |
--------------------------------------------------------------------------
| url          | 请求抓取的页面URL地址         |  http://www.xupu.gov.cn/|
--------------------------------------------------------------------------
| load_images  |是否加载页面中的图片信息，在截 |  加载为true             |
|              |图时建议加载图片，否则截图中无 |  不加载为false          |
|              |法显示页面中的图片内容         |                         |
--------------------------------------------------------------------------
| make_screen  | 是否进行网页截图              | 截图为true,否则为false  |
--------------------------------------------------------------------------
| headers      | 用于设置HTTP请求的头部        | 例如设置User-Agent的值  |
--------------------------------------------------------------------------
| timeout      | 请求超时的时间                | 单位为：秒。默认为120秒 |
--------------------------------------------------------------------------
```

### 3、返回的结果

```
{
  "orig_url": "http://www.testurl.cn/",
  "status_code": 200,
  "content": "<!DOCTYPE html PUBLIC \"-//W3C//DTD XHTML 1.0 Transitional//EN\"
\"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd\"><html
xmlns=\"http://www.w3.org/1999/xhtml\"><head>\n<meta
http-equiv=\"Content-Type\" content=\"text/html;
charset=utf-8\">\n<title>欢迎访问 TESTURL.CN  -  华创互联</title>\n<style
type=\"text/css\">\nbody,td,th {\n\tfont-family: \"微软雅黑
Light\";\n}\n</style>\n</head>\n\n<body>\n<div style=\"font-size:36px;
padding-left:10%; margin-top:10%\">欢迎访问 TESTURL.CN </div>\n\n\n<div
style=\"font-size:16px; padding-left:10%;
margin-top:20px\">这是测试网站的临时域名，很高兴能为您服务...</div>\n\n<div
style=\"font-size:16px; padding-left:10%;
margin-top:20px\">我们能为您做些什么？ </div>\n\n\n<div
style=\"font-size:16px; padding-left:10%;
margin-top:20px\">网站设计&amp;定制，网站SEO，企业官网、响应式H5、营销型网站、外贸网站、商城开发。</div>\n\n\n<div
style=\"font-size:16px; padding-left:10%;
margin-top:20px\">如有需要，请联系我们</div>\n\n\n\n\n</body></html>",
  "headers": {
    "Date": "Wed, 30 Aug 2017 09:15:15 GMT",
    "Content-Type": "text/html",
    "Transfer-Encoding": "chunked",
    "Connection": "keep-alive",
    "Last-Modified": "Thu, 22 Jun 2017 03:22:24 GMT",
    "ETag": "W/\"01821c46ebd21:0\"",
    "X-Powered-By": "ASP.NET",
    "Server": "wts/1.2",
    "Content-Encoding": "gzip"
  },
  "url": "http://www.testurl.cn/",
  "cookies": {},
  "time": 2.028,
  "js_script_result": null,
  "snapshot": "snapshots/www_testurl_cn_2017-8-30_17-15-16-387.jpg"
}
```

## 三、Phantomjs 调试方法

### 1、Phantomjs命令
```
  Phantomjs命令行： phantomjs [options] somescript.js [arg1 [arg2 [...]]]
  关于调试的[options]：
     --remote-debugger-port  开启调试模式并监听制定端口
     --remote-debugger-autorun 在调试器中立即执行脚本（Yes/No）
  例如：
    在crawler_fetcher.js脚本的开头添加：
    debugger;//放在开头  或者任意位置（当断点）
```

### 2、Phantomjs调试过程

```
    =============调试过程======================================
    (1) 调试方式启动脚本
　　　./phantomjs --remote-debugger-port=9000 crawler_fetcher.js
    (2) 打开chrome 输入 http://127.0.0.1:9000/ 回车
       点击链接 ： file://crawler_fetcher.js
    (3) 在跳转进去的Console选项界面中中输入：
          __run()  回车
    (4) 根据调试情况修改JS脚本代码
    ============================================================
```

