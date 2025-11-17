# COBOLでHello World - 初心者向けマニュアル

## はじめに
このマニュアルでは、macOS環境でCOBOLのHello Worldプログラムを作成し、実行するまでの手順を説明します。VSCodeを使用して快適な開発環境を構築します。

## 必要な環境

- macOS（Catalina以降推奨）
- Homebrew（パッケージマネージャー）
- VSCode（テキストエディタ）

## 1. COBOLコンパイラのインストール

### Homebrewのインストール

もしHomebrewがインストールされていない場合は、ターミナルで以下のコマンドを実行してください：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### GnuCOBOLのインストール

ターミナルで以下のコマンドを実行します：

```bash
brew install gnu-cobol
```

### インストールの確認

以下のコマンドでバージョンを確認できます：

```bash
cobc -version
```

以下のような出力が表示されれば成功です：

```
cobc (GnuCOBOL) 3.1.2.0
Copyright (C) 2020 Free Software Foundation, Inc.
...
```

## 2. Hello Worldプログラムの作成

### ソースコードの作成

`hello.cob`という名前でファイルを作成し、以下のコードを入力します：

```cobol
       IDENTIFICATION DIVISION.
       PROGRAM-ID. HELLO_WORLD.
       PROCEDURE DIVISION.
           DISPLAY "*** HELLO_WORLD ***"
           STOP RUN.
```

### COBOLの重要な記述ルール

1. **各行の最初に7つの空白が必要です**
   - これはCOBOLの歴史的な仕様です（パンチカード時代の名残）
   - 空白を忘れるとコンパイルエラーになります

2. **ファイルの最後に空の改行が必要です**
   - EOF（End of File）を明示するためです

3. **ピリオド（`.`）の位置に注意**
   - 各DIVISIONの後とSTOP RUNの後に必要です

## 3. コマンドラインでの実行

ターミナルで以下のコマンドを実行します：

```bash
cobc -x -Wall -debug hello.cob
./hello
```

以下のように表示されれば成功です：

```
*** HELLO_WORLD ***
```

### コマンドの説明

- `cobc`: COBOLコンパイラ
- `-x`: 実行可能ファイルを生成
- `-Wall`: すべての警告を表示
- `-debug`: デバッグ情報を含める
- `hello.cob`: ソースファイル名

## 4. VSCodeで統合開発環境を構築

### VSCodeのインストール

1. [VSCode公式サイト](https://code.visualstudio.com/download)からダウンロード
2. ダウンロードしたファイルをアプリケーションフォルダに移動
3. VSCodeを起動

### 拡張機能のインストール

VSCodeで以下の拡張機能をインストールします：

#### 1. COBOL拡張機能

1. VSCodeの左サイドバーから「Extensions」（拡張機能）アイコンをクリック
2. 検索バーに「COBOL」と入力
3. 「COBOL」という名前の拡張機能を見つけて「Install」をクリック

**機能**: COBOLのシンタックスハイライト（構文の色付け）を提供します。

#### 2. Save and Run拡張機能

1. 検索バーに「Save and Run」と入力
2. 「Save and Run」をインストール

**機能**: ファイル保存時に自動的にコンパイル・実行を行います。

### Save and Runの設定

1. インストールした「Save and Run」の歯車アイコンをクリック
2. 「Extension Settings」を選択
3. 「Edit in settings.json」をクリック
4. 以下の設定を追加：

```json
"saveAndRun": {
    "commands": [
        {
            "match": ".cob",
            "cmd": "cobc -x -Wall -debug ${file}; ./${fileBasenameNoExt}",
            "useShortcut": true,
            "silent": false
        }
    ]
}
```

5. 設定を保存
6. **VSCodeを再起動**（重要：再起動しないと設定が反映されません）

### 実行方法

1. `hello.cob`をVSCodeで開く
2. `Command + Shift + R`（macOS）または`Ctrl + Shift + R`（Windows/Linux）を押す
3. 統合ターミナルが開き、自動的にコンパイル・実行されます
4. エラーがなければ、以下のように出力されます：

```
*** HELLO_WORLD ***
```

## トラブルシューティング

### よくあるエラー

#### 1. コンパイルエラー：行頭の空白がない

**エラーメッセージ例:**
```
error: syntax error, unexpected IDENTIFICATION
```

**解決方法:** 各行の先頭に7つの空白を追加してください。

#### 2. ファイルが実行できない

**エラーメッセージ例:**
```
Permission denied
```

**解決方法:** 実行権限を付与します：
```bash
chmod +x hello
```

#### 3. Save and Runが動作しない

**解決方法:**
- VSCodeを再起動してください
- settings.jsonの記述が正しいか確認してください
- ショートカットキー（Command + Shift + R）を正しく押しているか確認してください

## まとめ

このマニュアルでは、以下の内容を学びました：

1. ✅ COBOLコンパイラのインストール
2. ✅ Hello Worldプログラムの作成と実行
3. ✅ VSCodeでの開発環境構築
4. ✅ 自動コンパイル・実行の設定

これで、COBOLプログラミングを始める準備が整いました！

## 次のステップ

- COBOLの基本文法を学ぶ
- データ処理プログラムを作成する
- ファイル入出力を扱う

Happy COBOL Programming! 🎉
