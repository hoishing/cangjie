# Custom Cangjie IME in Windows

[![GitHub](https://img.shields.io/github/license/hoishing/cangjie)](https://opensource.org/licenses/MIT) [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hoishing/cangjie/HEAD?labpath=create_code.ipynb)

> A utility to customize the [DIME](https://github.com/jrywu/DIME) CangJie(倉頡) IME in Windows.

See my [blog][blog] for the motivation of this project.

## Features

Build your own IME character set, such that you may define / amend:

- the exact characters in your CangJie IME character set
- the order of output candidates when more then one character matches the input
- custom characters that not exist in official character sets
- the input code of characters

## Technical Details

🔗 [source code](https://github.com/hoishing/cangjie)

### Files

- `common.txt` ~4800 commonly used chars from [常用國字標準字體表](https://zh.wikisource.org/wiki/常用國字標準字體表)
- `lessCommon.txt` ~6300 less common chars from [次常用國字標準字體表](https://home.gamer.com.tw/creationDetail.php?sn=4907610)
- `char_rank.txt` ranked chars from Taiwan Ministry of Education [字頻表排序](http://language.moe.gov.tw/001/Upload/files/SITE_CONTENT/M0001/86NEWS/download/86rest17.TXT)
- `add_on_char.txt` your custom add-on chars, eg. 粵語用字
- `char_db.csv` cangjie input of all chars
- `duplicated_code.txt` rare chars having same input code with others, to be removed from the final character list
- `create_code.ipynb` program that create the character list used in [DIME](https://github.com/jrywu/DIME) input method
- `dime_cangjie.txt` final character list to be imported to DIME

### Prerequisite

```toml
python = "^3.9"
jupyter = "^1.0.0"
```

## Usage

- run online with binder [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hoishing/cangjie/HEAD?labpath=create_code.ipynb)

or

- install the above python packages
- run `create_code.ipynb` to generate the character set, say in VSCode
- import the generated `dime_cangjie.txt` to DIME
- enjoy your custom made Cangjie IME 🎉

## Need Help?

Open a [github issue](https://github.com/hoishing/cangjie/issues) or ping me on [Twitter](https://twitter.com/hoishing) ![](https://api.iconify.design/logos/twitter.svg?width=20)

[blog]: https://hoishing.github.io/blog/2020/10/27/cangjie
