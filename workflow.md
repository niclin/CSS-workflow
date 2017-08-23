CSS開發規範

## 命名禁止縮寫

請精簡扼要的對 class 命名，請勿使用自定義縮寫

class name 的命名必須是行為、有語意的

## 禁止在非特殊情況寫 !important

CSS裡面本有權重設計，這樣一來任意的使用 !important 會造成權重混亂而無法維護，最後的情況就是互相
!important來!important去

## 不可輕易侷限寬高

請不要忘記用戶可以設定自己的瀏覽器，例如 andorid 的手機可以設定顯示字體大小，寫死的高度會讓字體相互重疊

RWD 失效

行動裝置（手機, ipad）的高是無限，寬是有限

請不要把寬寫死

當你在桌機板把高寫死
- 頂多就是往下掉

當你在桌機板把寬寫死
- 手機版就破版
- 手機版就破版
- 手機版就破版

## img 請讓他自動縮放

請不要替 img 的容器設定寬或高，請讓他依裝置縮放

請使用 bootstrap 的 img-responsive

如果你非要設定請用

```
width:100%;
height: auto;
```

假設如果要給 img border-radius 的 style

請用父元素控制行為，保持 img 只載入圖片，不有樣式

## 優先使用 grid 排版

請不要花一堆時間在寫 media query，定一堆 breakpoint，自己寫元件樣式，自己控制每種裝置上的容器寬度。

請使用 grid sysytem，這些都是已經成熟的框架，而且有些也已經幫你處理了瀏覽器相容問題，請不要引入了然後都不使用，都自己寫

## 不可直接 over write 或加料在原本框架的 class

請直接寫一個新的 class，不要覆蓋原有的設計，舉例來說

如果你真的很討厭 bootstrap container 自帶的 padding

那你可以寫一隻

.no-padding {}

在使用的情況下

```
<body class="container-fluid no-padding">
</body>
```

可以一目了然這是沒有 padding 的 container。

也請不要在以有的 class 上加料，請額外單獨寫一個

```
.container-fluid {
 font-size :18px
}
```


## 手機先決 如果製作 RWD網站，設計請以手機排版優先設計
設計師，設計順序，以桌面版優先，再設計手機版
前端工程師，拿到視覺圖，欲刻 HTML / CSS 時以手機版為第一優先

手機開啟網頁很吃手機效能和網路狀況
關於前端工程師開發
一開始就以Mobile為優先，
可以讓 HTML一開始載入，在不必推移下，動用最少的效能快速載入網頁
當你開始製作 Desktop 時，只會些微跑版，畫面不易跑版到無法找到的位置。

情況反過來，先作桌面版時，當手機版畫面被切掉或是跑位
你需要花更多時間去通靈，要移動多少px才能回到畫面上？

再來是Iphone 上的 retina ，會將圖片放到手機上時，自動做兩倍縮小
在一開始製作時即可發現圖片載入是否吃效能
那也當然為了讓圖片能在iphone 上有更好的體驗，會花較多工時
所以建議Mobile first

Mobile First 優點是
在 mobile 時沒有任何 media query 載進來

當偵測到 media query 時，表示效能已經提升了（因為已經不是行動裝置了）

### RWD 精隨

行動裝置（手機, ipad）的高是無限，寬是有限

請不要把寬寫死

當你在桌機板把高寫死
- 頂多就是往下掉

當你在桌機板把寬寫死
- 手機版就破版
- 手機版就破版
- 手機版就破版




## 不可使用 html tag selector
樣式不必要讓子子孫孫都背負，請直接定義 class 的樣式就好，不需要指定 html tag。
如果我要換 html tag, 那 CSS 不就要跟著改？

## 層級不可以超過三層
超過表示耦合度太高，不具有彈性、可維護性

## 用一樣的 Element 時不要把一堆東西全部寫在裡面，請把排版相關的獨立出來
把 border-radius 做在 img 上面，請把 img 保持乾淨，
定位，例如 postition absoulate

## 不要隨意 none 掉畫面上的 tag 或行為

請注意如果要 none 掉一些樣式，請依照使用程度決定

使用程度遍及整個網站，請直接做 reset.css

使用程度中等以下，請定義一個 class

例如 Rails 裡面的 simple form

<%= f.input :title %>

他會多帶一個 label tag 出來，如果你想關掉，請直接寫

<%= f.input :title, label: false %>

## reset.css

常見的
- a tag 不要有 underline
- list 消除原有樣式

請在 reset.css 上定義，並且設為第一隻載入

（套用框架 bootstrap 可以在文件上統一 overwrite 掉）

## 有 JavaScript 行為的 class 可以為命名加入 name space

```
#js-project-show {}
```

## 請勿任意使用  br hr tag

br是換行，請使用在 p tag 裡面，當 p 裡面文字過多時可以使用。
hr 是快速劃線，但是快被時代淘汰了，請直接用 border 寫在 class 裡面

br 必須去思考父區塊是不是 display:block;，如果要換行，應該思考是不是下一段文字？

線條請都使用 border 去寫
