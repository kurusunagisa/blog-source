---
title: "Macでcodeコマンドが使えない時のソリューション"
slug: EACCES
date: 2022-02-24T18:42:25+09:00
categories: ["Mac"]
with_date: true
tags: ["Mac","Visual Studio Code"]
---

## 実行環境
- MacBook Air (M1, 2020) 16GB
- macOS 12.2.1

## 発生した問題
最近、コーディングをしていたら突然codeコマンドが使えなくなりました。具体的には以下の状態になってしまったのです。
```shell
🔋100% ❯ code
zsh: command not found: code
```

zshがコマンドを認識していない、ということはzshのプロファイルがおかしいのかと思い.zshrcを覗いたのですが問題はなさそうで、、、

というわけで再度インストールを試すとVisual Studio Codeが以下のエラーを吐きます。
```shell
EACCES: permission denied, unlink '/usr/local/bin/code'
```

## 解決策
一度codeコマンドをアンインストールをします。command+Shift+Pで「Shell Command」と入力して「シェルコマンド：PATH内に'code'コマンドをアンインストール」を選択、「管理者特権でシェル コマンドをインストールできるように、Code が 'osascript' のプロンプトを出します。」をOKし、認証を行います。そして、再度インストールします。


## なぎさの一言
{{<chat face="wink" text="codeコマンドが使えない時にはcodeコマンドをアンインストールしてから再度インストールします！">}}