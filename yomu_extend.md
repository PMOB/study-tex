編纂について
===========
部誌の記事をまとめかたについて記述

書いた記事をまとめるrootファイル的なものが必要となるので，
それについて書きます．
（hato-magazineでいうmain.texのこと）

usepackageについては，
必要のないモノまで含まれている可能性が高いので，
吟味が必要かも知れませんね．

```tex
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
pppp
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

