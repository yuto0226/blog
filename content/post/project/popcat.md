---
title: POPCAT 自動連點器
date: 2021-08-18 19:13:26
img: https://i.imgur.com/BoGQnP1.jpg
categories:
    - 作品
tags:
    - Python
    - 網路爬蟲
    - Hack Life
---
# 前言
近期Pop cat風靡全球 大家都想拿到第一名
什麼是Pop cat? 這就要從一隻可愛的貓說起
>Popcat風潮來自推特上一段爆紅的貓咪影片 這隻名為Oatmeal的貓咪正在向主人Xavier撒嬌 嘴巴一開一合的 樣子非常可愛
>Xavier也把Oatmeal的圖片做成gif圖 後來被他的朋友PO到Reddit論壇上 突然爆紅 被歐美網友們做成各式各樣的迷因（meme） 搭配上「POP」的音效
>-數位時代。檢自https://www.bnext.com.tw/article/64440/popcat-click-competition-janis (2021/08/19)

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">So there&#39;s a video with some images of my cat Oatmeal out and here&#39;s the full clip of him chirping at a bug. <a href="https://t.co/4MVTWiIknc">pic.twitter.com/4MVTWiIknc</a></p>&mdash; Xavier (@XavierBFB) <a href="https://twitter.com/XavierBFB/status/1315184155274211329?ref_src=twsrc%5Etfw">October 11, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

我那時就想 一直點一直點手很酸 國外也有人用連點器 (物理)
那為什麼我不來試看看用程式寫
然後又剛好看到 Youtube 上的 Selenium 教學
剛好可以讓我寫出連點器 於是便著手編寫了

# Selenium
>Selenium 是一個綜合性的項目，為web瀏覽器的自動化提供了各種工具和依賴包

要在 Python 中使用 Selenium 要先安裝它的套件
```shell
$ pip install selenium
```
然後要安裝對應的 WebDriver 才能讓它在瀏覽器上面跑
這邊就用 Chrome ([網址][ChromeDriver])
記得要挑對版本下載
下載完後把他丟到程式檔案的同一個資料夾就可以了

[ChromeDriver]:https://sites.google.com/a/chromium.org/chromedriver/downloads

# 程式碼
Github:  [連結](https://github.com/yuuto-0226/popcat_autoclick)
```py
from selenium import webdriver
import time
import random

PATH = "./chromedriver.exe"

driver = webdriver.Chrome(PATH)

driver.get("https://popcat.click/")
neko = driver.find_element_by_id("app")

# 隨機點擊次數及休息時間
click_random = int(random.random()*500)
sec_random = int(random.random()*5)

c = 0
while c < 1:
    for i in range(click_random):
        neko.click()
    time.sleep(sec_random)
```
