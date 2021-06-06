---
title: "[教學]用Github Pages+Hexo建立網站分享"
date: 2021-06-06 12:47:23
categories: "教學"
tags: 
   - "Github Pages"
   - "Hexo"
---

建立個人blog的動機，比起的個人心得分享，更多的是看越來越多朋友建立了自己的blog，心裡就很想跟著玩玩。
本篇作為blog第一篇文，就先把整個blog的建立流程記錄起來，以防自己忘記。
本文主要參考自[這裡](https://blog.jaojaolin.com/%E8%BB%9F%E9%AB%94%E8%88%87%E7%B3%BB%E7%B5%B1/2020-05-06-Hexo-GitPage-%E6%90%AD%E5%BB%BA-Blog-%E6%95%99%E5%AD%B8/)。

個人建立環境是Windows10+wsl2的Ubuntu 20.04。大部分流程都是在Windows Terminal上完成的，所以基本上都是用Linux指令，完全沒有使用到Windows cmd。

Github Pages只支援靜態網頁設計，基本上就是html, css, javascript等，所以只能拿來寫寫部落格或放一些文件，與使用者做互動編譯的動態網頁將無法成功顯示。

# Prerequisite
## Github Repo
先在[Github](https://github.com/)上建立個人Repo，取名做`<username>.github.io`，<username>填入個人帳號。可見[這裡](https://github.com/Ergodica10002/Ergodica10002.github.io)。
接著將Repo clone到本地端，個人還是習慣在terminal上運作git。
```bash=
git clone https://github.com/<username>/<username>.github.io.git
cd <username>.github.io.git
```
接著可以在Repo內新增`index.html`，commit+push上去後，應該就能在`https://<username>.github.io`上看到剛剛編輯的內容了。

另外到Github上個人的Repo裡，點選Settings->Pages，可以看到Choose a Theme，裡面已有許多Github預設的主題可以使用。

![](https://i.imgur.com/6PgAFYW.png)

底下還可以修改domain，不過目前也沒這需求，維持原本的github.io就好XD。

## 安裝Hexo
Hexo是個簡單的部落格建立軟體，支援Markdown編輯。雖然是基於Node.js，但個人目前還沒碰過javascript，照著指示也還是完成了。
首先先安裝[npm](https://www.npmjs.com/)(node package manager)，這是專屬Node.js的套件管理工具。
```bash=
sudo apt update
sudo apt install npm
```
可透過`npm --version`確認安裝是否成功。

![](https://i.imgur.com/hkYW6vk.png)

接著安裝`Hexo-cli`，這是能透過terminal操作Hexo的套件。
```bash=
sudo npm install hexo-cli -g
```
`-g`參數能讓我們在全域環境皆能使用。


# 建立網頁
先建立個人專案，透過以下指令。
```bash=
hexo init blog
```
其中`blog`可以換成自己想要的任何名稱。如果順利應該可以看到當前資料夾多了一個叫`blog`的資料夾。進入該資料夾
```bash=
cd blog
npm install
```
建立完成後，可以看到裡面已有許多的package。底下說明各檔案意義。
* `node_modules/`: 透過npm安裝的套件會放在這邊。
* `scaffolds/`: 新增貼文的模板。
* `source/`: 新增貼文的原始碼。Markdown 和 HTML 檔案會被處理並放到`public`資料夾(等等會介紹)。
* `themes`: 貼文的主題。
* `_config.yml`: 網站的設定檔 
* `package.json`: 應用程式的相關資料

## 設定網頁資訊
選擇任意editor打開`_config.yml`。個人使用sublime。
修改網站的基本內容，如圖。

![](https://i.imgur.com/HtjNHA4.png)

可以自己置換相關的資訊。
接著為了讓網站內容deploy到Github Page上，要在`_config.yml`最後加上底下資訊。

![](https://i.imgur.com/10zjCUM.png)

## 產生檔案

將整份專案編譯產生靜態檔案，編譯完後檔案會存在`blog/public`底下。
```bash=
# 可先用hexo clean清理目前資料夾中的靜態網頁
hexo generate # or hexo g
```
個人在這步有出現Error:
```
FATAL { err:
   TypeError: line.matchAll is not a function
```
研究一陣子後發現應是Node.js版本太舊。先安裝nvm(node version manager)。
```bash=
wget -q0- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
# 個人是使用zsh，因此修改成
# wget -q0- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | zsh
```
接著重啟terminal或重新source .rc檔。
```bash=
source ~/.bashrc
# 個人是使用zsh，因此修改成
# source ~/.zshrc
```
接著確認是否安裝成功。

![](https://i.imgur.com/pZB3SbK.png)

接著透過`nvm ls-remote`，確認要安裝的版本，個人是安裝LTS。透過`nvm install <version>`安裝

![](https://i.imgur.com/nfTptAp.png)

現在重新`hexo generate`應該就可以了。這步驟會將在`source`裡的`Markdown`和`HTML`檔案處理，並放到`public`資料夾，而`public`裡就是最後網頁呈現的結果。

## 新增文章
以下透過`Markdown`語法新增文章。選擇文章標題`"title"`。
```bash=
hexo new "title"
```
接著可以在`blog/source/_posts`看到`title.md`檔案，編輯後`hexo generate`就能產生相關網頁文件。

## 檢視成果
可以在本機伺服器啟動網頁看看成果。
```bash=
hexo server #or hexo s
```
預設網頁會放在`http://localhost:4000`。

## 部署至Github Pages
透過以下指令將內容push到remote上。
```bash=
hexo deploy
```
現在可以在`https://<username>.github.io`上檢視剛剛編輯的成果了！
*網頁更新可能會需要幾分鐘的時間*