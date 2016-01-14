読むやつを書くやつ
===========
部誌の**記事の**書き方の正規系。
改善があったり追加がある可能性大なので要チェキである。


項目一覧
-----------
- [記事タイトル、著者、要約](#head)
- [章・節・項](#parts)
- [数式](#equation)
- [画像](#image)
- [表](#table)
- [ソースコード](#code)
- [フォントの追加](#add_fonts)
- [独自スタイルの追加](#add_sty)


※documentclassにjsbookを使うヤーツを想定

<a name="head">
記事タイトル、著者、要約
-----------

```
\chapter{タイトル} % 第XX章 タイトル みたいになる

\begin{flushright}名前\end{flushright} % 右側にちっちゃく表示される

\begin{abstract}
概要 とか, はじめに とかをここに書く
\end{abstract}
```

<a name="parts">
章・節・項
-----------

- `section`と`subsection`を使う．
- `section`は 2.1 とか 3.4 とかになる．
  - 章番号.番号 みたいな感じ
  - jsarticleだと 番号 で 1コになる．
- `subsection`は 章番号.番号.番号 みたいな感じ．
  - 2.1.4 とか 3.4.4 とかになる．
  - jsarticleだと 番号.番号 で 2コになる． 
- `subsubsection`はデフォルトでは番号は付かない．
  - `subsubsection`より小さなやつ．
  - 何かのオプションをつければ，章番号.番号.番号.番号みたいにできるっぽい．


<a name="equation">
数式
-----------
```
\[
数式
\]
```
みたいな？

<a name="image">
画像
-----------



<a name="table">
表
-----------



<a name="code">
ソースコード
-----------

- listings or verbatim
- 2015文化祭の部誌ではlistingsを使いました
- listingsは外部からstyファイルを入れた記憶...?

<a name="add_fonts">
フォントの追加
-----------



<a name="add_sty">
独自スタイルの追加
-----------
