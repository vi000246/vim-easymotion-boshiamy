# vim-easymotion-boshiamy

基於 [vim-easymotion-zh](https://github.com/zzhirong/vim-easymotion-zh) 修改，讓 EasyMotion 支援嘸蝦米輸入法識別中文。

Patch EasyMotion to support Chinese text navigation using Boshiamy (嘸蝦米) input method.

## 演示

使用嘸蝦米編碼快速跳轉到中文字：

- **單字元跳轉**：輸入嘸蝦米編碼的第一個字母，匹配所有以該字母開頭的中文字
- **雙字元跳轉**：輸入嘸蝦米編碼前2個字母，精確匹配對應的中文字

## 動機

- EasyMotion 是一個很棒的 Vim 插件，但原生只能識別英文字母
- 我平時使用嘸蝦米輸入法，希望能用相同的編碼方式在 Vim 中快速定位中文字
- 基於 vim-easymotion-zh 的小鹤双拼實現，改為支援嘸蝦米輸入法

## 先決條件 (Requirements)

- 需要安裝 [EasyMotion](https://github.com/easymotion/vim-easymotion)
- 必須設置 `let g:EasyMotion_use_migemo = 1`
- 需要熟悉嘸蝦米輸入法的編碼方式

## 安裝 (Installation)

### 使用 vim-plug

在你的 `~/.vimrc` 或 `~/.config/nvim/init.vim` 中添加：

```vim
Plug 'easymotion/vim-easymotion'
Plug 'vi000246/vim-easymotion-boshiamy'
```

然後執行：

```vim
:PlugInstall
```

### 使用其他插件管理器

#### Vundle

```vim
Plugin 'easymotion/vim-easymotion'
Plugin 'vi000246/vim-easymotion-boshiamy'
```

#### Packer (Neovim)

```lua
use {
  'easymotion/vim-easymotion',
  requires = {'vi000246/vim-easymotion-boshiamy'}
}
```

## 配置範例

```vim
" 基本配置
Plug 'vi000246/vim-easymotion-boshiamy'
Plug 'easymotion/vim-easymotion'

" 必須啟用 migemo
let g:EasyMotion_use_migemo = 1

"搜尋一個char
map  ,m <Plug>(easymotion-bd-f)
"搜尋兩個char
map ,s <Plug>(easymotion-s2)
```

## 使用方法

### 單字元跳轉 (適用於 `<Plug>(easymotion-f)` 等)

輸入嘸蝦米編碼的**第一個字母**，會匹配所有以該字母開頭的中文字。

**範例**：跳轉到「金」字
- 「金」的嘸蝦米編碼是 `ae`
- 使用 `<Plug>(easymotion-f)` + `a`
- 會匹配所有編碼以 `a` 開頭的中文字，包括「金」

### 雙字元跳轉 (適用於 `<Plug>(easymotion-s2)` 等)

輸入嘸蝦米的**前兩個編碼**，會精確匹配對應的中文字。

**範例**：跳轉到「金」字
- 「金」的嘸蝦米編碼是 `ae`
- 使用 `<Plug>(easymotion-s2)` + `ae`
- 會匹配編碼以 `ae` 開頭的所有中文字
- 相比單字元跳轉，重碼更少，候選位置更精確

### 為什麼使用嘸蝦米？

- 嘸蝦米是一種形碼輸入法，編碼規則基於字形，學習曲線較陡但輸入效率高
- 如果你已經熟悉嘸蝦米，可以用相同的編碼邏輯在 Vim 中快速定位


## 可能存在的問題

- 需要熟悉嘸蝦米輸入法
- 生僻字可能無法定位（取決於 liu7.cin 詞庫）
- 使用的是 EasyMotion 不穩定的接口，後續 EasyMotion 升級可能會導致本插件無法使用

## 技術細節

### 字典來源
- 基於 liu7.cin（嘸蝦米7.0）
- 包含 19,680 個中文字和 22,778 個編碼

### 實現方式
- 單字元模式：在 `autoload/EasyMotion/migemo/utf8.vim` 中實現
- 雙字元模式：在 `autoload/EasyMotion/cmigemo.vim` 中實現



## 支援平台

- Vim 8.0+
- Neovim 0.5+
- MacVim
- GVim

