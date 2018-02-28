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

Android エミュレーター
---

Visual Studio for Mac
---

Xcode
---


NuGet
---

Xamarin.Forms
---

### 処理の開始点 (エントリーポイント)

### クロスプラットフォームの仕組み

### プロファイル

### XAML

XAML (ザムル) は Xamarin.Forms アプリケーションのユーザーインターフェースを定義することが出来るマークアップ言語です。コードでユーザーインターフェースを定義することも出来ますが、XML ベースの言語である XAML で定義したほうがぱっと見わかりやすいです。また、 **MVVM** (Model-View-ViewModel) アプリケーションを作成するために、データバインディングによって ViewModel と連携させた View を定義できます。

XAML には GUI デザイナーがまだ存在しないので手書きする必要があります。ただし、Visual Studio による補間機能などの支援があるので単純なエディターでプレーンテキストを編集するより少しは楽です。

### レイアウト

#### サイズ

パフォーマンス
---

### Layout Compression

#### 概要

Layout Compression を使うことで、ビジュアルツリーから指定されたレイアウトを削除し、ページレンダリングのパフォーマンスが改善されます。

Xamarin.Forms がレイアウトを決定する際の走査範囲は 2 種類あります。
1 つめは、ビジュアルツリーの頂点から下っていって走査するすべての要素です。
もうひとつは、サイズや位置が変更されて最新の情報を取得できていない要素とその先祖要素です。

Xamarin.Forms がどのようにレイアウトを決定するかの詳細は [Creating a Custom Layout - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/custom/) を参照してください。

レイアウト処理を行うとネイティブコントロールの階層が作成されます。ただし、この階層には Xamarin.Forms がコンテナーやラッパーとして作成した層が余分に含まれています。ネストが深くなればなるほど、Xamarin.Forms がページを表示する際の計算量が増えてしまいます。レイアウトを複雑にしてビューの数が多い場合も同様です。

#### Layout Compression

XAML の場合、`CompressedLayout.IsHeadless` プロパティーに `true` を指定することで Layout Compression が有効になります。

```xml
<StackLayout CompressedLayout.IsHeadless="true">
  ...
</StackLayout>
```

C# の場合、`CompressedLayout.SetIsHeadless` メソッドの最初の引数にレイアウトインスタンスを渡すことで有効にできます。

```csharp
CompressedLayout.SetIsHeadless(stackLayout, true);
```

Layout Compression はビジュアルツリーからレイアウトを削除するため、視覚的な役割がある場合やタッチ入力を受け付ける場合は適切ではありません。
そのため、 [VisualElement](https://developer.xamarin.com/api/type/Xamarin.Forms.VisualElement/) プロパティー (BackgroundColor、IsVisible、Rotation、Scale、TranslationX、TranslationY など) またはジェスチャーを入力させるレイアウトの場合は推奨しません。しかし、その場合でもビルドやランタイムエラーにはならず、ただ単に視覚効果が適用されないということに注意してください。

#### Fast Rendereres

Fast renderers は、ネイティブビューの階層を平坦化することにより Android 上の Xamarin.Forms コントロールの inflation とレンダリングコストを削減します。これによってビジュアルツリーの複雑さとメモリーの使用量を減りパフォーマンスを改善します。Fast renderers の詳細については [Fast Renderers - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/under-the-hood/fast-renderers/) を参照してください。良いケースだとビューの数が半分程度になります。

**参考**

* [Layout Compression - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/layout-compression/)

コミュニティ
---

書籍
---

デバッグ
---

### Xamarin.Android のデバッグビルドとデプロイ

### Xamarin.iOS のデバッグビルドとデプロイ

### iOS シミュレーター

### デバッグプレビュー

#### Live Inspector

#### Android Device Monitor
