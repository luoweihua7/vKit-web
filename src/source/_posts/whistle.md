---
title: whistle常用配置方法
date: 2021-09-26 11:12:15
tags:
---

Whistle的常用配置方式记录

# 劫持响应
```
#/heartBeat/  statusCode://200 resBody://({"code":"1"})
```

# 替换响应
JSON必须是rfc标准，如果value有空格，可以使用Values选项添加内容后替换
```
zhaopin.oa.com resReplace://{"5849392":22984210}
```

# 正则替换
```
/dp_web\/static\/([^.]*)\.(.+$)/    xfile:///Users/[path_to_your_workspace]/dest/$1.js
```

# 本地代理
```
/./ proxy://127.0.0.1:12639 excludeFilter://127.0.0.1 excludeFilter://localhost
/./ enable://proxyHost proxy://127.0.0.1:12639
```

# 在Network请求列表中隐藏命中规则的请求
```
*.url.cn enable://hide
```

# 在Network请求列表中，对命中规则的请求标记颜色，pattern可以是正则
```
pattern style://color=@fff&fontStyle=italic&bgColor=red
```

# 替换Set-Cookie
这里示例增加SameSite和Secure的Cookie属性
```
pattern headerReplace://res.set-cookie:/example\.cn/=example.cn%3B%20SameSite%3DNone%3B%20Secure
```

# 添加请求参数
```
pattern reqMerge://{"a":"1","b":"2"}
```

# 添加Header头
```
pattern reqHeaders://X-Forwarded-Proto=https
pattern reqHeaders://{"uin":"","skey":""}
```

# 使用代理请求Host

> 可组合Host代理一起使用


```
pattern enable://proxyHost proxy://127.0.0.1:12639 
```

# 替换UA头（值需要进行一次encodeURIComponent）
```
pattern reqHeaders://User-Agent=Mozilla%2F5.0%20(Macintosh%3B%20Intel%20Mac%20OS%20X%2010_15_6)%20AppleWebKit%2F605.1.15%20(KHTML%2C%20like%20Gecko)%20Version%2F14.0.3%20Safari%2F605.1.15
```

# 如果有一些带有空格的参数，无法进行配置，可使用Values进行设置
## 例如配置UA头：
# Values 中配置 IE11，内容直接填对应的UA头即可
```
/./ ua://{IE11}
```

## 例如配置Header头
# Values 中配置 HEADERS，内容为(可以为多个，一行一个)
```
"Header Name1": "Header Value1"
"Header Name2": "Header Value2"
```

在Rules中配置对应规则即可
```
/./ reqHeaders://{HEADERS}
```