# VS CodeでLualatex環境を作る
## やること
1. VS CodeとLatexのインストール
1. ターミナルでコマンドをたたいてコンパイルする
1. 拡張機能「Latex Workshop」を入れて少し作業しやすくする
## 前提
Texはマークアップ言語の一種で、Texのルールに則って記述されたテキストファイル(.tex)を○○latexといったエンジンが読み取ってpdfに変換(コンパイル)してくれます。
したがって、テキストファイルを作成するためのテキストエディターとTexエンジンをインストールする必要があります。テキストエディターはメモ帳などでもいいのですが、VS Codeには様々な便利機能があるのでこちらを使います。
## VS CodeとLatexのインストール
世界中に記事があふれているので割愛します。
## ターミナルでコマンドをたたいてコンパイルする
https://github.com/junseidesu/Lualatex_VSCode_settings/tree/main
こちらのレポジトリを開き、Code→Download ZIPからダウンロードし、展開します。
VS Codeを開きファイル→フォルダーを開く　から展開したフォルダーを開きます。
表示→ターミナルからターミナルを開き
```
lualatex main
```
を実行します。うまくlatexがインストールされていればいくつかの中間ファイルとmain.pdfが作成されるはずです。これが基本的なコンパイルの仕方です。
## 拡張機能「Latex Workshop」を入れて少し作業しやすくする
毎回コマンドを打つのは面倒なので、少し工夫します。
VS Codeの拡張機能から「Latex Workshop」をインストールします。
続いて、左下の歯車から設定→右上の「設定(JSON)を開く」→
```
{
    "latex-workshop.latex.tools": [
        {
            "name": "lualatex",
            "command": "lualatex",
            "args": [
                "-ghostscript-options=\"-dNOSAFER\"",
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "lualatex",
            "tools": [
                "lualatex"
            ]
        }
    ],
    "latex-workshop.view.pdf.viewer": "tab",
    "editor.wordWrap": "on",
    "security.workspace.trust.untrustedFiles": "open"
}
```
こちらをコピペ(もともと何か記述があれば下に付け加える)して、保存します。
上手くいっていれば、main.texを編集しCTRL+Sなどで保存するたびにぱっとコンパイルされ、更新されるはずです。
## おまけ
ローカルでの環境構築が手間ならWebサービスを使う手もあります。ここではOverleafを例にしますが、アカウントを作成し新規プロジェクト→プロジェクトのアップロードから先ほどダウンロードしたzipファイルをアップロードすると使用可能です。その際、設定→コンパイラからコンパイラをLuaLatexに変更するのを忘れないで下さい。
なにか間違っている点があれば教えてください。
また、上手くいかない点があればもしかしたら力になれるかもしれないので気軽に聞いてください。