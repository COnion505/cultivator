# cultivator

Cultivator: 木を育てる人。カルチベーター。

## 概要

引数に渡したテキストファイルを読み込んで、そこに書かれているディレクトリ構造を作成するコマンドラインプログラム。

例：引数に渡すテキストの中身
root  
 dev  
 work  
 app  
  log  
  exe  
  ini  
 pics  
user  
 shion  
  home  
 shared  
  home  


一行ずつ読み込む。インデント改行でベクタにパスを追加する。  
EOFで読み込み終了、追加したパスからフォルダを生成する。  
OSのファイルシステムに依存しないようにRUSTのFILE、PATH、などの標準クレートを使用する。  


スペース以外にもハイフンとかタブも使えると便利か。  
root  
-folder1  
--folder_in_folder1  
users  

## 設計

第一引数に渡されるファイル名を取得する。
ファイル名はフルパスで渡される。

ファイルが存在しなければエラー終了。

ファイルが存在すれば、開く。

変数．前回の行の深さ＝０
変数．前回の行のフォルダ名＝””
FOR l in lines
  



変数．1段落のスペースの数＝０

FORで1行ずつ読み込み。
変数．tree深さ＝０
FORで文字列を一文字ずつ先頭から取り出す。
スペースだったら変数．treeの深さにプラス1する。

スペース以外だったら文字列全体のスペースをトリムして変数．フォルダ名に格納

