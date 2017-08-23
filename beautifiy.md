在這邊我們預計實現團隊中使用 sublime + Atom 的開發人員都能夠對 `.scss` 做自動縮進，並且效果必須一樣。

- 縮進書寫規範：兩格空白

每個團隊或個人使用的 CSS 規範不盡相同，可以在細節部分自行調整，也可以參考一些[CSS编码规范](https://github.com/fex-team/styleguide/blob/master/css.md)

有的人喜歡四格縮進，也有喜歡兩格的。

## Atom

安裝 atom-beautify

command line 裡面輸入 `apm install atom-beautify`

![螢幕快照 2017-08-21 下午2.10.56.png](http://user-image.logdown.io/user/15503/blog/14681/post/2203152/AXwv2N1XRQyUeGdlAoFf_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-08-21%20%E4%B8%8B%E5%8D%882.10.56.png)


安裝完畢之後，請完全關閉 Atom 後重新啟動。

接著嘗試打開 .scss 的檔案，按下 `command + shift + p` 並輸入 Beautify，選擇 run Beautify Editor。

![1c8d975c-4085-11e6-8307-e35df7430a10.png](http://user-image.logdown.io/user/15503/blog/14681/post/2203152/O3XHE8i8RmmeZtWxOsaQ_1c8d975c-4085-11e6-8307-e35df7430a10.png)

你就會看到 SASS/SCSS 自動進行縮進排列。

如果要做到存檔自動 beautify ，請鍵入 `cmd + ,`，進入 package setting 的介面，找到 `atom-beautify` 點擊 settings，並往下拉找到 Sass 或是 Scss，將 Beautify On Save 打勾。

![螢幕快照 2017-08-21 下午2.23.17.png](http://user-image.logdown.io/user/15503/blog/14681/post/2203152/GW4DuAQuG8IpmbnJAkxg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-08-21%20%E4%B8%8B%E5%8D%882.23.17.png)

- 將 Default Beautifier 換成 SassConvert
- 打勾 Bautify on save (option，看個人，非必選)

![螢幕快照 2017-08-21 下午3.01.46.png](http://user-image.logdown.io/user/15503/blog/14681/post/2203152/Cgus6KFbTKMxvxU8eX8A_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-08-21%20%E4%B8%8B%E5%8D%883.01.46.png)

那麼未來在開發 Sass 的時候，將在存檔(Command + S)的時候自動整理縮進。


## Sublime

用 [Install Package](https://packagecontrol.io/installation) 安裝 [SassBeautify](https://github.com/badsyntax/SassBeautify)

注意：正常來說不需任何設定就可以直接使用，預設自帶 4 格縮排，可以依照團隊規範調整，依此文章設定是兩格縮排，所以我們客製化內容如下

### 安裝開始

`Preferences >> Package Settings >> SassBeautify >> Settings - User`

將下面的內容複製上去

```
{
  // How many spaces to use for each level of indentation. "t" means use hard tabs.
  "indent": 2,
  // Convert underscores to dashes.
  "dasherize": false,
  // Output the old-style ":prop val" property syntax. Only meaningful when generating Sass.
  "old": false,
  // Custom environment PATH.
  "path": fasle,
  // Custom environment GEM_PATH.
  "gemPath": false,
  // Beautify the sass file after saving it?
  "beautifyOnSave": false,
  // Keep "inline" comments inline?
  "inlineComments": false,
  // Add a new line between selectors?
  "newlineBetweenSelectors": false,
  // Use single quotes everywhere
  "useSingleQuotes": false
}
```

這邊可以直接打開 .scss 檔案，用 `command + shift + p` 來搜尋 `SassBeautify`，按下 enter，就會自動縮排了

![螢幕快照 2017-08-21 下午2.31.45.png](http://user-image.logdown.io/user/15503/blog/14681/post/2203152/qw01tv9pRAuxgPgB3IgQ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202017-08-21%20%E4%B8%8B%E5%8D%882.31.45.png)

如果有跳 error ，應該是你的相依檔案路徑他找不到，可以依照官方的解法進行排除

#### Compatibility with RVM/rbenv

You need to specify the custom PATH and GEM_PATHvalues in your SassBeautify user settings.

Follow the steps below:

1. Open up terminal
2. Run: echo $PATH
3. Copy the entire PATH into the 'path' setting
4. Run: echo $GEM_PATH
5. Copy the entire GEM_PATH into the 'gemPath' setting

Done.


## 後記心得

Atom 編輯器在使用 `atom-beautify` 插件後，可以選擇處理 sass 的 beautifier，預設是使用 `pretty diff` ，而且最坑的是下方的客製化選項 `只支援pretty diff`，簡單說，如果你想用 SassConvert，那你就無法調整預設 indent 為兩格的設置。

因為選項竟然都只支援 `pretty diff`...

偏偏 `pretty diff` 和 `SassConvert` 整理出來的 SASS 又有些微不同

- pretty diff 的註解與樣式中間不會有空一行
- SassConvert 的註解與樣式中間會有空一行

所以如果團隊中用兩個不同的編輯器，只要 beautifier ，設定的不一樣，你就會看到 git commit 永遠一直在變動一大堆結構，這會使 PR 更難閱讀。

所以本文章實現了兩個不同編輯器卻能有同樣的自動化整理風格是退一步求其次，將原先的 SassConvert 自帶的四格縮進改為兩格，與 Atom 的 beautify 一樣，就可以排除這奇怪的問題了。

