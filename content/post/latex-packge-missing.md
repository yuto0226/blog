---
title: 'Latex 編譯時缺少 .sty 檔案'
date: 2022-11-21 01:04:43
categories:
- Troubleshooting
tags:
    - 'Latex'
    - '除錯紀錄'
---
用 [CTAN](https://ctan.org/pkg) 單獨把遺失的檔案載回來，整個資料夾放回 `C:\texlive\<年分>\texmf-dist\tex\latex`，然後在 Terminal 裡面 :
```bash command:("[root@localhost] $":1)
texhash
```

