---
title: "初めてのFlutterアプリを開発・リリースするまでに使用したツール・パッケージ"
emoji: "🚚"
type: "tech"
topics:
  - "android"
  - "flutter"
  - "dart"
published: true
published_at: "2021-08-16 16:51"
---

# はじめに
社内勉強会でFlutterに興味を持ち、勉強がてらアプリを作っていたのですが、せっかく作ったので先日AndroidアプリとしてGoogle Playストアにリリースしました。

今回のアプリの開発や、リリース資材の準備等に使用したサイトやWebサービス、Dartパッケージを紹介していこうと思います。

各ツールについては簡単な紹介となってしまいますが、他のFlutterアプリの開発する方の参考になればと思います。

# 今回リリースしたアプリ
![](https://storage.googleapis.com/zenn-user-upload/a7e66439f059c0f3e9214629.png)
https://play.google.com/store/apps/details?id=com.miyashiiii.sudoku

表示された数字の読み方をポチポチ解答していくミニゲームです。

このゲームでトレーニングすれば1000億までの数字であれば一目で読めるようになります。実際に私は開発のために何度もプレイしたおかげで、1000億までなら「いち、じゅう、ひゃく、、、」と数えずに読めるようになりました。笑

Google/広告や解析以外のサーバー機能は使わずアプリ内で処理が完結しています。

# Dart・Flutterの学習
Dart、Flutterの学習に当たっては多くの記事にお世話になっていますが、主に参考にしたものを挙げます。
### [初めての Flutter アプリの作成（パート 1）](https://codelabs.developers.google.com/codelabs/first-flutter-app-pt1/)

まずは公式のサンプルアプリを実装しながらDart・Flutterの雰囲気を掴みました。

### [Flutter Widget of the Week!](https://www.youtube.com/playlist?list=PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)
各Widgetの理解にあたってはWidget of the Weekの知らないWidgetの動画を暇なときに眺めて、引き出しを増やすようにしています。

# 開発管理に使用しているWebサービス
## [Notion](https://www.notion.so/ja-jp)
カード機能を用いたタスク管理と、その他メモの管理を行っています。
数読(今回開発のアプリ)のページを作成し、画面上部はタスク管理のカンバンを表示、それ以下に子ページをギャラリー表示、といった配置で使用しています。

## [Figma](https://www.figma.com/)
シンプルなUIと豊富なフォント・素材を用いて簡単に画像作成ができます。
アイコン作成、ストア用のスクリーンショット等のリリース資材の作成に使用しました。

ストア用の画像作成にあたっては別記事も書いています。
[スクショをスマホ画像にはめ込んでストア掲載用画像を作成する](https://note.com/mysh_iiii/n/nb3998ab4eb8e)

# Dartパッケージ
##  基本機能系
### [shared_preferences](https://pub.dev/packages/shared_preferences)
iOSのNSUserDefaults, AndroidのSharedPreferencesをwrapする、ローカルにkey-valueデータを保管するためのライブラリ。
ハイスコアの保管、初回起動の判別(チュートリアル表示有無の判定)に使用してます。

### [provider](https://pub.dev/packages/provider)
状態管理にはProvider+ChangeNotifierを使用しました。
Providerの理解にあたっては、下記チュートリアルを参考にしました。
[Simple app state management](https://flutter.dev/docs/development/data-and-backend/state-mgmt/simple)
### [just_audio](https://pub.dev/packages/just_audio)
BGMの再生に使用しています。
同様のパッケージに[audioplayers](https://pub.dev/packages/audioplayers)があり、当初こちらを使用していましたが、ループ再生時に一瞬音が途切れる問題が解決できず、just_audioに乗り換えました。
### [url_launcher](https://pub.dev/packages/url_launcher)
指定したURLをブラウザで開く事のできるパッケージ。
後述するお問い合わせ用のGoogleフォームに使用しました。
メールやSMSの作成、電話発信画面への誘導もできるらしい。
### [package_info](https://pub.dev/packages/package_info)
[AboutDialog](https://api.flutter.dev/flutter/material/AboutDialog-class.html)に記載する、アプリ名、アプリのバージョンを動的に取得するために使用。
![](https://storage.googleapis.com/zenn-user-upload/82a68f16cfda65b7b0aea5c4.jpg =300x)

## UI系
### [page_transition](https://pub.dev/packages/page_transition)
画面遷移のアニメーションを手軽に実装できるパッケージ。
![](https://storage.googleapis.com/zenn-user-upload/8dd0a15029fa940c75f92c84.gif)

### [flutter_screenutil](https://pub.dev/packages/flutter_screenutil)
初期化時にデザインの前提となる画面サイズを設定し、各コンポーネントのサイズ指定時下記のように記述することで、画面サイズが変わっても比率を保持してくれます。

```dart
Container(
  width: 50.w,
  height:200.h
)
```

### [tutorial_coach_mark](https://pub.dev/packages/tutorial_coach_mark)
以下のようなチュートリアル画面を手軽に実装できるパッケージです。
![](https://storage.googleapis.com/zenn-user-upload/d996accf9ec351f9eef230ff.gif)

## 外部サービス系
外部サービスとしてはFireBaseのAnalyticsとCrashlytics(クラッシュレポート)、Google Admobを使用しています。
- [firebase_core](https://pub.dev/packages/firebase_core)
- [firebase_analytics](https://pub.dev/packages/firebase_analytics)
- [firebase_crashlytics](https://pub.dev/packages/firebase_crashlytics)
- [google_mobile_ads](https://pub.dev/packages/google_mobile_ads)



# その他使用しているWebサービス

## [Googleフォーム](https://www.google.com/intl/ja_jp/forms/about/)
社内アンケートやイベントのアンケート等でよく目にするGoogleフォームですが、アプリ開発をするようになって初めて自分で作成しました。
アプリ内にリンクを配置し、お問い合わせフォームとして使用しています。
