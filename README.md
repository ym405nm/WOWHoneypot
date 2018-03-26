# WOWHoneypot: 初心者向け! 攻撃者をおもてなしする Web ハニーポット

Welcome to Omotenashi Web Honeypot(WOWHoneypot)は、簡単に構築可能で、シンプルな機能で動作を把握しやすくした、サーバ側低対話型の入門用 Web ハニーポットです。
ルールベースのマッチ&レスポンス機能により、攻撃者に気持ちよく攻撃してもらい、得られるログの幅を広げることができます。

送信元からの HTTP リクエストをそのまま保存するので、後からじっくりゆっくりログ分析をすることが可能です。

ハニーポッター技術交流会で発表したときの資料はこちらで公開しています。  
[初心者向けハニーポット WOWHoneypot の紹介](https://speakerdeck.com/morihi_soc/chu-xin-zhe-xiang-kehanihotuto-wowhoneypot-falseshao-jie)

## 特徴
- 構築が簡単
- HTTP リクエストをまるっと保存
- デフォルト200 OK
- マッチ&レスポンス

## 必要なもの
- Python3

## 構築方法(Ubuntu 16.04 Server 64bit)
```
$ sudo ufw default DENY
$ sudo ufw allow 80/tcp
$ sudo ufw allow 8080/tcp
※ SSH のアクセスポートも環境に合わせて追加してください。
$ sudo ufw enable
$ sudo vi /etc/ufw/before.rules
※ 「*filter」より前に下記の4行を追記する。
———————————————————————————
*nat
:PREROUTING ACCEPT [0:0]
-A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
COMMIT
———————————————————————————
$ sudo ufw reload
$ cd ~/
$ git clone https://github.com/morihisa/WOWHoneypot.git wowhoneypot
$ cd wowhoneypot
$ python3 ./wowhoneypot.py
```

## 動作確認
- ブラウザでハニーポットの IP アドレスにアクセスして、何かしらの HTML ファイルが返ってきたら OK です。

## ログファイル
- log/wowhoneypot.log
- WOWHoneypot の動作ログが記録されます。
- log/access_log
- アクセスログが記録されます。

## 動作テスト済み環境
- macOS High Sierra & Python 3.6.3
- Ubuntu 16.04.3 Server 64bit & Python 3.5.2
- Windows 7 SP1 & Python 3.6.3

## リリースノート
- 2017年11月25日 WOWHoneypot Version 1.0 公開

## Licence

[BSD License](https://github.com/morihisa/WOWHoneypot/blob/master/LICENSE)

## Author

- [morihi-soc.net](http://www.morihi-soc.net/)
- [@morihi_soc](https://twitter.com/morihi_soc)

## TENICHI EDITION

デフォルトページを天下一品のラーメンの画像に切替える機能です。

たぶん requests と FlickrAPI が必要になります。

```bash:bash
$ pip install requests
$ pip install flickrapi
```

画像取得に Flickr にアクセスしますので API が必須になります。Flickr にアクセスして API KEY と SECRET を取得して、
config.txt の flickrpublic / flickrsecret に記入してください。各クォートは不要です。イコールの前にスペースを入れないでください。
外部に通信しますのでネットワーク設定をご確認ください。

初回起動のみで次回以降は取得しません。

本機能を使用しない場合は当該設定を消すか、デフォルトのままで動きます。

> 人間はハニーポットにアクセスしないから・・・

せやな
