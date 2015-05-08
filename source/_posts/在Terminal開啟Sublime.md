title: "在 Terminal 開啟 Sublime"
date: 2015-04-29 17:14:54
categories:
- Tech
- OS X
tags:
- Hexo
---

開使用 Hexo 寫筆記以後，常常都要先 hexo new 一則文章，在用 vim 開啟他。然後問題就來了，我很多時候都要在文章裡面貼上程式碼的內容，但因為我有開啟 vim 的自動縮排功能，直接貼上去後，程式碼就會被縮排縮到找不到內文，自作孽啊... 囧rz

就因為這樣我想找個類似 UltraEdit 的軟體來用，然後聽說 Sublime 似乎不錯，但每次開啟 Hexo 的 Markdown 檔案都要做拖拉的動作，這時候我的懶毛病就犯了！好我想讓 Sublime 跟 vim 一樣可以直接在 Terminal 開啟文章的 md 檔，那要怎麼做呢？以下就是我所做的設定：

1. 先測試可不可以直接啟動 Sublime
```bash
$ /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl
```
2. 如果可以的話，現在為 Sublime 建立一個 alias：
```bash
alias sublime="/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl"
```
3. 然後把他加到 shell 的 rc 檔裡面，以下以 zsh 為例：
```bash
$ echo 'alias sublime="/Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl"' > ~/.zshrc
$ source ~/.zshrc
```

Reference: [在 Terminal 啟動 Sublime Text](http://azyukei.github.io/2015/04/Sublime-Text-OSX-Terminal-Launch/)
