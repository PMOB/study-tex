参考: https://gist.github.com/cohalz/7d169cad51f60b525c5b#file-texmemo-md

---
# MacでTeXstudio(TeXのIDE)を使ってTeXを書くやつ

まず，MacTeXとTeXstudioをダウンロードサイトからインストールする

以下のコマンドを実行する
(brew caskで入る場所を/Applicationsにするだけなので必須ではないけどやっとくとよい)

```
echo "export HOMEBREW_CASK_OPTS="--appdir=/Applications"" >> .bash_profile
echo "export HOMEBREW_CASK_OPTS="--appdir=/Applications"" >> .zprofile
```

ターミナル再起動する  

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew tap phinze/cask  
brew install brew-cask
brew cask install xquartz
brew install poppler
```

# 環境設定編

```
echo "\nshell_escape_commands = \\\nbibtex,bibtex8,bibtexu,upbibtex,biber,\\ \nkpsewhich,\\ \nmakeindex,mendex,texindy,xindy,\\ \nmpost,upmpost,\\ \nrepstopdf,epspdf,extractbb" | sudo tee -a /usr/local/texlive/2014/texmf.cnf
```
を実行しTeXstudioを再起動

## TeXstudioの設定

TeXstudio->環境設定->コマンドから  
LaTeXの  
`/usr/texbin/latex -src -interaction=nonstopmode %.tex`
を  
`/usr/texbin/platex -src -interaction=nonstopmode -shell-escape %.tex`に変更   
DviPdfの  
`/usr/local/bin/dvipdf %.dvi`  
を  
`/usr/texbin/dvipdfmx %.dvi` に変更  

TeXstudio->環境設定->ビルドから
既存のコンパイラを`latex`に  
ビルド表示を`DVI->PDFチェーン`に  
左下高度なオプションの表示にチェックを入る  
コマンド($PATH)を`/usr/texbin`に

詳細なエディタ設定から，  
「暗黙的に、保存したファイルを再読み込みして外部での変更を適用」にチェックを入れる  
(お好きなエディタで編集するのが楽になる)


pdf生成と表示は⏩マークから

サンプル
https://drive.google.com/file/d/0B0gl_qaSWCF0aER1dXBaZjdPelk/view?usp=sharing
