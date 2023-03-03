---
title: "PHP, python: serwer WWW uruchamiany z wiersza poleceń"
description: "Jak szybko uruchomić serwer WWW z wiersza poleceń?"
image: /img/2023-02-12-23-01-39.png
date: 2022-05-25
hidden: false
comments: true
draft: false
tags:
    - php
    - python
    - oneliner
    - programowanie
categories:
    - PHP
    - Python
    - Oneliner
    - Programowanie

---


Jak szybko uruchomić serwer WWW z wiersza poleceń? 

kilka sposobów:

## PHP
```
php -S 127.0.0.1:8080 -t ./www
```
## python
```
# python 3.x
python -m http.server 8080
# python 2.X
python -m SimpleHTTPServer 8080
```

## źródła

- https://gist.github.com/willurd/5720255 - Big list of http static server one-liners
