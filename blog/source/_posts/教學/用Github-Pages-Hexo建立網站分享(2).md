---
title: "[教學]用GitHub Pages+Hexo建立網站分享(2)--NEXT主題"
date: 2021-06-07 16:43:17
updated: 2021-06-14 14:27:00
categories: "教學"
tags: 
   - "Github Pages"
   - "Hexo"
---
自建立部落格後，又花了不少時間更新內容。這邊就記錄下最近完成的內容。

另外有個心得是，每次更新頁面設定一定要從頭進行`git clean`,`git generate`，否則`git deploy`後的結果可能會出錯，有機會會和`git server`不同。另外檢查網站更新情況可以用`Ctrl+F5`取代單純的`F5`，確保資料是重新獲取而不是來自cache。

這篇主要是如何使用NexT主題的基本介紹，個人使用版本是NexT 8.5.0。詳細內容與demo可以參考NexT的[blog](https://theme-next.js.org/)。
另外本篇內容主要參考自[網站](https://ed521.github.io/2020/05/hexo-next-upgrade/)。

<!--more-->

# Prerequisite
* {% post_link 教學/用Github-Pages-Hexo建立網站分享(1) %}

# 設定tags, categories
進入個人網站的根目錄，依序輸入指令。
```bash=
hexo new page tags
hexo new page categories
```
接著進入sourcevu，應該會看到新增了兩個資料夾`tags`,`categories`，裡面各有一個`index.md`，修改其中的內容。
* tags:
```
title: tags
date: #your update date
type: "tags"
```
* categories:
```
title: categories
date: #your update date
type: "categories"
```

接著就可以對每篇文章新增所屬的tag及category。其中tag一篇文章可以有好幾個，而categories一篇文章只能有一個。
如範例，在文章開頭編輯:
```
---
title:
date:
categories: "教學"
tags: 
   - "Github Pages"
   - "Hexo"
---
```
這樣可以讓這篇文章新增在`教學`這個category下，且帶有`Github Pages`,`Hexo`這兩個tag。

另外可以修改`/scaffolds/post.md`，讓每次新增文章`hexo new post`時，都帶有category與tag的設定。
```
---
title: {{ title }}
date: {{ date }}
cetegories:
tags:
---
```
# 設定主題NexT
Hexo要新增主題很簡單，只要將該主題的Repo clone到`themes/`這個資料夾底下就可以了。欲使用[NexT主題](https://github.com/next-theme/hexo-theme-next)，在個人的`blog`跟目錄底下使用指令
```bash=
git clone https://github.com/next-theme/hexo-theme-next themes/next
```
這樣會在`themes/`底下建一個資料夾`next/`，接者進入`_config.yml`中修改使用主題成next
```yaml=
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```
重新生成就會看到主題變更了。

# NexT基本設定
打開`themes/next/_config.yml`。裡面可以設定使用者自己的資料。基本上每個項目都有註解教你各功能代表的意思，底下僅介紹我覺得重要的。
## 主題設定
搜尋檔案找到`scheme:`
```yaml=
# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini

# Dark Mode
darkmode: true
```
NexT設有4種scheme可以選擇(Muse,Mist,Pisces,Gemini)，取消註解即可使用。
另外可以選擇深色模式，打開`darkmode`即可。

## Menu設定
搜尋檔案找到`menu:`
```yaml=
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```
取消掉註解即可顯示該項目，其中每一個項目裡，`||`左邊表示愈顯示的內容，右邊則表示使用的icon，icon可以至[網站](https://fontawesome.com/v5.15/icons?d=gallery&p=2)找尋自己喜歡的取代。

## 頭像設定
搜尋檔案找到`avatar:`
```yaml=
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```
在`url`裡放入圖片連結即可更改頭像。例如將頭像圖片`avatar.jpg`放入`themes/next/source/images`裡，圖片連結就是`/images/avatar.jpg`

## Social設定
搜尋檔案找到`social:`
```yaml=
social:
  GitHub: https://github.com/Ergodica10002 || fab fa-github
  E-Mail: mailto:ergodica10002@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  FB Page: https://www.facebook.com/gengyuc || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  Instagram: https://instagram.com/garychen_0126 || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype
```
這邊可以設定網站sidebar會顯示的連結，一樣可以修改`||`右邊的內容來使用想要的圖片。

## footer設定
搜尋檔案找到`footer:`
```yaml=
footer:
  # Specify the year when the site was setup. If not defined, current year will be used.
  since: 2021

  # Icon between year and copyright info.
  icon:
    # Icon name in Font Awesome. See: https://fontawesome.com/icons
    name: fas fa-camera
    # If you want to animate the icon, set it to true.
    animated: false
    # Change the color of icon, using Hex Code.
    color: "#636363"

  # If not defined, `author` from Hexo `_config.yml` will be used.
  copyright:

  # Powered by Hexo & NexT
  powered: false
```
這邊設定網站末尾會有的標示。`icon`項目可以修改使用的icon，預設是愛心，我將其修改為一台相機，並調整顏色為灰色。
另外`powered`在true的情況下，網站末尾會有類似的文字
![](https://i.imgur.com/tx8ryjc.png)
設為false即可關掉。

## 程式碼區塊設定
搜尋檔案找到`codeblock:`
```yaml=
codeblock:
  # Code Highlight theme
  # All available themes: https://theme-next.js.org/highlight/
  theme:
    light: default
    dark: tomorrow-night
  prism:
    light: prism
    dark: prism-dark
  # Add copy button on codeblock
  copy_button:
    enable: true
    # Available values: default | flat | mac
    style:
```
這邊可以修改想要的程式碼樣式，底下的`copy button`設true可以讓程式碼區塊帶有copy功能。

## 右上角Github連結
```yaml=
# `Follow me on GitHub` banner in the top-right corner.
github_banner:
  enable: true
  permalink: https://github.com/Ergodica10002
  title: Follow me on GitHub
```
修改link為個人的github網站，這樣網站右上角會有個icon可以進入。

## 新增站內文章搜尋功能
找到底下內容，將`enable`設為true。
```yaml=
# Local Search
# Dependencies: https://github.com/next-theme/hexo-generator-searchdb
local_search:
  enable: true
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false
```
接著須至terminal上安裝工具
```bash=
npm install hexo-generator-searchdb --save
```
最後在blog的根目錄的`_config.yml`裡加上
```yaml=
# 文章搜尋功能
search:
  path: search.xml
  field: post
  content: true
  format: html
```
更多細節可以參考[這裡](https://github.com/theme-next/hexo-generator-searchdb#Options)。

## 更換背景圖片
在next底下的`_config.yml`，取消註解掉style這句。
```yaml=
custom_file_path:
  #head: source/_data/head.njk
  #header: source/_data/header.njk
  #sidebar: source/_data/sidebar.njk
  #postMeta: source/_data/post-meta.njk
  #postBodyEnd: source/_data/post-body-end.njk
  #footer: source/_data/footer.njk
  #bodyEnd: source/_data/body-end.njk
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  style: source/_data/styles.styl
```
接著在blog的根目錄的`source/`新增`_data/`資料夾，在裡面新增一個檔案`styles.styl`，裡面寫入
```
body {
      background:url(/images/圖片的檔名);
      background-size: cover;
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-position:center center;
}
```
圖片要放在`themes/next/source/images`，才能成功讀取。
另外可以在上述的`source/_data/styles.styl`檔案後面加入
```
.main-inner {
      opacity: 0.9;
}
```
如此可以為網站文章設定透明度，讓背景圖片更明顯。