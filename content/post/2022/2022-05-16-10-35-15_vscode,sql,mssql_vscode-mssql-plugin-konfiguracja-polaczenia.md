---
title: "VSCode: mssql plugin - konfiguracja połączenia"
description: 
date: 2022-05-16
image: 
hidden: false
comments: true
draft: false
tags:
    - vscode
    - sql
    - mssql
categories:
    - VSCode
    - Programy których używam
---

`Preferences: Open Settings (JSON)`

a w nim konfiguracja połączeń MSSQL:

```json
    "mssql.connections": [
        {
            "server": "127.0.0.1,52019",
            "database": "",
            "authenticationType": "SqlLogin",
            "user": "sa",
            "password": "",
            "emptyPasswordInput": false,
            "savePassword": true,
            "profileName": "SQL2019"
        }
    ],
```

