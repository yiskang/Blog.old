title: "git submodule 介紹"
date: 2015-04-16 13:46:36
categories:
- Tech
tags:
- git
---

### 簡介
最近為了方便管理專案，將他拆成了好幾個小專案來維護，然後透過參考引入想要的檔案。但 git 沒辦法像 SVN 那樣只單獨下載一個檔案，它必需整個 repository 都 clone 下來，可是整個 clone 下來還要把想要的檔案分別丟到對的位置，這樣好像太麻煩了，還好 git 有提供 submodule 這個機制可以用來做外部資源參考與更新，解救了我這個懶人～～～ XD

### 新增 submodule
指令：
```bash
git submodule add {repository}      {path/folder name}
```

範例：
```bash
git submodule add https://github.com/yiskang/hexo-theme-pure.git  theme/pure
```

<b>注意：</b>在下新增指令前，請注意<span style="color:red;font-wegiht:bold;"> {path/folder name} </span>的部份，先不要新增空目錄，git 自己會新增，不然 會產生衝突，submodule 就會無法新增。<b>不需要為 submodule 建立目錄</b>

新增完後會看到類似下面的內容：
```bash
Cloning into 'theme/pure'...
remote: Counting objects: 202, done.
remote: Compressing objects: 100% (27/27), done.
remote: Total 202 (delta 14), reused 0 (delta 0), pack-reused 175
Receiving objects: 100% (202/202), 49.48 KiB | 0 bytes/s, done.
Resolving deltas: 100% (84/84), done.
Checking connectivity... done.
```
這時候輸入 <code>git status</code> ，就會發現多了兩檔案需要 commit:
```bash
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
      new file:   .gitmodules
      new file:   theme/pure
```
此外，git 會將 submodule 的資訊記錄在 .gitmodules 裡面:
```bash
[submodule "theme/pure"]
      path = theme/pure
      url = https://github.com/yiskang/hexo-theme-pure.git
```
最後記得要 commit :
```bash
git commit -m "Add submodule pure theme"
```

### 更新 submodule
每個 submodule 獨自更新：
```bash
cd {module folder}
git pull origin master
```

但我很懶的，都用這個直接更新整個專案的 submodule
```bash
git submodule foreach git pull
```

### 下載有 submodule 的 repository
下載 remote repository 到 local 端：
```bash
git clone https://github.com/yiskang/Blog.git
```
註冊 submodule 到 .gitmodules ，告訴 git 要新增哪些 modules
```bash
git submodule init
```
將 submodule 的內容下載下來：
```bash
git submodule update
```

### 移除 submodule
如果不要想使用某個 submodule 了，要移除它要怎麼做呢？我們可以透過下面的步驟將它移除，但在移除前還有一些動作要做！移除 submodule 時得告訴 git 你要移除的 module 名稱，這名稱要去哪找？透過 .gitmodules 就可以啦，在新增 submodule 時，git就將它記錄在 .gitmodules 裡了。那假設現在要移除 pure theme module，我們可以在 .gitmodules 找到這樣的描述：
```bash
[submodule "theme/pure"]
      path = theme/pure
      url = https://github.com/yiskang/hexo-theme-pure.git
```
module 明稱就是上面的 path，現在要移除 pure theme module，所以就是 theme/pure。 接著就可以開始進行移除了，移除 submodule 的命令就是：
```bash
git submodule deinit {path/folder name}
git rm {path/folder name}     or  git rm --chched {path/folder name}
```
現在要將 pure theme module 移除，將上面的 {path/folder name} 換成 theme/pure：
```bash
# 先移除 submodule 裡面的內容
git submodule deinit theme/pure
# 移除資料夾
git rm theme/pure
# 或者你不想留下先前的修改記錄，要將它從 Woking Tree 移除
git rm --cached theme/pure
```
移除完以後，可以從 git status 看到：
```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
      modified:   .gitmodules
      deleted:    theme/pure
```
最後記得 commit：
```bash
git add -A
git commit -m "Remove submodule pure theme"
```
