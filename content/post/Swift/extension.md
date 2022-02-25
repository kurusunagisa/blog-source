---
title: "Swiftの記法とかをまとめる"
slug: extension
date: 2022-02-25T20:30:37+09:00
categories: ["Swift"]
with_date: true
tags: ["Swift","xcode"]
---

## extension
extensionは既存のクラスに定義を追加するために用いられます。例えば以下の例だと、UIColorにrandomというプロパティ(定数とは何が違うのか知らないけど)が新たに定義されたということになります。

```swift
import UIKit

extension UIColor {    
    static var random: UIColor {
        let r = CGFloat.random(in: 0...255) / 255.0
        let g = CGFloat.random(in: 0...255) / 255.0
        let b = CGFloat.random(in: 0...255) / 255.0
        return UIColor(red: r, green: g, blue: b, alpha: 1.0)
    }
}

```

わからないこと
- extendと何が違うのか？
- extendとの使い分けがよくわからない


## ClosedRange
ClosedRangeは上限と下限の間の間隔を自動で補完してくれる機能です。例えば、`let throughFive = 0...5`と書いたときに、`throughFive`では内部的に`0,1,2,3,4,5`と展開されるため、以下のように0から5の間の整数が`throughFive`に含まれている。

```shell
throughFive.contains(3)
// true
throughFive.contains(10)
// false
throughFive.contains(5)
// true
```

小数のときには自動的にdoubleに変換されて一番小さな桁で間隔がとられる。