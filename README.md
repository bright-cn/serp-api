# SERP API

[![Promo](https://github.com/bright-cn/Google-News-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner%20CN.png)](https://www.bright.cn/products/serp-api)

本仓库提供了两种获取搜索引擎结果页 (SERP) 数据的方法：  
1. 适用于基础数据收集的免费小规模 Google 抓取工具  
2. 面向大规模、实时数据收集需求的企业级 API 解决方案，可从主要搜索引擎获取数据  

## 目录
- [免费 SERP 抓取工具](#免费-serp-抓取工具)
   - [输入参数](#输入参数)
   - [实现方式](#实现方式)
   - [示例输出](#示例输出)
- [局限性](#局限性)
- [Bright Data SERP API](#bright-data-serp-api)
   - [主要特性](#主要特性)
   - [快速开始](#快速开始)
   - [直接 API 访问](#直接-api-访问)
   - [原生代理方式访问](#原生代理方式访问)
- [查询参数概览](#查询参数概览)
   - [Google](#google)
     - [Google Search](#1-google-search)
     - [Google Maps](#2-google-maps)
     - [Google Trends](#3-google-trends)
     - [Google Reviews](#4-google-reviews)
     - [Google Lens](#5-google-lens)
     - [Google Hotels](#6-google-hotels)
     - [Google Flights](#7-google-flights)
   - [Bing](#bing)
   - [Yandex](#yandex)
   - [DuckDuckGo](#duckduckgo)
- [SERP API 其他设置](#serp-api-其他设置)
   - [异步请求](#异步请求)
   - [多查询请求](#多查询请求)
- [支持与资源](#支持与资源)

## 免费 SERP 抓取工具
[免费抓取工具](https://github.com/bright-cn/serp-api/tree/main/free_serp_scraper) 可用于小规模的 Google SERP 数据收集。

<img width="700" alt="google-search" src="https://github.com/luminati-io/serp-api/blob/main/Images/bright%20data%20products%20serp.png" />

### 输入参数
- **File（文件）：** 包含搜索关键词的文本文件（必需）  
- **Format（格式）：** 每行一个搜索关键词  

### 实现方式
在 Python 文件中修改以下参数：
```python
# free_serp_scraper/google_serp.py
HEADLESS = False
MAX_RETRIES = 2
REQUEST_DELAY = (1, 4)

with open("search_terms.txt", "r", encoding="utf-8") as file:
    pass
```

### 示例输出
<img width="700" alt="google-serp-data" src="https://github.com/luminati-io/serp-api/blob/main/Images/samle%20output%20serp.png" />

## 局限性
Google 对自动化抓取有多种防护策略：

1. **验证码（CAPTCHA）**：用来区分人类和自动程序  
2. **IP 封锁**：对可疑活动进行临时或永久封锁  
3. **速率限制**：快速检测并阻止非授权请求  
4. **地理定位**：根据地区、语言、设备不同返回不同结果  
5. **诱捕陷阱**：通过隐藏元素来检测自动化访问  

## Bright Data SERP API
[Bright Data 的 SERP API](https://www.bright.cn/products/serp-api) 为可靠的 SERP 数据采集提供了强大的解决方案。

### 主要特性

- 按“成功请求”付费的模式  
- 响应速度快  
- 支持基于位置的精确定位  
- 支持多种设备类型和搜索参数  
- 覆盖主流搜索引擎（Google、Bing、DuckDuckGo、Yandex、Baidu、Yahoo、Naver）  
- 内置反爬解决方案  
- 实时结果，支持城市级别精确度  
- 数据结构化输出（JSON/HTML）  

**注意：** **SERP API** 是 [**Bright Data 的 Web Scraping Suite**](https://docs.brightdata.com/scraping-automation/introduction) 的一部分，包含完整的代理管理、解封锁和解析功能。

### 快速开始

1. **先决条件：**  
   - 注册 [Bright Data 账户](https://www.bright.cn/)  
   - 获取你的 [API key](https://docs.brightdata.com/general/account/api-token)  
2. **设置 SERP API：** 按照 [步骤指南](https://github.com/luminati-io/SERP-API/blob/main/setup_serp_api.md) 在 Bright Data 账户中配置新的 SERP API。  
3. **实现方式：**  
   1. 直接 API 访问  
   2. 原生代理方式访问  

### 直接 API 访问
最简单的方式是通过直接请求使用该 API。

**cURL 示例**
```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://www.google.com/search?q=ollama&brd_json=1",
        "format": "raw"
      }'
```

**Python 示例**
```python
import requests
import json

url = "https://api.brightdata.com/request"

headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}

payload = {
    "zone": "ZONE_NAME",
    "url": "https://www.google.com/search?q=ollama&brd_json=1",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("serp_direct_api.json", "w") as file:
    json.dump(response.json(), file, indent=4)

print("Response saved to 'serp_direct_api.json'.")
```

👉 查看 [完整 JSON 输出](https://github.com/bright-cn/SERP-API/blob/main/serp_api_outputs/serp_direct_api.json)

**注意**: 使用 `brd_json=1` 可获取解析后的 JSON，或使用 `brd_json=html` 可获取解析后的 JSON 与完整嵌套 HTML。

了解更多解析结果的方法： [SERP API 解析指南](https://docs.brightdata.com/scraping-automation/serp-api/parsing-search-results)

### 原生代理方式访问
另一种通过代理路由的方法。

**cURL 示例**
```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<CUSTOMER_ID>-zone-<ZONE_NAME>:<ZONE_PASSWORD> \
  -k \
  "https://www.google.com/search?q=ollama"
```

**Python 示例**
```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer_id>-zone-<zone_name>"
password = "<zone_password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}

url = "https://www.google.com/search?q=ollama"
response = requests.get(url, proxies=proxies, verify=False)

with open("serp_native_proxy.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved to 'serp_native_proxy.html'.")
```

👉 查看 [完整 HTML 输出](https://github.com/bright-cn/SERP-API/blob/main/serp_api_outputs/serp_native_proxy.html)

**SSL 证书**：在生产环境中加载 Bright Data 的 SSL 证书。详情参见：[SSL 证书指南](https://docs.brightdata.com/general/account/ssl-certificate)

## 查询参数概览
Bright Data SERP API 支持对多个搜索引擎进行定制请求，包括 Google、Bing、Yandex 和 DuckDuckGo。可通过查询参数配置本地化、分页、设备模拟等。以下为主要能力概述。

> 查看所有查询参数及其详细说明，请参阅 [详细查询参数文档](https://docs.brightdata.com/scraping-automation/serp-api/query-parameters)。

### Google
SERP API 支持多种 Google 服务，包括 [**Search**](https://www.bright.cn/products/serp-api/google-search)、[**Maps**](https://www.bright.cn/products/serp-api/google-search/maps)、[**Trends**](https://www.bright.cn/products/serp-api/google-search/trends)、[**Reviews**](https://www.bright.cn/products/serp-api/google-search/reviews)、**Lens**、[**Hotels**](https://www.bright.cn/products/serp-api/google-search/hotels) 和 [**Flights**](https://www.bright.cn/products/web-scraper/google-flights)。以下是各服务的关键配置参数：

#### 1. Google Search
可通过本地化、搜索类型、分页、地理位置及设备定向等参数定制搜索结果。

**本地化**  
- `gl`：搜索所在地的国家代码（如 `gl=us`）  
- `hl`：搜索结果语言代码（如 `hl=en`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/search?q=pizza&gl=us&hl=en"
```

**搜索类型：**  
使用 `tbm` 参数指定搜索类型：  
- 图片：`tbm=isch`  
- 购物：`tbm=shop`  
- 新闻：`tbm=nws`  
- 视频：`tbm=vid`  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/search?q=pizza&tbm=shop"
```

**分页：**  
- `start`：结果的偏移量（第一页为 0，第二页为 20，依此类推）  
- `num`：每页显示的结果数（默认 20）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/search?q=pizza&start=20&num=50"
```

**地理位置：**  
- `uule`：用于生成地理定位结果的编码位置字符串

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/search?q=pizza&uule=w+CAIQICINVW5pdGVkK1N0YXRlcw"
```

**设备定向：**  
使用 `brd_mobile` 参数：  
- `0`：桌面端（默认）  
- `1`：随机移动端  
- 指定值：`ios`（或 `iphone`）、`ipad`、`android`、`android_tablet`  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/search?q=pizza&brd_mobile=1"
```

#### 2. Google Maps
通过指定坐标或住宿类型来定制 Google Maps 查询。

**坐标：**  
- 格式：`@latitude,longitude,zoom`，`zoom` 从 `3z` 到 `21z` 不等。

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/maps/search/restaurants/@47.30227,1.67458,14.00z"
```

**住宿搜索：**  
- `brd_accomodation_type`：  
  - `hotels`（默认）  
  - `vacation_rentals`  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/maps/search/hotels+new+york/?brd_accomodation_type=vacation_rentals"
```

#### 3. Google Trends
通过自定义时间范围和小部件 (widgets) 选项来获取趋势数据。

**必需参数：**  
- `brd_json=1`：返回结构化的 JSON 结果  
- `brd_trends`：指定要获取的小部件如 `timeseries,geo_map`  

**时间范围：**  
- `date`：指定时间范围（如 `now 1-d` 表示过去 1 天）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://trends.google.com/trends/explore?q=pizza&date=now+1-d&brd_trends=timeseries,geo_map&brd_json=1"
```

#### 4. Google Reviews
使用商家或地点的特征 ID (feature ID) 获取评论，并可根据需要排序。

**关键参数：**  
- `fid`：从搜索结果中获取的特征 ID  
- `sort`：排序方式（如 `newestFirst`、`ratingHigh`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user "brd-customer-<id>-zone-<name>:<pass>" \
  "https://www.google.com/reviews?fid=0x808fba02425dad8f&sort=newestFirst"
```

#### 5. Google Lens
通过图片 URL 或文件上传进行以图搜图。

**图片搜索：**  
- `url`：要搜索的图片链接  
- `brd_json=1`：以 JSON 格式返回结果  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://lens.google.com/uploadbyurl?url=https://example.com/image.jpg&brd_json=1"
```

#### 6. Google Hotels
通过预订时间及货币选项来定制酒店搜索。

**预订参数：**  
- `brd_dates`：入住和退房日期，格式 `YYYY-MM-DD,YYYY-MM-DD`  
- `brd_currency`：货币代码（如 `USD`、`EUR`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/travel/hotels?q=hotels+new+york&brd_dates=2022-01-20,2022-02-05"
```

#### 7. Google Flights
使用与本地化类似的参数进行机票搜索。

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.google.com/travel/flights?q=flights+new+york&gl=us&hl=en"
```

### Bing
可通过本地化、地理定位、分页、设备/浏览器定向及输出格式等参数来配置 Bing 查询。更多信息请参见 [Bing API 专页](https://brightdata.com/products/serp-api/bing-search)。

**本地化**  
- `setLang`：界面使用的语言（如 `setLang=en-US`）。  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&setLang=en-US"
```

**地理定位**  
- `location`：搜索地（如 `location=New+York`）  
- `cc`：国家代码（如 `cc=us`）  
- `mkt`：市场代码（如 `mkt=en-US`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&location=New+York&cc=us&mkt=en-US"
```

**分页**  
- `count`：结果数量（如 `count=50`）  
- `first`：分页偏移量（如 `first=11` 表示第二页）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&count=50&first=11"
```

**过滤**  
- `safesearch`：成人内容过滤（如 `safesearch=off`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&safesearch=off"
```

**设备定向**  
- `brd_mobile`：指定设备类型（如 `brd_mobile=1` 表示移动端，或 `brd_mobile=ios`）。  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&brd_mobile=1"
```

**浏览器定向**  
- `brd_browser`：指定浏览器（如 `brd_browser=chrome`）。  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&brd_browser=chrome"
```

**解析**  
- `brd_json`：返回解析后的 JSON（如 `brd_json=1`）。  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.bing.com/search?q=pizza&brd_json=1"
```

### Yandex
可针对 Yandex 进行简单的参数配置，如本地化、分页、时间范围、设备/浏览器定向。更多信息请参见 [Yandex API 专页](https://brightdata.com/products/serp-api/yandex-search)。

**本地化**  
- `lr`：指定地区（如 `lr=84` 表示美国）  
- `lang`：页面语言（如 `lang=en`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.yandex.com/search/?text=pizza&lr=84&lang=en"
```

**分页**  
- `p`：结果页数（如 `p=2` 表示第二页）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.yandex.com/search/?text=pizza&p=2"
```

**时间范围**  
- `within`：指定时间范围（如 `within=1`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.yandex.com/search/?text=pizza&within=1"
```

**设备定向**  
```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.yandex.com/search/?text=pizza&brd_mobile=1"
```

**浏览器定向**  
```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://www.yandex.com/search/?text=pizza&brd_browser=chrome"
```

### DuckDuckGo
简要介绍对 DuckDuckGo 搜索进行本地化、安全搜索、时间范围及设备/浏览器定向的自定义。更多详情参考 [DuckDuckGo API 专页](https://brightdata.com/products/serp-api/duckduckgo-search)。

**本地化**  
- `kl`：国家和语言（如 `kl=us-en`）  
- `kad`：界面语言配置  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://duckduckgo.com/?q=pizza&kl=us-en"
```

**安全搜索**  
- `kp`：启用安全搜索（如 `kp=1`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://duckduckgo.com/?q=pizza&kp=1"
```

**时间范围**  
- `df`：指定时间范围（如 `df=d`）  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://duckduckgo.com/?q=pizza&df=d"
```

**设备定向**  
- `brd_mobile`：移动端模拟  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://duckduckgo.com/?q=pizza&brd_mobile=1"
```

**浏览器定向**  
- `brd_browser`：指定浏览器（如 `chrome`）。  

```bash
curl \
  --proxy brd.superproxy.io:33335 \
  --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
  "https://duckduckgo.com/?q=pizza&brd_browser=chrome"
```

## SERP API 其他设置

### 异步请求
- 同步（默认）：立即获取实时响应  
- 异步：结果可稍后获取（适合大量查询场景）  

详情请参阅：[异步工作原理](https://docs.brightdata.com/scraping-automation/serp-api/asynchronous-requests#how-it-works)

### 多查询请求
在一次 API 调用中，通过 `multi` 参数并行发送 **多个查询**，并可共享同一 IP 和会话。

```python
multi:[
  {"keyword":"shoes","num":50},
  {"keyword":"shoes","num":200}
]
```
了解更多：[多查询指南](https://docs.brightdata.com/scraping-automation/serp-api/asynchronous-requests#multiple-queries-in-a-single-request)

## 支持与资源
- **文档：** [SERP API 文档](https://docs.brightdata.com/scraping-automation/serp-api/)  
- **查询参数文档：** [详细查询参数文档](https://docs.brightdata.com/scraping-automation/serp-api/query-parameters)  
- **更多指南：** [Web Unlocker API](https://github.com/luminati-io/web-unlocker-api)、[Google Maps](https://github.com/luminati-io/Google-Maps-Scraper)、[Google News](https://github.com/luminati-io/Google-News-Scraper)  
- **更多阅读：** [最佳 SERP APIs](https://brightdata.com/blog/web-data/best-serp-apis)、[使用 SERP API 搭建 RAG Chatbot](https://brightdata.com/blog/web-data/build-a-rag-chatbot)、[Python 抓取 Google Search](https://brightdata.com/blog/web-data/scraping-google-with-python)  
- **技术支持：** [联系我们](mailto:support@brightdata.com)  
