# report_template_LaTeX

LaTeX で簡単なレポートを書く際のテンプレートです．ご自由にお使いください．

- LuaLaTeX + [jlreq](https://ctan.org/pkg/jlreq) クラスで日本語の文書を作成します．
- 表紙（著者は複数人に対応）・目次・柱（ページ上部の節見出し）を自動で出力します．
- 参考文献は [biblatex](https://ctan.org/pkg/biblatex) + [Biber](https://ctan.org/pkg/biber) で出力し，日本語文献と英語文献で書式を自動で切り替えます．
- 参考文献の体裁は Typst 版のテンプレート [`report_template_Typst`](https://github.com/matsukawa-group/report_template_Typst) と同じで，`bib` ファイルも共通で使えます．

使い方の詳細は [`template-manual/template-manual.pdf`](template-manual/template-manual.pdf) を参照してください．

## LaTeX について

### LaTeX の環境構築

[TeX Live](https://www.tug.org/texlive/) をインストールしてください．
インストール方法は OS によって異なるので，[TeX Wiki](https://texwiki.texjp.org/) の各 OS 向けのページを参考にしてください．

- Windows：[TeX Live のインストーラ](https://www.tug.org/texlive/acquire-netinstall.html)（`install-tl-windows.exe`）を使用
- Mac：[MacTeX](https://www.tug.org/mactex/) を使用（Homebrew を使う場合は `brew install --cask mactex`）

このテンプレートのコンパイルには次のものを使用します．
いずれも TeX Live をフルインストールしていれば含まれています．

- LuaLaTeX：文書のコンパイル
- Biber：参考文献の処理
- latexmk：LuaLaTeX と Biber を必要な回数だけ自動で実行

### LaTeX のアップデート

TeX Live のパッケージは，ターミナル上で以下のように入力すると最新版に更新できます．

```
tlmgr update --self --all
```

Windows では管理者権限，Mac では `sudo` が必要になる場合があります．
また，TeX Live 本体は毎年新しい版が公開されるので，年に 1 回程度は入れ直すとよいでしょう．

### コンパイル

`main.tex` と同じディレクトリで，ターミナル上で以下のように入力します．

```
latexmk main.tex
```

同じディレクトリにある `latexmkrc` の設定が自動で読み込まれ，LuaLaTeX と Biber が必要な回数だけ実行されます．
PDF ファイルなどの生成ファイルは `latex.out/` に出力されます．
生成ファイルをまとめて削除したいときは `latex.out/` ディレクトリごと削除してください．

### Visual Studio Code を使用する場合

エディタとして Visual Studio Code を使用すると編集が楽です．
拡張機能として [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) を入れておくと，保存時の自動コンパイルや PDF のプレビュー，PDF とソースコードの相互ジャンプ（SyncTeX）が使えます．

LaTeX Workshop の標準の設定では `latexmk` に pdfLaTeX 用のオプションが付くため，`settings.json` に以下を追加して，このテンプレートの `latexmkrc` の設定がそのまま使われるようにしてください．

```json
"latex-workshop.latex.tools": [
  {
    "name": "latexmk",
    "command": "latexmk",
    "args": ["%DOC%"]
  }
],
"latex-workshop.latex.recipes": [
  {
    "name": "latexmk (latexmkrc)",
    "tools": ["latexmk"]
  }
],
"latex-workshop.latex.outDir": "%DIR%/latex.out"
```

## リポジトリの構成

```
report_template_LaTeX/
├── .gitignore                    # Git の追跡対象から除外するファイルを指定
├── LICENSE                       # 本テンプレートのライセンス
├── README.md                     # リポジトリの概要および使用方法
├── bibliography.bib              # 参考文献の BibTeX データベース
├── latexmkrc                     # latexmk の設定（LuaLaTeX + Biber）
├── main.tex                      # レポートのメイン LaTeX ファイル
├── settings.sty                  # 文書全体の書式および各種設定
│
├── figure/                       # レポートで使用する図
│
└── template-manual/              # テンプレートの使用方法を示したマニュアル
    ├── figure/                   # マニュアルで使用する図
    ├── bibliography.bib          # マニュアル用の参考文献データベース
    ├── latexmkrc                 # マニュアル用の latexmk の設定
    ├── settings.sty              # マニュアル用設定ファイル
    ├── template-manual.tex       # マニュアルのメイン LaTeX ファイル
    └── template-manual.pdf       # コンパイル済みマニュアル
```

## このレポートテンプレートの使用方法

### レポートリポジトリの作成

各自の Git/GitHub で管理することを前提に説明します．

1. Organization ではなく個人の GitHub アカウントに空のリポジトリを作成．ここでは仮に `report_physics` というリポジトリ名にする．リポジトリ作成時に `README.md` や `.gitignore` は作成しない．
2. Private になっていることを確認したら `Create repository` を押す．
3. このテンプレートのリポジトリをローカルにクローンする．

例えば `@Yuki-MATSUKAWA` がレポートを執筆する場合：

```
# ローカルにテンプレートをクローン
git clone https://github.com/matsukawa-group/report_template_LaTeX report_physics
cd report_physics

# リモート URL を自身のものに変更
git remote set-url origin https://github.com/Yuki-MATSUKAWA/report_physics

# URL の変更が反映されているか確認
git remote -v

# 自身のリモートリポジトリにテンプレートの中身を反映
git push origin HEAD
```

これでテンプレートの中身が自身のレポートリポジトリに反映されたので自由に編集して大丈夫です．

### レポートの執筆

- タイトル・日付・著者は `main.tex` の冒頭（「基本設定」「著者の登録」）で設定します．表紙が不要な場合は `\coverfalse` にしてください．
- 本文は `main.tex` の `\begin{document}` 以降に書きます．
- 図は `figure/` に置き，`\includegraphics{figure/xxx.pdf}` のように読み込みます．
- 参考文献は `bibliography.bib` に書誌情報を追加し，本文中で `\cite{参照キー}` や `\citet{参照キー}` のように引用します．
- 書式を変更したい場合は `settings.sty` を編集してください．

### テンプレートへの修正の反映

このレポートテンプレートが更新された場合は，以下のコマンドを実行して自身のリポジトリに反映してください．

```
# このレポートテンプレートのリポジトリを登録
git remote add upstream https://github.com/matsukawa-group/report_template_LaTeX.git

# テンプレートの最新状態を取得
git fetch upstream

# 自分が main ブランチにいることを確認し，テンプレートの最新状態をマージ
git switch main && git merge upstream/main

# 自身のリモートリポジトリを更新
git push origin HEAD
```

## 参考文献

レポート執筆のほか，LaTeX の使用方法に関して参考になる文献を紹介します．
また，このリポジトリの `template-manual/` のディレクトリには LaTeX の使い方に関して簡単な説明があります．
テンプレートマニュアルを含め，説明事項の一部は以下の文献と重複する箇所があります．ご了承ください．

- 奥村晴彦，黒木裕介：［改訂第 9 版］LaTeX 美文書作成入門，技術評論社 (2023)．
- [TeX Wiki](https://texwiki.texjp.org/)
- [Learn LaTeX（日本語版）](https://www.learnlatex.org/ja/)
- [Overleaf Documentation](https://www.overleaf.com/learn)
- [`tsukahara-lab/TUS-ME_thesis_template`](https://github.com/tsukahara-lab/TUS-ME_thesis_template)
- [`matsukawa-group/report_template_Typst`](https://github.com/matsukawa-group/report_template_Typst)（Typst 版のレポートテンプレート）
- [`matsukawa-group/Meiji-mech_thesis_template_Typst`](https://github.com/matsukawa-group/Meiji-mech_thesis_template_Typst)（Typst 版の学位論文テンプレート．`bib` ファイルの書き方の詳細はこちらのマニュアルを参照）
