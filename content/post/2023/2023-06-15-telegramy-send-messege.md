---
title: "Telegram - wysyłanie wiadomości przez API"
description: ""
date: 2023-06-15
hidden: false
comments: true
draft: false
tags:
    - telegram
    - api
categories:
    - API
    - PHP
---


```
https://api.telegram.org/bot<API-KEY>/getUpdates <- tu mozna szukać id grupy
```

```
https://api.telegram.org/bot<API-KEY>/sendMessage?chat_id=<CHAT-ID>&text=Wiadomosc
```

### Użycie Telegrama w Mikrotiku

```
/tool/fetch url="https://api.telegram.org/bot<API-KEY>/sendMessage" http-method=post http-data="chat_id=<CHAT-ID>&text=Wiadomosc
```



