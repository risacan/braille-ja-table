Japanese Braille Table
======================

日本語点字（凸面、凹面）のための静的な変換表です。著作権等は主張しません。

これはフリーソフトウェア・オープンソースソフト等で広く用いられるのを意図して
作られた、静的なテキストの対応表です。すべてのファイルはUTF-8でエンコード
されています。

単純な一覧表のため、著作権は発生しない可能性も大きいと考えていますが、もし
発生した場合には、それが確かに無効とされるためにCC0ライセンスを適用します。
同梱のファイル、LICENSEをご覧ください。

## 現状の制限

現在、日本語かな一文字にしか対応していません。これは単に、作業途中のためです。

## ファイルの構成

以下の8つのファイルから構成されています。全ては実質的に同じ物で、いづれも
2つのファイルbraille-ja-table-source.tsv、braille-ja-table-reversed-source.tsvから生成されています。詳しくは
Rakefileをご覧ください。

* braille-ja-table-raw.tsv
    * TSVファイルです。生のUTF-8で記述された「日本語ひらがな」と「点字（凸面）」が
	一行に入っています。
* braille-ja-table-escaped.tsv
    * TSVファイルです。ASCIIによるUnicodeエスケープで記述された
	「日本語ひらがな」と「点字（凸面）」が一行に入っています。
* braille-ja-table-raw.json
    * JSONファイルです。生のUTF-8で記述された「日本語ひらがな」がキーになり、
	「点字（凸面）」がその値になっています。
* braille-ja-table-escaped.json
    * JSONファイルです。ASCIIによるUnicodeエスケープで記述された
	「日本語ひらがな」がキーになり、「点字（凸面）」がその値になっています。
* braille-ja-table-reversed-raw.tsv
    * TSVファイルです。生のUTF-8で記述された「日本語ひらがな」と「点字（凹面）」が
	一行に入っています。
* braille-ja-table-reversed-escaped.tsv
    * TSVファイルです。ASCIIによるUnicodeエスケープで記述された
	「日本語ひらがな」と「点字（凹面）」が一行に入っています。
* braille-ja-table-reversed-raw.json
    * JSONファイルです。生のUTF-8で記述された「日本語ひらがな」がキーになり、
	「点字（凹面）」がその値になっています。
* braille-ja-table-reversed-escaped.json
    * JSONファイルです。ASCIIによるUnicodeエスケープで記述された
	「日本語ひらがな」がキーになり、「点字（凹面）」がその値になっています。

## ファイルの生成法

ソースであるbraille-ja-table-source.tsv、braille-ja-table-reversed-source.tsvを編集した後、単純に `rake` を
実行します。これで8つのファイルが自動的に生成されます。成果物を一旦削除したい
場合は `rake clobber` を実行してください。
