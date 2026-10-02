#!/usr/bin/env perl

# 変数
# %O: 実行時オプション
# %S: 入力ファイル名
# %D: 出力ファイル名
# %B: 処理するファイル名の拡張子を除いた文字列

#################
##### LaTeX #####
#################
# -synctex=1: SyncTeX が有効になり，適切な pdf viewer を用いることで pdf の文章から該当するソースコードに飛べる．
# -interaction=nonstopmode: コンパイル中にエラーが起きても，ユーザーにどう処理するかの指示を求めずにコンパイルを続行する．
# -halt-on-error: コンパイル中にエラーが発生した場合，コンパイルを終了する．
# -file-line-error: tex ファイルの何行目でエラーが発生したかを表示．
# $max_repeat: 最大コンパイル回数（latexmk の既定値も 5）．

## pLaTeX でコンパイルするならこれを使う．このとき $pdf_mode = 3 に変更し，$dvipdf の行のコメントアウトもはずす．
# $latex = 'platex -synctex=1 -interaction=nonstopmode -halt-on-error -file-line-error %O %S';
## upLaTeX でコンパイルするならこれを使う．このとき $pdf_mode = 3 に変更し，$dvipdf の行のコメントアウトもはずす．
# $latex = 'uplatex -synctex=1 -interaction=nonstopmode -halt-on-error -file-line-error %O %S';
## LuaLaTeX でコンパイルするならこれを使う．
$lualatex = 'lualatex -synctex=1 -interaction=nonstopmode -halt-on-error -file-line-error %O %S';
$max_repeat = 5;

###########################
##### BibTeX/biblatex #####
###########################
# kanji=utf8: 文字コードを UTF-8 に指定．
# $biber: biblatex のバックエンドで Biber を動かすときの設定．
# 文字コードは biblatex から Biber に自動で渡される（既定値も UTF-8）ので指定不要．
## pLaTeX で pBibTeX を使うときはこれ．
# $bibtex = 'pbibtex %O %S';
## upLaTeX で upBibTeX を使うときはこれ．
# $bibtex = 'upbibtex kanji=utf8 %O %S';
## LuaLaTeX で BibTeX（upBibTeX）を使うときはこれ．
# $bibtex = 'upbibtex %O %S';
## biblatex を使うときはこれ．
$biber = 'biber %O %S';

#################
##### index #####
#################
# 索引を作成する場合に使用．
# $makeindex = 'upmendex %O -o %D %S';

#####################
##### dvi / pdf #####
#####################
## pLaTeX/upLaTeX の場合に使用．LuaLaTeX の場合は不要．
# $dvipdf = 'dvipdfmx %O -o %D %S';

# $pdf_mode: pdf ファイルの出力形式を指定．
## 0: pdf ファイルを作成しない（$latex により dvi ファイルを生成する場合など）．
## 1: $pdflatex により直接 pdf ファイルを作成．
## 2: $latex により dvi ファイルを生成し，dvips で ps ファイルに変換後，ps2pdf により pdf ファイルを作成．
## 3: $latex により dvi ファイルを生成し，$dvipdf により pdf ファイルを作成．
## 4: $lualatex により直接 pdf ファイルを作成．
## 5: $xelatex により xdv ファイルを生成後，xdvipdfmx により pdf ファイルを作成．
$pdf_mode = 4;
## latexmk -pv などで pdf を開くときのプレビューア．
## Windows: "start %S"，Mac: "open %S"，Linux: "xdg-open %S"
$pdf_previewer = "start %S";

######################################
##### 生成ファイルの出力先フォルダ #####
######################################
$out_dir = 'latex.out';
