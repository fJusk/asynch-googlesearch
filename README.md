# googlesearch

> **DISCLAIMER:** This fork was entirely created by AI with no human review. While efforts were made to ensure quality, there is no guarantee of correctness, security, or performance. Use at your own risk.

googlesearch is a Python library for searching Google, easily. This version uses aiohttp and BeautifulSoup4 to scrape Google.

## Installation
To install, run the following command:
```bash
python3 -m pip install git+https://github.com/fJusk/asynch-googlesearch.git
```

## Usage
The library provides both asynchronous and synchronous interfaces.

### Synchronous Interface
For backward compatibility, you can use the synchronous `sync_search` function:

```python
from googlesearch import sync_search
results = sync_search("Google")
print(results)
```

### Asynchronous Interface
For using the asynchronous API:

```python
import asyncio
from googlesearch import search, gsearch

# Using async generator
async def main():
    async for result in search("Google"):
        print(result)
    
    # Or get full list of results
    all_results = await gsearch("Google")
    print(all_results)

asyncio.run(main())
```

## Additional options
googlesearch supports various additional options. By default, it returns 10 results. This can be changed. For example, to get 100 results:

```python
from googlesearch import sync_search
results = sync_search("Google", num_results=100)
```

If you want to have unique links in your search results, use the `unique` parameter:
```python
from googlesearch import sync_search
results = sync_search("Google", num_results=100, unique=True)
```

You can also change the language Google searches in. For example, to get results in French:
```python
from googlesearch import sync_search
results = sync_search("Google", lang="fr")
```

You can specify the region ([Country Codes](https://developers.google.com/custom-search/docs/json_api_reference#countryCodes)) for your search results. For example, to get results specifically from the US:
```python
from googlesearch import sync_search
results = sync_search("Google", region="us")
```

If you want to turn off the safe search function (this function is on by default):
```python
from googlesearch import sync_search
results = sync_search("Google", safe=None)
```

To extract more information, such as the description or the result URL, use an advanced search:
```python
from googlesearch import sync_search
results = sync_search("Google", advanced=True)
# Returns a list of SearchResult objects
# Properties:
# - title
# - url
# - description
```

When requesting more than 100 results, the library will send multiple requests to go through the pages. To increase the time between these requests, use the `sleep_interval` parameter:
```python
from googlesearch import sync_search
results = sync_search("Google", sleep_interval=5, num_results=200)
```

If you're requesting more than 10 results but want to manage the batching yourself, use `start_num` to specify the starting point of the results you want to get:
```python
from googlesearch import sync_search
results = sync_search("Google", sleep_interval=5, num_results=200, start_num=10)
```

If you are using an HTTP Rotating Proxy that requires installing their CA Certificate, you can add `ssl_verify=False` to the `search()` method to avoid SSL Verification.
```python
from googlesearch import sync_search

proxy = 'http://username:password@proxy.host.com:8080/'
# or for socks5
# proxy = 'socks5://username:password@proxy.host.com:1080/'

results = sync_search("proxy test", num_results=100, lang="en", proxy=proxy, ssl_verify=False)
```
