---
layout: post
title: 常時 SSL 化
img: pakutaso/PAK86_smonitatocode20140517_TP_V.jpg
---

Google が常時 SSL 化を推奨し、検索結果の表示順にもそれを反映するようになりました。Output を出すのが目的なので検索結果はよいとして、やはり常時 SSL 化を行いたいものです。

[GitHub Pages](https://pages.github.com/) では `*.github.io` ドメインでは標準で SSL 化できるものの、カスタムドメインでは独自に証明書を準備する必要があります。SSL 証明書は個人レベルではコストが高いので、{AWS Certificate Manager](https://aws.amazon.com/jp/certificate-manager/) で無料の証明書を使用しようかと思います。

### 常時 SSL 化の大まかな流れ

+ [Amazon Web Services](https://aws.amazon.com/jp/) (AWS) を契約する
+ Route 53 に Hosted Zone を作成する
+ DNS のレコードを Route 53 に移行する
+ レジストラのネームサーバの設定を AWS に変更する
+ Certificate Manager で SSL 証明書を発行する
+ CloudFront で上記証明書を使用し、Origin を `*.github.io` とした設定を追加する
+ Route 53 でカスタムドメインの alias を CloudFront に設定する
