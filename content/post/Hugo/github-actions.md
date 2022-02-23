---
title: "Github Actions"
slug: github-actions
date: 2022-02-23T18:34:50+09:00
categories: ["HUGO"]
with_date: true
tags: ["HUGO","Github"]
---

Github Actionsを使いたいとき、yamlファイルにアクションを定義します。ここでは、アップロード先のリポジトリをblog-sourceにしてGithub　Actionsでビルド、blogリポジトリにビルド結果をpushすることでソースをblog-source、ブログの静的ファイルをblogに置くこととします。このとき、blog-sourceにアップロードする`blog-source/.github/workflows/gh-pages.yml`は以下のように書きます 。

```yaml

name: Deploy Hugo

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-20.04
    concurrency:
      group: ${{ github.workflow }}-${{ github.ref }}
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true 
          fetch-depth: 0   

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "0.92.2"
          extended: true

      - name: Build
        run: hugo --minify

      - name: Push to blog repo
        uses: cpina/github-action-push-to-another-repository@main
        env:
          API_TOKEN_GITHUB: ${{ secrets.HUGO_DEPLOY_TOKEN }}
        with:
          source-directory: "public"
          destination-github-username: "kurusunagisa"
          destination-repository-name: "blog"
          user-email: kurusunagisa963@gmail.com
          target-branch: main
```

ここで行なっている処理とその効果は以下の通りです。
- Github ActionsでHugoをビルドするとpublicフォルダに静的ファイル群が生成される
- 静的ファイル群をblogリポジトリのルートにpushする
- Github Pagesをルートディレクトリに設定してあれば、静的ファイル群が自動的にGithub Pagesに乗っかる