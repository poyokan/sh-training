
新規作成：2023-09-10
最終更新：2023-09-10

※開発時のメモはObisidianに残す。ここでは確定したもののみ記載予定。

---

## 背景
- 案件でシェルスクリプトを扱っており、勉強がしたい
- 「00_要求分析」「01_要件定義」「02_設計」「03_実装」「04_テスト」...など先にフォルダ構造が決められていることがあり、いちいち手動で作るのが面倒 → 自動化したい


## コマンド仕様

### 機能概要
- フォルダの階層構造を定義したTXTファイルをInputとして、指定したディレクトリにフォルダを作成する

### コマンド名
`create_dirs`

### 実行例
`./create_dirs <テキストファイルパス> <作成先ディレクトリ>`

### 引数定義

| No  | 名前         | 意味                                                            |
| --- | ------------ | --------------------------------------------------------------- |
| 1   | dirStructure | ディレクトリ構造を定義したTXTファイル。ファイルパスを指定する。 |
| 2   | outputDir    | 出力先ディレクトリ。                                              |

### 入出力定義
#### 入力

ディレクトリ構造を定義したTXTファイル`dirStructure.txt`(任意の名前)の中身の仕様について定義する。

```TXT
# コメント
- 00_要求分析
	- 00.01_顧客提供資料
	- 00.02_仕様調査・技術選定
	- 00.02_スケジュール・見積
- 01_要件定義
	- 01.01_要件定義書
		- _Archive
- 02_設計

...etc.
```
1. Markdownのリストの感じで階層構造を表現する
	- 「-」 + 「半角スペース」の後の文字が”フォルダ名”
	- その行のハイフン「-」の位置が前の行のハイフン「-」の位置よりも奥にあったら同じ階層と見なす
2. 「#」で始まる行はコメントとして無視する

#### 出力
上の例だと、以下のようなフォルダが出来る
```
./
 ├─00_要求分析
 │	├─00.01_顧客提供資料
 │	├─00.02_仕様調査・技術選定
 │	└─00.02_スケジュール・見積
 ├─01_要件定義
 │	└─01.01_要件定義書
 │		└─_Archive
 └─02_設計

...etc.
```

