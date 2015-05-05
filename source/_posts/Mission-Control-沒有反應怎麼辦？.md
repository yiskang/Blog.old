title: "Mission Control 沒有反應怎麼辦？"
date: 2015-05-02 09:49:33
categories:
- Tech
- Mac OS
tags:
- OS X
---

最近變的很不愛關電腦，常常螢幕一蓋就收到包包裡了。但久沒有重開機，有些應用程式就會不乖，突然沒有反應了，像這次不乖的就是 Mission Control。它掛掉的當下，我剛好在用 Evernote 語音記事記錄演討會的內容，沒辦法重開機，非常囧！！！還好 Mission Control 可以在不重開機的狀態下重開，以下是我使用的方法，供大家參考！（當然在使用前必需先開起 Terminal ～）

### 比較暴力的作法
```bash
$ killall Dock
```

### 溫柔的作法
```bash
$ osascript -e 'quit application "Dock"'
```
Reference: [10.7: Restart Mission Control](http://hints.macworld.com/article.php?story=20110802073945173)
