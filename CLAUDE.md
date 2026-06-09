# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

TECS (TOPPERS Embedded Component System) の日本語リファレンスマニュアルを Sphinx で生成するドキュメントリポジトリ。対象システム: ASP3+TECS、ATK2+TECS、mruby-on-ev3rt+tecs、mruby-on-gr-peach+tecs、tinet+tecs、tlsf+tecs。

## セットアップ

```bash
# Pipenv で依存パッケージをインストール（推奨）
pipenv install
pipenv shell
```

## ビルドコマンド

すべて `docs/` ディレクトリ内で実行する。

```bash
cd docs

# HTML ビルド
make html

# ライブプレビュー（ファイル変更を監視して自動ビルド）
make livehtml

# PDF ビルド（platex が必要）
make latexpdfja
```

出力先: `docs/_build/html/`

## ドキュメント構造

```
docs/
├── conf.py              # Sphinx 設定（言語: ja_jp、テーマ: sphinx_rtd_theme）
├── index.rst            # ルート toctree
├── _extensions/
│   ├── tecs.py          # TECS CDL Sphinx ドメイン
│   └── tecslexer.py     # TECS CDL Pygments レクサー
├── _static/style.css    # カスタム CSS（no-alt-color クラス等）
├── tecs/                # TECS リファレンス（CDL仕様、コマンド、プラグイン等）
├── asp3/                # ASP3+TECS カーネル API
├── atk2+tecs/           # ATK2+TECS
├── mruby-on-ev3rt+tecs/ # mruby EV3RT バインディング
└── mruby-on-gr-peach+tecs/
```

## TECS 固有マークアップ

### シンタックスハイライト

`tecs-cdl` を言語として指定すると TECS CDL のハイライトが適用される。

```rst
.. code-block:: tecs-cdl

   celltype tTask { ... };
```

### TECS ドメインディレクティブ

`conf.py` で `primary_domain = 'tecs'`、`default_role = 'any'` に設定されているため、ドメイン省略で参照可能。

```rst
.. tecs:celltype:: nNamespace::tCellTypeName

   .. tecs:attr:: Type attributeName
   .. tecs:var:: Type variableName
   .. tecs:entry:: sSignature eEntryPortName
   .. tecs:call:: sSignature cCallPortName

.. tecs:signature:: sSignatureName

   .. tecs:sigfunction:: ReturnType functionName(int param)
```

クロスリファレンス:

```rst
:tecs:attr:`tCellTypeName::attributeName`   # フルネーム表示
:tecs:attr:`~tCellTypeName::attributeName`  # 末尾要素のみ表示
```

### 日本語インラインマークアップ

分かち書きなし言語では両側バックスラッシュでスペースをエスケープする。

```rst
使用方法として\ :ref:`タスクを通知先とする場合 <label>`\ を例として…
```

### 表の縞模様を無効化

```rst
.. rst-class:: no-alt-color

+---------+---------+
| column1 | column2 |
+=========+=========+
```
