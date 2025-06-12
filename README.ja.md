# S3 + CloudFront + Route 53 による静的Webサイト公開

## ✅ 成果物
サイトURL：https://www.takahiro-hasegawa.net

## ✅ 使用AWSサービス
- Amazon S3（静的Webサイトホスティング）
- Amazon CloudFront（CDN + HTTPS）
- Amazon Route 53（DNS）
- AWS Certificate Manager（SSL証明書）

## ✅ 構成概要
独自ドメインである `www.takahiro-hasegawa.net` を利用し、AWSの各種サービスを組み合わせて静的WebサイトをHTTPS対応で公開した。S3にホスティングされた`index.html`をCloudFront経由で配信し、Route 53でDNSルーティング、ACMでHTTPS対応。

## ✅ 構成図
```mermaid
flowchart TD
    User["ユーザー"]
    DNS["Route 53\n(DNSルーティング)"]
    CF["CloudFront\n(CDN + HTTPS)"]
    S3["S3 バケット\n(index.html)"]
    ACM["AWS Certificate Manager\n(SSL証明書)"]

    User -->|"① アクセス / DNS解決"| DNS
    DNS -->|"② CloudFront へ誘導"| CF
    CF -->|"③ index.html を取得"| S3
    CF -->|"④ HTTPS 応答"| User
    ACM -->|"SSL証明書を提供"| CF
```
## ✅ 各サービス設定詳細

### 1. Route 53 設定（Aレコード）
独自ドメイン `www.takahiro-hasegawa.net` を CloudFront にルーティングするための設定。

![Route 53 のAレコード設定](screenshots/route53-a-record.png)

### 2. CloudFront 一般設定（HTTPS・代替ドメイン）
カスタムドメイン名と ACM による SSL 証明書を設定。

![CloudFrontの一般設定画面](screenshots/cloudfront-general.png)

### 3. CloudFront オリジン（S3との接続）
オリジンに静的Webサイトをホスティングした S3 バケットを指定。

![CloudFrontのオリジン設定](screenshots/cloudfront-origin.png)

### 4. 証明書発行（ACM）
バージニア北部（us-east-1）リージョンでの SSL 証明書発行と CNAME 検証完了後の状態。

![ACMの証明書詳細](screenshots/acm-certificate.png)

### 5. S3 に配置した index.html の情報
ホスティング対象となる `index.html` のファイル情報画面。

![S3のindex.htmlの詳細](screenshots/s3-index-html.png)

### 6. 静的ホスティング設定（S3プロパティ）
S3 バケットのプロパティで静的ウェブサイトホスティングを有効化した設定。

![S3の静的ホスティング設定](screenshots/s3-static-hosting.png)

### 7. ブラウザでの表示確認（完成画面）
CloudFront経由で HTTPS による安全な配信が確認できる完成状態。

![ブラウザでの最終表示](screenshots/final-site.png)

## ✅ 学んだこと
- AWSサービス間の連携（S3/CloudFront/Route 53/ACM）
- DNSやSSL証明書の仕組み、CNAME検証、HTTPS通信
- キャッシュコントロールやCDNの役割
- トラブル発生時の自力での原因調査と解決方法

## ✅ 備考
HTML自体は非常に簡素なものであり、今回はインフラ構成と公開の実現を主目的としている。
