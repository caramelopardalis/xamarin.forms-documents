Android
---

### ガイドライン

### SDK

iOS
---

### ガイドライン

### SDK

Xamarin
---

### Xamarin.Android

### Xamarin.iOS

Xamarin ではすべてのプラットフォームにおいて、Mono C# (または F#) コンパイラーが C# または F# コードを Microsoft Intermediate Language (MSIL: 中間言語) にコンパイルします。
さらに、ターゲットデバイス上の .NET Common Language Runtime (CLR) が Just in Time (JIT: 実行時) コンパイラーを使い、MSIL をネイティブコードにコンパイルして実行します。

ただし、iOS の場合はセキュリティー上の制約があるため、デバイス上で動的生成されたコードを実行することが出来ません (シミュレーターの場合は JIT コンパイラーによって実行されます)。
この制約を守った上で動作させるため、Xamarin.iOS では MSIL を Ahead of Time (AOT: 事前) コンパイラーによってコンパイルします。
これにより、必要に応じ LLVM で最適化されたネイティブの iOS バイナリーが生成されます。

AOT により、いくつかの制限があります。詳細は [Limitations - Xamarin](https://developer.xamarin.com/guides/ios/advanced_topics/limitations/) を参照してください。
また、JIT に比べて起動時間の短縮など様々なパフォーマンスの最適化によるメリットもあります。

Windows 上で開発を行っている場合、ビルドを行ったときは C# から MSIL へのコンパイルのみ Windows 上で行われます。
MSIL から iOS バイナリーへの AOT コンパイル、バンドルへのパッケージング、署名などがリモートの Mac 上で行われます。
そのため、ビルドパフォーマンスに影響する箇所は、Windows 上でのコンパイル、Mac 上でのコンパイルから署名、そしてそれらをつなぐネットワークのいずれかになります。

**参考**

* [iOS Architecture - Xamarin](https://developer.xamarin.com/guides/ios/under_the_hood/architecture/)
* [iOS Build Mechanics - Xamarin](https://developer.xamarin.com/guides/ios/advanced_topics/ios-build-mechanics/)

Visual Studio 2017
---

### ソリューションとプロジェクト

Xamarin.Android のデバッグビルドとデプロイ
---

Android エミュレーター
---

Visual Studio for Mac
---

Xcode
---

Xamarin.iOS のデバッグビルドとデプロイ
---

iOS シミュレーター
---

NuGet
---

Xamarin.Forms
---

### エントリーポイント

### クロスプラットフォームの仕組み

### プロファイル

XAML
---

XAML (ザムル) は Xamarin.Forms アプリケーションのユーザーインターフェースを定義することが出来るマークアップ言語です。コードでユーザーインターフェースを定義することも出来ますが、XML ベースの言語である XAML で定義したほうがぱっと見わかりやすいです。また、 **MVVM** (Model-View-ViewModel) アプリケーションを作成するために、データバインディングによって ViewModel と連携させた View を定義できます。

XAML には GUI デザイナーがまだ存在しないので手書きする必要があります。ただし、Visual Studio による補間機能などの支援があるので単純なエディターでプレーンテキストを編集するより少しは楽です。

Live Inspector
---

デバッグプレビュー
---

コミュニティ
---

書籍
---

デバッグ
---
