# アドオンの共有

- [AnkiWeb による共有](sharing.md#ankiweb-%E3%81%AB%E3%82%88%E3%82%8B%E5%85%B1%E6%9C%89)
- [AnkiWeb 以外での共有](sharing.md#ankiweb-%E4%BB%A5%E5%A4%96%E3%81%A7%E3%81%AE%E5%85%B1%E6%9C%89)

## AnkiWeb による共有

アドオンを配布するためにパッケージ化するには、zip 圧縮して .ankiaddon で終わる名前をつけます。

トップレベルフォルダは zip ファイルに含めないでください。例えば、次のようなモジュールがあるとします:

```
addons21/myaddon/__init__.py
addons21/myaddon/my.data
```

ZIPファイルの中身は以下の通りです:

```
__init__.py
my.data
```

以下のように zip にフォルダ名を含めると、AnkiWeb は zip ファイルを受け付けません。:

```python
myaddon/__init__.py
myaddon/my.data
```

Unix ベースのマシンでは、次のコマンドで正しい形式のファイルを作成することができます。:

```
$ cd myaddon && zip -r ../myaddon.ankiaddon *
```

Python はアドオン実行時に自動的に `pycache` フォルダを作成します。AnkiWeb は `pycache` フォルダを含む zip ファイルを受け付けないため、zip ファイルを作成する前にこれらを削除しておいてください。

.ankiaddon ファイルを作成したら、<https://ankiweb.net/shared/addons/> にある Upload ボタンを使ってアドオンを他の人と共有することができます。

## AnkiWeb 以外での共有

.ankiaddon ファイルを AnkiWeb 以外で配布する場合、アドオンフォルダに manifest.json ファイルが含まれている必要があります。このファイルには、少なくとも2つのキーを含める必要があります。package はアドオンが格納されるフォルダ名を指定し、nameはユーザーに表示される名前を指定します。オプションで、アドオンと競合する他のパッケージのリストである conflicts キーと、アドオンがいつ更新されたかを指定する mod キーを含めることができます。

Anki が AnkiWeb からアドオンをダウンロードする場合、マニフェストから conflicts キーのみが使用されます。
