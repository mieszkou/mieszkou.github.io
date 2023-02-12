---
title: "Electron: creating portable windows application"
description: "Electron: creating portable windows application"
image: 
date: 2022-06-14
hidden: false
comments: true
draft: false
tags:
    - js
    - javascript
    - electron
    - programowanie
categories:
    - JavaSript
    - Programowanie

---


## How to create a portable windows application without an installer from an electron project:

Clone the electron-quick-start repo:
git clone https://github.com/electron/electron-quick-start
yarn
Make your application - probably edit main.js to navigate to some URL
yarn add electron-packager
Edit package.json - update the 'name' and add a new script 'packager':

```json
{
  "name": "my-app-name",
  ...
  "scripts": {
	"start": "electron .",
    "packager": "electron-packager ./ --platform=win32"
  }
}
```

'npm start' will bring up the application
'npm run packager' will package the app for windows. You will see a new directory 'my-app-name-win32-x64' in the top directory of the project, with a my-app-name.exe