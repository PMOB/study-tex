vimmerなあなたに
========

### :makeで一発PDF生成
- `~/vim/ftplugtin/tex.vim`でmakeprgにptex2pdfを設定すると楽。

```tex
setlocal makeprg=ptex2pdf\ -l\ %
```

uptexackerなあなたは-uオプションも忘れずに。
latexmk使うなら別にいらないぞい。

#### :make打つのすらめんどい
```tex
nnoremap <Down> :make<CR><CR><CR>
```
