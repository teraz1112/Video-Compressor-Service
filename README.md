# Video-Compressor-Service

## 概要
動画圧縮サービス

## デモ
![output](https://github.com/Aki158/Video-Compressor-Service/assets/119317071/9386459e-1894-46ae-ac95-9c207caafe36)

## 説明
動画圧縮サービスです。

基本的な機能として、下記のような機能を提供しています。

- 動画ファイルを圧縮する(圧縮度をlow,medium,highの3段階から選択できます)
- 動画の解像度を変更する
- 動画の縦横比を変更する
- 動画をオーディオに変換する
- 指定した時間範囲からGIFを作成する


## インストール

1. リポジトリをクローンする
```
git clone https://github.com/teraz1112/Video-Compressor-Service.git
```

2. クローンしたリポジトリへ移動する
```
cd Video-Compressor-Service
```

## 開発環境の構築
### FFmpeg
FFmpegは、ビデオおよびオーディオの変換、エンコード、ストリーミングなどの機能を提供しているライブラリです。

[Download FFmpeg](https://ffmpeg.org/download.html)からダウンロードすることもできます。

下記手順でインストールしてください。

1. FFmpegがインストールされているか確認する
```
ffmpeg -version
```

2. システムを更新する
```
sudo apt-get update
```

3. FFmpegをインストールする
```
sudo apt install ffmpeg
```

4. FFmpegがインストールされたことを確認する。
```
ffmpeg -version
```

### エンコーダー
Ubuntuを利用している場合は、MP4ファイルが再生できないことがあります。

その場合は、下記記事を参考にしてエンコーダーをインストールしてください。

[Ubuntu 22.04でMP4ファイルが再生できない場合の対処法](https://blog.janjan.net/2022/08/15/ubuntu-play-mp4-movie-file/)


## 使用方法
1. inputとoutputフォルダに入っている不要なファイルを削除する
2. インプット用の動画を用意してinputフォルダに格納する
3. 1つ目のターミナル(**サーバ用ターミナル**とする)を起動する
4. サーバ用ターミナルに下記コマンドを入力する
```
python3 server.py
```
5. 2つ目のターミナル(**クライアント用ターミナル**とする)を起動する
6. クライアント用ターミナルに下記コマンドを入力する
```
python3 client.py
```
7. `Type in a file to upload: `と表示されたら、Inputのパスを入力する<br>**推奨 : inputフォルダのファイルパス**
8. 下記指示が表示されたら、利用したい機能を0から4の中から選択して入力する<br>`Please enter a number from 0 to 4`<br>`0 : 動画ファイルを圧縮する`<br>`1 : 動画の解像度を変更する`<br>`2 : 動画の縦横比を変更する`<br>`3 : 動画をオーディオに変換する`<br>`4 : 時間範囲からGIFを作成する`
9. その後、追加で指示が表示されたら、指示に従い入力する
10. サーバ用ターミナルが動き出したら、クライアント用ターミナルに`File generated.`と表示されるまで待つ
11. `Do you want to continue ?`と表示されたら、サービスを続けるか選択する(0 : 終了する/1 : 続ける)
12. outputフォルダにダウンロードされた動画を確認する

## 使用技術
<table>
<tr>
  <th>カテゴリ</th>
  <th>技術スタック</th>
</tr>
<tr>
  <td>開発言語</td>
  <td>Python</td>
</tr>
<tr>
  <td rowspan=3>インフラ</td>
  <td>Ubuntu</td>
</tr>
<tr>
  <td>Docker</td>
</tr>
<tr>
  <td>VirtualBox</td>
</tr>
<tr>
  <td rowspan=3>その他</td>
  <td>Git</td>
</tr>
<tr>
  <td>Github</td>
</tr>
<tr>
  <td>FFmpeg</td>
</tr>
</table>

## 機能一覧
![image](https://github.com/Aki158/Video-Compressor-Service/assets/119317071/ca894d69-d9ca-46b7-af07-d10cbfa51e65)

| 機能 | 内容 |
| ------- | ------- |
| メッセージの表示 | サービスの進行に必要なメッセージを表示します。 |
| サーバへのファイルアップロード | ユーザーが入力したパスを読み取ります。<br>ファイルが問題なければ、サーバへファイルをアップロードします。<br>下記のような場合には、ファイルのアップロードが出来ずメッセージを表示します。<br>・ファイルサイズが4GBを超える場合:`File must be below 4GB.`<br>・ファイルの拡張子がmp4でない場合:`File extension must be mp4.` |
| サービスに必要な入力の要求 | サービスを利用する際は、いくつかの指示が表示されます。<br>利用するサービスによって指示は異なります。<br>サービスに必要な入力が完了すると、そのデータをサーバへ送信します。 |
| サービスの実行 | サーバは、クライアントからサービスに必要なデータを受信すると、サービスを実行します。<br>サービスは、FFmpegライブラリと実行に必要なデータを利用して実現させています。<br>サービスの実行が完了するとoutputフォルダに動画がダウンロードされます。<br>その後、サーバは、サービスの完了メッセージをクライアントへ送信します。 |
| サービスを続けるかの確認 | サービスを続けるか確認します。<br>続ける場合は、アップロードされたファイルをそのまま使用し、サービスに必要な入力の要求を行います。 |
| サーバへアップロードしたファイルの削除 | サービスを続けるかの確認で終了するを選択した場合、クライアントは、終了通知をサーバへ送信します。<br>サーバは、終了通知を受け取るとアップロードファイルされていたファイルを削除します。 |

## 📑参考文献
### 公式ドキュメント
- [Python](https://docs.python.org/ja/3/)


### 参考にしたサイト
- [Python_Download](https://www.python.org/downloads/)
- [Download FFmpeg](https://ffmpeg.org/download.html)
- [Ubuntu 22.04でMP4ファイルが再生できない場合の対処法](https://blog.janjan.net/2022/08/15/ubuntu-play-mp4-movie-file/)
- [HTML の基本](https://developer.mozilla.org/ja/docs/Learn/Getting_started_with_the_web/HTML_basics)
