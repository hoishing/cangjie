# Personalize Cangjie IME in Windows

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hoishing/cangjie/HEAD?labpath=create_code.ipynb)

🔗 [source code](https://github.com/hoishing/cangjie)

A utility to customize the [DIME](https://github.com/jrywu/DIME) CangJie(倉頡) IME in Windows. It allows you to build your own IME character set, such that you may define / amend:

- the exact characters in your CangJie IME character set
- the order of output candidates when more then one character matches the input
- custom characters that not exist in official character sets
- the input code of characters

## Files

- `common.txt` ~4800 commonly used chars from [常用國字標準字體表](https://zh.wikisource.org/wiki/常用國字標準字體表)
- `lessCommon.txt` ~6300 less common chars from [次常用國字標準字體表](https://home.gamer.com.tw/creationDetail.php?sn=4907610)
- `char_rank.txt` ranked chars from Taiwan Ministry of Education [字頻表排序](http://language.moe.gov.tw/001/Upload/files/SITE_CONTENT/M0001/86NEWS/download/86rest17.TXT)
- `add_on_char.txt` your custom add-on chars, eg. 粵語用字
- `char_db.csv` cangjie input of all chars
- `duplicated_code.txt` rare chars having same input code with others, to be removed from the final character list
- `create_code.ipynb` program that create the character list used in [DIME](https://github.com/jrywu/DIME) input method
- `dime_cangjie.txt` final character list to be imported to DIME

## Prerequisite

```toml
python = "^3.9"
jupyter = "^1.0.0"
```

## Usage

- install the above python packages
- run `create_code.ipynb` to generate the character set, say in VSCode
- import the generated `dime_cangjie.txt` to DIME
- enjoy your custom made Cangjie IME 🎉

## Blog - 打造你專屬的倉頡輸入法

我是倉頡輸入法的使用者，在 windows 10 之前，微軟倉頡輸入法是可以選擇只顯示 big5 字元的。但 windows 10 之後這選項便不復存在。

我想只顯示 big5 是因為 unicode 有非常多的的罕用字，這導致嚴重的重碼問題，而那些罕用字在大部分情況下根本用不著，它們只會降低我的輸入速度和爽快感。

我嘗試在各論壇詢問是否可設定只顯示 big5 字元，截至 windows 10 version 2004，還是沒有辦法設定的。而最接近的答案，是重新安裝舊版的「微軟新倉頡」輸入法，詳情可看這篇：

https://irregular.enzan.org/post/3292

但它有幾個問題：

1. 聯想字必需按入候選字中才能顯示出來，不能邊打邊顯示。
2. 大五碼本身亦有重碼的問題，例如你打「夢」字他會有 「夢甍藅蘮 」四個輸出。
3. 它是使用 IMM 架構的舊版輸入法，每次更新 windows 便要重裝一次…

既然要安裝另一個輸入法，我在想，有沒有其他的倉頡輸入法可以完全客製化，把那些罕用字刪除，成為我心目中理想的倉頡輸入法呢？

然後我找到一篇關於 [dime 輸入法](https://github.com/jrywu/DIME)的文章：

https://terryhung.pixnet.net/blog/post/35608897

dime 相當接近我要的東西，其可取之處在於：

1. 它是基於新的 TSF 輸入法架構，這樣使輸入法的安裝和移除更加方便，未來的支援更有保障，而且不用每次更新 windows 便要重裝。
2. 它可以自行修改內碼表，這樣我便可以移除一些根本用不到的罕有字，令重碼問題大幅降低。

內碼表應如何製作呢？我先把已做好的內碼表放在這裏給大家參考，是純文字，內容亦相當容易理解：

https://github.com/hoishing/cangjie/blob/main/dime_cangjie.txt

我對內碼表有以下的要求：

1. 不要包含太多罕有字。
2. 重碼字常用的應在前，例如輸入「人大口」，「知」應在「佑」之前。

對於問題一，我的解決方法是使用中華民國教育部編訂的「[常用國字標準字體表](https://zh.wikisource.org/wiki/常用國字標準字體表)」和「[次常用國字標準字體表](https://home.gamer.com.tw/creationDetail.php?sn=4907610)」，其他的字暫時不包括在內，這樣整個字庫加起來只有11000多字。

要解決第二個問題，字庫可依教育部的[字頻表排序](http://language.moe.gov.tw/001/Upload/files/SITE_CONTENT/M0001/86NEWS/download/86rest17.TXT)。

至於每個字對應的倉頡碼，可到政府資料開放平台下載全字庫

https://data.gov.tw/dataset/5961

就這樣，我用 python 把上述的原材料整理一番後
  
🔗 [source code](https://github.com/hoishing/cangjie)

便得出上面的代碼表。然後把它載入 dime 的「自建」輸入法內，一個完全客製化的倉頡便大功告成！

最後對於 dime 的使用，有以下幾點註腳：

1. windows 的 language settings 內並沒有輸入法的設定。先打開 notepad，然後按 ctrl \ 才可進入設定，這是 dime 最需要改善的地方。進入後，記得把 「組字區最大長度」設為 5，因倉頡最長可有五碼。
2. 如果安裝後發現沒有聯想字，可先安裝內置的「微軟注音」輸入法，打開「相容性：使用舊版的微軟注音」，然後把 user folder 內的 appdata\roaming\dime 刪除，再重裝 dime 即可。
3. 安裝 dime 後，它會一拼安裝注音、大易等輸入法，而你要用的只是自建輸入法。要移除不需要的輸入法，你先要在 language setting 中把所有的 dime 輸入法加上去，re-login 後再從 language settings 中移除。
