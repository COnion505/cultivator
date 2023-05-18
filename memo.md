# overview

tree.yamlファイルを読み取ってディレクトリ構造を構築する。

キーがディレクトリ、リストがファイルになる。

directory:
  - file
  - file2
direcotry2:
  inner_directory:
    - file
    - file2


パースcrate "serde" を使用してyamlファイルのパースを行う。

cultコマンド実行でカレントディレクトにあるtree.yamlを読み込んでディレクトリを生成。
std::fsとstd::path::Pathとstd::env使えばいける？

```rust
//get current_directory
//fn current_dir() -> Result<PathBuf>
let path: PathBuf = env::current_dir()?;
//PathBufのメソッドpushでファイル名を追加する？
path.push("tree.yaml");
//current_dir/tree.yamlになるはず...?

//上で読み込んだパスからtree.yamlの内容を読み込む
//read_to_stringの引数はAsRef<Path>だがPathBufはAsRef<Path>のトレイトを継承しているので&は不要...?
let tree: String = fs::read_to_string(path).expect("cannot read tree.yaml");

//treeにtree.yamlの内容が入ったのでserde_yamlでパースする。
//戻り値に使用するのでstd::collections::BTreeMapが必要？
use std::collections::BTreeMap;
//tomlでserde書いておけばuseでのインポートは不要...?
fn main() -> Result<(), serde_yaml::Error> {
    //パース結果の戻り値が何になるのか分からん。型指定する必要あり？
    let values = serde_yaml::from_str(tree).unwrap();

}

```

階層の深さもディレクトリの数もファイルの数も不定だから既存の方でパースするのは無理？
自身を再起的に持つ型を定義してそれにパースさせる？
```toml
#依存を修正
serde={version = "1.0", features = ["derive"]}
serde_yaml = "0.9"
```

```rust
//パース用の型を定義する。自分とVec<String>を持たせて対応させる？
struct Tree {
    trees: Vec<Tree>,
    files: Vec<String>,
}
```
