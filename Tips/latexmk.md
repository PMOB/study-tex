latexmk
=====
latexmkはPerlで書かれたLaTeXビルドスクリプトです。
入ってなかったらtlmgr

```sh
sudo tlmgr install latexmk
```

走らす
-----
perlで走ってるのでperlないと動かないけどまあ入ってるでしょう。

```sh
latexmk
```

とりあえずこれで動きます。
カレントディレクトリに複数のtexファイルがある場合はファイル名を明示してください。

```sh
latexmk hogehoge.tex
```

オプションはなんかいっぱいありますが代表的なものを

| オプション | 意味 |
|------------|------|
| `-c` | clear. 中間ファイルの削除 |
| `-C` | clear. めっちゃ消す。pdfとかも消す |
| `-f` | force. エラーで止まらなくなる猪突猛進 |
| `-pv` | preview. ビルド後に設定したpreviewerで開く |
| `-pvc` | preview continually.<br>pvモードで継続ビルド |

よく継続ビルドで出力捨てながらバックグラウンドに回してエディタで編集してます。
texファイルを更新すると組版も更新されるので便利。
```sh
latexmk -pvc hogehoge.tex &> /dev/null &
```
ログは`hogehoge.log`に残るので問題なし。
終わったらkillを忘れずに。

あと、latexmkは`.latexmkrc`を参照します。
参照順は

0. `/opt/local/share/latexmk/LatexMk`
0. `/usr/local/share/latexmk/LatexMk`
0. `/usr/local/lib/latexmk/LatexMk`
0. `/opt/local/share/latexmk/latexmkrc`
0. `/usr/local/share/latexmk/latexmkrc`
0. `/usr/local/lib/latexmk/latexmkrc`
0. `~/.latexmkrc`
0. カレントディレクトリの`latexmkrc or .latexmkrc`
0. `latexmk -r`で指定されたファイル

です。参照の度に上書きする。スコープの広いものには基本的な設定をする。
カレントディレクトリにはプロジェクトの設定をする。
`-r`オプションを使うような（普段使わない）ものは本ビルド用のビルドオプションを書く感じ。
まあ`~/.latexmkrc`とカレントディレクトリくらいしか使いません。


latexmk.rcでできること
-----
ひとつづつ叶えましょう。

```perl
#!/usr/bin/env perl

$latex = 'platex -halt-on-error';
$bibtex = 'pbibtex';
$dvipdf = 'dvipdfmx %S';
$max_repeat = 3;
$pdf_mode = 3;
```

私の`~/.latexmkrc`です。まあこんな感じに設定できるのよという例。
`latexmk`がPerl製なので一応Perlのスクリプトです。
設定項目は使いそうなものだけ適当に以下

| 変数 | 意味 |
|------|------|
| `$aux_dir` | 補助ファイル(aux, logなど)の出力および参照ディレクトリ |
| `$bibtex` | 使うbibtexプログラムの指定 |
| `$clean_ext` | `-c/-C`オプションで消す拡張子の種類を追加 |
| `$clean_full_ext` | `-C`オプションで消す拡張子の種類を追加 |
| `$dvi_previewer` | dviプレビュワープログラムの設定 |
| `$dvipdf` | dviからpdfを生成するプログラムの設定 |
| `$latex` | latexコンパイラの設定 |
| `$makeindex` | makeindexプログラムの設定 |
| `$max_repeat` | ソースの変更なしに繰り返せるコンパイル回数。既定値5 |
| `$new_viewer_always` | `-pvc`オプションで走ってる時毎回プレビュワーを起動するかの設定<br>既定値0。0ならプレビュワーが走ってない時だけ開き直す。non-zeroで毎回強制的に開く |
| `$out_dir` | 出力ディレクトリ |
| `$pdf_mode` | 既定値0。0なら`$pdflatex`でpdfを生成、<br>1なら`$pdflatex`でpdfを生成、<br>2なら`$ps2pdf`でpsからpdfを生成、<br>3なら`$dvipdf`でdviからpdfを生成する |
| `$pdflatex` | texソースからpdfを生成するプログラムの設定 |
| `$pdf_previewer` | pdfのプレビュープログラムの設定|

`%S`とかはプレースホルダです。以下のような感じ。

| プレースホルダ | 意味 |
|----------------|------|
| `%B` | 生成ベース名。`hoge.dvi`から`hoge.pdf`を生成するなら`hoge` |
| `%D` | 生成名。`hoge.dvi`から`hoge.pdf`を生成するなら`hoge.pdf` |
| `%O` | オプション |
| `%R` | `latexmk`対象ファイルのベース名。`latexmk hoge.tex`なら`hoge` |
| `%S` | ソース名。`hoge.dvi`から`hoge.pdf`を生成するなら`hoge.dvi` |
| `%T` | TeXソース名。`latexmk hoge.tex`なら`hoge.tex` |
| `%Y` | 補助ディレクトリ。ようは`$aux_dir` |
| `%Z` | 出力ディレクトリ。ようは`$out_dir` |

プレースホルダを指定しないとなんかいい感じにやってくれます。
大抵指定しなくていい。


だいたい書いた気がしますがもっと詳しく知りたい変態はCTAN行ってね。
あるいは`which latexmk`からlatexmkのシンボリックリンクがわかると思うのでソース見るもよし。

https://www.ctan.org/pkg/latexmk/?lang=en
