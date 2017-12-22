ラズパイ基本セットアップ
------------

1. OSイメージのダウンロードとSDカードへの書き込み  
本家Raspberry Piサイトの[インストールガイド](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)を参照しながら進めます。

2. ヘッドレスセットアップのための準備  
OSイメージが書き込まれたSDカードを、パソコンのSDカードリーダーで開き、ルートディレクトリに中身が空の`ssh`ファイルと、下記の内容の`wpa_supplicant.conf`ファイルを置きます。
```
country=GB
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
        ssid="<SSID名>"
        psk="<パスワード>"
        key_mgmt=WPA-PSK
        proto=RSN
        pairwise=CCMP
        auth_alg=OPEN
}
```

3. Raspberry Piの起動  
パソコンからSDカードを取り出し、RPi本体に入れて起動する。

4. IPアドレスの確認  
同じネットワークセグメントにつながっているパソコンから下記コマンドでRasperry PiのIPアドレスを探す。
下記はWindows上のコマンドプロンプトを使う場合。
Raspberry PiのMACアドレス`B8-27-EB`から始まるので、それらに紐づいているIPアドレスを探す。
>for /l %i in (0,1,255) do ping -w 1 -n 1 192.168.X.%i && arp -a 192.168.X.%i
>arp -a

5. ssh経由でRaspberry Piにリモートログイン
クライアントプログラムは[Tera Term(Windows)](https://forest.watch.impress.co.jp/library/software/utf8teraterm/)や、Chromeブラウザーの[Secure Shell](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?hl=ja)などがお勧め。
sshクライアントから上記で調べたIPアドレスにログインする。


6. OSのモジュールを最新にアップデートする
```
sudo apt-get update
sudo apt-get upgrade
```

7. カメラモジュールを使えるようにする
'''
sudo raspi-config
'''

ラズパイ基本セットアップ
------------


6. カメラからの画像配信
リンク先の[ブログ記事(Raspberry Pi 3 の標準カメラで撮影した動画をブラウザに配信する方法まとめ-配信方法1 - mjpg-streamer)](https://qiita.com/okaxaki/items/72226a0b0f5fab0ec9e9)を参照しながら設定を行う。