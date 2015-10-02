# Redmine Serial Number Field

Redmine plugin for automatically available to custom field to generate a sequential number.

## Features

* 自動的に連番を生成するカスタムフィールド(チケット専用)が利用可能
  * カスタムフィールドの設定画面で、設定されたフォーマットを元にプロジェクト単位で
    * チケット作成時に自動的に採番する
      * フォーマットを変更した場合は該当フォーマットで採番を新たに開始します。
    * 一括編集時に自動的に採番する
      * 既存のチケットの場合は自動採番の `CustomValue` が存在しないため、一度更新後に、再度更新すると付加される。
* チケットのフィルタ条件、検索対象など、カスタムフィールドの基本的なオプションも利用可能
  * 表示は全ユーザーに対して行われる
* 原則編集不可とし、照会画面には表示（編集画面には表示しない）

### Unimplemented

* 異なるプロジェクトへチケット移動した場合の採番
* 採番対象のトラッカーへ変更した場合の採番
* 単一チケット編集した場合の採番
* 単一チケット作成した場合にカスタムフィールドがあった箇所が空で表示される

## Usage

1. チケットの新しいカスタムフィールドを作成します。
2. 項目「書式」を自動採番に変更します。
3. 項目「正規表現」に自動採番のフォーマットを指定します。
4. フィルタや検索条件として使いたい場合はチェックを入れます。
5. 自動採番をしたいトラッカーとプロジェクトを指定します。

![usage.png](https://github.com/matsukei/redmine_serial_number_field/blob/master/doc/images/usage.png)

## Supported versions

* Redmine 2.6.0

## Format specifications

|採番対象の日付|年表記フォーマット |年度            |連番フォーマット|結果                    |
|--------------|-------------------|----------------|----------------|------------------------|
|created_on    |`yy`               |No              |000             |2015-03-01 => '15001'   |
|created_on    |`yyyy`             |No              |0000            |2015-03-01 => '20150001'|
|created_on    |`YY`               |Yes             |000             |2015-03-01 => '14001'   |
|created_on    |`YYYY`             |Yes             |0000            |2015-03-01 => '20140001'|

* OK
  * `{000000}` #=> `000001`
  * `ABC-{yy}-{00}` #=> `ABC-15-01`
* NG
  * 末尾が連番フォーマット出ない場合 e.g. `ABC-{000}-{yy}`
  * 年表記フォーマット、連番フォーマットでない場合 e.g. `{abc}-{yy}-{000}`

## Install

1. `your_redmine_path/plugins/redmine_serial_number_field/` に clone もしくはダウンロードしたソースを配置します
2. Redmineを再起動してください
