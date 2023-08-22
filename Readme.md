# Raspberry Pi 4 への pyenv の導入方法

Created on August 21, 2023  
Updated on August 22, 2023    
Copyright (c) 2023 led-mirage

## はじめに

この資料では Raspberry Pi 4 に Python のバージョン管理ツール pyenv を導入する手順について説明します。

公式には[GitHub](https://github.com/pyenv/pyenv#automatic-installer)に導入手順が載っていますので、最新・正確な手順を確認したい場合はそちらを参照してください。Debianの手順でやればOKです。

検証に使用した環境は以下の通りです。

- Raspberry Pi 4 Model B 4GB
- Raspberry Pi OS 64bit Bullseye
- pyenv 2.3.24

## １．依存するモジュールのインストール

まず最初に pyenv が依存するモジュールをインストールします。  
次のコマンドを実行してください。  
[ここ](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)を見ると何をインストールすればいいかわかります。

```bash
sudo apt update
sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

## ２．pyenvを自動インストール

次のコマンドで pyenv をインストールします。

```bash
curl https://pyenv.run | bash
```

## ３．パスの設定

以下のコマンドで、`~/.bashrc` に行を追加します。

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```

以下のファイル（`~/.profile`、`~/.bash_profile`、`~/.bash_login`）がある場合は、それらにも同じように追加します。導入直後のラズパイの場合、`~/.profile` のみ存在しました。

`~/.profile` に追加する例

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile
```

## ４．シェルの再起動

シェルを再起動してパスの変更を有効化します。

```bash
exec "$SHELL"
```

## ５．pyenv のバージョンの確認

以上で pyenv はインストールされたはずなので、次のコマンドでバージョンを確認してみましょう。

```bash
pyenv --version
```

## ６．Python のインストール

次のコマンドで指定したバージョンの Python をインストールできます。

```bash
pyenv install 3.11.4
```

インストールが可能な Python のバージョンは次のコマンドで調べることができます。

```bash
pyenv install -list
```

## ７．使用する Python のバージョンの選択

次のコマンドで使用する Python のバージョンを選択できます。

```bash
pyenv global 3.11.4
```

## ８．その他のコマンド

### 指定したバージョンの Python のアンインストール

```bash
pyenv uninstall 3.11.4
```
### pyenv の更新

```bash
pyenv update
```
