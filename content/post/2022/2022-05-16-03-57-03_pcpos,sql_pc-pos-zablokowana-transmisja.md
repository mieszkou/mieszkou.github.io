---
title: "PC-POS: zablokowana transmisja"
description: 
date: 2022-05-16
image: /img/2023-02-12-23-08-32.png
hidden: false
comments: true
draft: false
tags:
    - insoft
    - pcpos
    - sql
categories:
    - Insoft
---

## Problem

Transmisja zatrzymuje się na jednym z dokumentów.

## Rozwiązanie

- 11234 - id dokumentu na którym staje łączność

```sql
Select top 100 externalid, * from receipt where receiptid > 11230

UPDATE receipt set isactive = 0 where receiptid = 11234 
```