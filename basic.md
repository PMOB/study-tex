# coding: utf-8
TeXの基本・簡単な扱い方
===========
TeXの基本的なやつまとめ

- [TeXとは](#about)
- [インストール](#install)
- [書く](#writing)
- [コンパイル](#compile)
- [エディタ](#editor)

<a name="about">
TeXとは
-----------
TeXは1978年に開発された組版システム（typesetting system）です。
より具体的には、マークアップによって記述された文章から版を組むソフトウェア群です。
マークアップで文章を作成できるため、機械的に処理したり文章を汎用化したりするのが楽であり、
何よりクロスプラットフォームのOSSということで進化を続けています。
モノがモノですから情報系を始めとする理数系に好まれており、
論文や技術文書を書くための進化は特に著しいものとなっています。

LaTeXとは
-----------
LaTeXって何なんですか。正直分かりません。
訳分かりませんが、現在「テック」と言った場合はこのLaTeXのことを指すことが多いです。
というかTeXそのものについて話をすることはあまりないでしょう。
viとvimのような関係だと思います。
LateX2eというのはLaTeXの最新版(2016年1月現在)のことだそうです。
次バージョンは3が予定されているとか。

詳しくは[ここ](https://oku.edu.mie-u.ac.jp/~okumura/texwiki/?LaTeX "LaTeX - TeX Wik")をチェキだ！
とても分かりやすく書いてあります。


### 豆知識：発音に関して
TeXを素直に読むとテックス(/tecks/)ですが、
TeXの開発者Donald E. Knuthの著書「The TeXbook」によると
"TEX"の文字はアルファベットではなく
ギリシャ文字のタウ・イプシロン・カイの大文字から取っているらしいです。
ということで発音も一味あるという設定らしいですが、
そんなこと言われても日本でカタカナに興すときに困ります。
特にカイの部分の発音に一悶着ございまして、ざっと発音の一覧を書くと以下のようになります。

|       | 日本語                       | 英語               |
|-------|------------------------------|--------------------|
| TeX   | テック、テックス、テフ       | teck, tecks        |
| LaTeX | ラテック、レイテック、ラテフ | la-teck, lei-tecks |

ところで、上記の「The TeXbook」の練習問題1.1である

> After you have mastered the material in this book, what will you be: A TeXpert, or a TeXnician?

の解答は

> A TeXnician (underpaid); sometimes also called a TeXacker.

となっています。問題は後者で、"TeXacker"は「テック・ハッカー」ですね。
これが"TE-F\*cker"とか"TECK-S\*cker"とかなっちゃうとちょっと意味通らない以前にアレになりますね。
ということで「テック」と呼ぶのが無難だと思うぞ！


<a name="install">
インストール
-----------

<a name="writing">
書く
-----------
### 他マークアップ言語からの変換
- [org-mode](http://orgmode.org/ja/)
- Markdown

<a name="compile">
コンパイル
-----------

<a name="editor">
エディタ
-----------
リアルタイムプレビューとかできるGUIエディタがあるぞ！知らんけど
