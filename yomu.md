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

※基本的に前回のフォーマットと同じという形で加筆していきます

<a name="head">
記事タイトル、著者、要約
-----------

```
\chapter{タイトル} % 第XX章 タイトル みたいになる

\begin{flushright}名前\end{flushright} % 右側にちっちゃく表示される

\thispagestyle{empty} % pagestyleをemptyにすることでページ番号を消す

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
```
\begin{figure}[位置指定]
  \centering
  % clipははみ出しを切り取るoption
  \includegraphics[clip, width=ここにサイズを書く]{画像.jpg}
  \caption{これは画像です}
\end{figure}
```
- 位置指定に関しては, `h, t, b, p`のオプションがある
- サイズは`cm`だろうと`mm`だろうと何でも良いかと思う
- 画像が大きすぎてはみ出るとかは避けたいので，
サイズの上限の設定は必要?
- issue立てときます

<a name="table">
表
-----------

```
\begin{table}[位置指定]
  \begin{tabular}{c|c|c} 
    \hline
    name  & author & latest version(2016/01/20)\\
    \hline \hline
    Linux Kernel & Linus Torvalds & 4.3.3 \\
    Star Wars & George Lucas & ep7 \\
    \hline
  \end{tabular}
\end{table}
```

みたいな

- 表のフォーマットに関しては自由でいいだろうか..?
  - ex: 絶対四角で囲うとか，ここは二重線にする〜とか
- longtableってのもあるらしい
- 個人的にはtableを使うことが多いですが，
違いがよく分かってません
- issue立てときます


<a name="code">
ソースコード
-----------

- listings or verbatim
- 2015文化祭の部誌ではlistingsを使いました
- listingsは外部からstyファイルを入れた記憶...?
- issue立てときます

<a name="add_fonts">
フォントの追加
-----------

- 求む知見 

<a name="add_sty">
独自スタイルの追加
-----------

- 求む知見 

<a name="compilation_book">
編纂するにあたって
-----------

書いた記事をまとめるrootファイル的なものが必要となるので，
それについて書きます．
（hato-magazineでいうmain.texのこと）

usepackageについては，
必要のないモノまで含まれている可能性が高いので，
吟味が必要かも知れませんね．

```
%% documentclassのオプションでは
%% フォントの大きさ，日本のB5を指定．
%% openanyを使うと，章の開始位置が奇数ページのみでなくなる．
%% 本なのでjsbookを指定．
\documentclass[10pt, b5j, openany]{jsbook}

%% 各usepackageを記述

% amsmath, amssymb 
%   amsはAmerican Mathematical Societyらしい
%   つまりは数式関連のpackage
\usepackage{amsmath, amssymb}

% bm
%   太字のベクトルを表すときに使う？
\usepackage{bm}

% graphicx
%   includegraphicsを使うために必要
\usepackage[dvipdfmx]{graphicx}

% color
%   色文字を使う際に必要
\usepackage[dvipdfmx]{color}

% hyperref
%   PDFにHTMLと同じハイパーリンク機能を
%   加えるためのマクロ
%   目次からジャンプできるのはこいつのおかげ？
\usepackage[dvipdfmx]{hyperref}

% ascmac
%   文書を枠で囲う際に必要
%   itemboxやscreen等
\usepackage{ascmac}

% makeidx
%   \makeindexとかの目次関連に必要
\usepackage{makeidx}

% longtable
%   前回はtableにlongtableを使ったようです
\usepackage{longtable}

% booktabs
%   \tabularや\hlineなどを使った表が
%   いい感じにきれいになるっぽい
\usepackage{booktabs}

% etoolbox
%   なんかTeXでプログラミングするためのヤーツ？
%   ifっぽいやつとかandとかあるっぽい
\usepackage{etoolbox}

% ulem
%   アンダーラインとか打ち消しとか使うときに必要？
%   \ulineとかそれ系のやつ
\usepackage[normalem]{ulem}

% listings
%   コードを貼り付ける際に必要
%   ハイライト等も使えるので良い
\usepackage{listings}

%% ここよくわからない
\makeatletter
\patchcmd{\@makechapterhead}{\vspace*{2\Cvs}}{}{}{}
\makeatother

% textwidthをfullwidthに
\setlength{\textwidth}{\fullwidth}

% 両面印刷用の左右のマージンを統一
\setlength{\evensidemargin}{\oddsidemargin}

%% Tips: 
%  \usepackage{layout}
%  ...
%  \begin{document}
%  ...
%  \layout
%  ...
%  \end{document}
%  でレイアウト確認できるっぽいっすよ
% 
%  あと参考に: 
%  http://ideas.paunix.org/latex/latex_6_docclasspreamble.htm#preamble

% スタイルが色々あるっぽい
% 前回は指定無しでやりました
% \pagestyle{plain} 

% 目次用に宣言
% 事前にauxファイルが無いと機能しないっぽい？
% -> 2回コンパイル必要か
\makeindex 


\begin{document}

% 本文前の事をここから書く
\frontmatter 

% 外部ファイルはincludeで組み込んでいく
% これは，はじめに，の部分
\include{intro}

% 目次を挿入
\tableofcontents 

% 本文開始
\mainmatter 

% tmp.texファイルをinclude
% \include{tempdir/tmp.tex} でないことに注意
\include{tempdir/tmp} 

．．．% どんどんincludeしていく

% あとがきを入れるなら最後に入れる
\include{atogaki/sub} 

\end{document}
```




