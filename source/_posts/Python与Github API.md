---
title: Python与Github API
author: yikafu
date: 2022-08-06 14:42:13
updated: 2022-08-06 14:42:13
tags: others
categories: Code
cover: https://cdn.jsdelivr.net/gh/yikafu/blog_img/random_cover/cover2.jpg
---

# github api格式

```html
https://api.github.com/repos/用户名/仓库名/releases/latest
```



# github api 获取版本号

```python
response = requests.get(api_url)
tags_name = response.json()["tags_name"]
```

使用json获取最新版本号


# 通过github api 获取下载链接

```python
api_url =
"https://api.github.com/repos/yikafu/fuck-reprository/releases/latest"

# 返回下载链接
def find_download_url(api_url):
    response = requests.get(api_url)
    assets_url = response.json()["assets_url"]
    response1 = requests.get(assets_url)
    r = response1.json()
    for i in r :
        return i["browser_download_url"] 
        
```

我们所需要的`"browser_download_url"`位于 **assets** 里面
![](https://cdn.jsdelivr.net/gh/yikafu/blog_img/gitapi-1.png)

因此通过`response = requests.get(api_url)`获取页面中的`"assets_url"` , 进而进入**assets**页面

![](https://cdn.jsdelivr.net/gh/yikafu/blog_img/gitapi-2.png)

`r = response1.json()`获取assets页面内容，并通过for循环进行查找字典键为`"browser_download_url"`的元素，得到他的值，即下载链接

```python
download = requests.get(find_download_url(api_url))
# 确定目录和下载
with open( "xxx", "wb") as f:
    f.write(download.content)
```

