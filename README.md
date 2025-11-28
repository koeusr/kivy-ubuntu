# Kivy(Python)のAndroidアプリビルド方法

## 概要

Ubuntu環境において、Kivy(Python)で作ったアプリケーションを、AndroidOS向けアプリへのビルド方法を記載しています。

## 環境

- Ubuntu: 20.04.1 LTS
- python: 3.8.10
- Kivy: 1.10.1
- python-for-android: 2024.1.21

## 用意するもの

- Kivyで作ったアプリ

## ビルド方法

1. Kivyで作ったアプリをUbuntu上に配置する。
    1. e.g. workフォルダにsample-appフォルダを作成して、その中にmain.pyを配置する。
2. アプリを配置した場所で"buildozer init"を実施する。そうすると、buildozer.spec(Androidアプリ用のスペック設定ファイル)が作成される。
4. アプリを配置した場所で"buildozer android debug"を実施する。そうすると、アプリのビルドが実行され、APKファイルが作成される。
    1. 注)APKファイル作成完了後にエラーメッセージが出力されるが、APKファイル自体の作成は成功しているので問題ない。
5. ビルドメッセージに"debug.apk"のPathが出力されているので、そのPathを利用して、Android端末にAPKファイルをインストールする。
    1. adb install -r <debug.apkのPath>

## ビルドポイント

#### buildozer.specの書き方

targetAPIとSDKを決定する必要がある。対象とするAndroid端末のOSVersionを調べて、適切な値を設定すること。
- android.api = xx
- android.sdk = xx

#### Android端末の開発者モード

Android端末に対して直接APKファイルをインストールするためには、開発者モードにする必要がある。
1. デバイスの設定からビルド番号のメニューを探して、７回連打タップする。
2. その後、設定に開発者オプションが表示される。
3. 開発者オプションから、USBデバッグのメニューを探して、有効にする。

## 参考
- [Kivy](https://kivy.org/)
- [Buildozer](https://kivy.org/doc/stable/guide/packaging-android.html#buildozer)
- [Kivy on Android](https://kivy.org/doc/stable/guide/android.html)
- [BuildozerのAndroid apk作成のspecファイルの書き方](https://airgrammar.net/kivy-buildozer-spec-file-apk/)
- [デバイスの開発者向けオプションを設定する](https://developer.android.com/studio/debug/dev-options?hl=ja)
