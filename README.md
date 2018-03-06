このドキュメントは参考先のめちゃ意訳などを記述してます。

<!-- TOC -->

- [Android](#android)
    - [ガイドライン](#ガイドライン)
    - [SDK](#sdk)
- [iOS](#ios)
    - [ガイドライン](#ガイドライン-1)
    - [SDK](#sdk-1)
- [Xamarin](#xamarin)
    - [Xamarin.Android](#xamarinandroid)
    - [Xamarin.iOS](#xamarinios)
- [Visual Studio 2017](#visual-studio-2017)
    - [ソリューションとプロジェクト](#ソリューションとプロジェクト)
- [Android エミュレーター](#android-エミュレーター)
- [Visual Studio for Mac](#visual-studio-for-mac)
- [Xcode](#xcode)
- [NuGet](#nuget)
- [Xamarin.Forms](#xamarinforms)
    - [処理の開始点 (エントリーポイント)](#処理の開始点-エントリーポイント)
    - [クロスプラットフォームの仕組み](#クロスプラットフォームの仕組み)
        - [プロファイル](#プロファイル)
        - [カスタムレンダラー](#カスタムレンダラー)
        - [DependencyService](#dependencyservice)
    - [XAML](#xaml)
    - [レイアウト](#レイアウト)
        - [サイズ](#サイズ)
    - [Messaging Center](#messaging-center)
        - [MessagingCenter の使い方](#messagingcenter-の使い方)
            - [シンプルなメッセージ](#シンプルなメッセージ)
        - [引数を渡す](#引数を渡す)
        - [監視の解除](#監視の解除)
    - [トリガー](#トリガー)
        - [プロパティートリガー](#プロパティートリガー)
            - [スタイルでトリガーを使う](#スタイルでトリガーを使う)
        - [データトリガー](#データトリガー)
        - [イベントトリガー](#イベントトリガー)
- [パフォーマンス](#パフォーマンス)
    - [Layout Compression](#layout-compression)
        - [概要](#概要)
        - [Layout Compression](#layout-compression-1)
        - [Fast Rendereres](#fast-rendereres)
- [コミュニティ](#コミュニティ)
- [書籍](#書籍)
- [デバッグ](#デバッグ)
    - [Xamarin.Android のデバッグビルドとデプロイ](#xamarinandroid-のデバッグビルドとデプロイ)
    - [Xamarin.iOS のデバッグビルドとデプロイ](#xamarinios-のデバッグビルドとデプロイ)
    - [iOS シミュレーター](#ios-シミュレーター)
    - [デバッグプレビュー](#デバッグプレビュー)
        - [Live Inspector](#live-inspector)
        - [Android Device Monitor](#android-device-monitor)

<!-- /TOC -->

## Android

### ガイドライン

### SDK

## iOS

### ガイドライン

### SDK

## Xamarin

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

## Visual Studio 2017

### ソリューションとプロジェクト

## Android エミュレーター

## Visual Studio for Mac

## Xcode

## NuGet

## Xamarin.Forms

### 処理の開始点 (エントリーポイント)

### クロスプラットフォームの仕組み

#### プロファイル

#### カスタムレンダラー

#### DependencyService

### XAML

XAML (ザムル) は Xamarin.Forms アプリケーションのユーザーインターフェースを定義することが出来るマークアップ言語です。コードでユーザーインターフェースを定義することも出来ますが、XML ベースの言語である XAML で定義したほうがぱっと見わかりやすいです。また、 **MVVM** (Model-View-ViewModel) アプリケーションを作成するために、データバインディングによって ViewModel と連携させた View を定義できます。

XAML には GUI デザイナーがまだ存在しないので手書きする必要があります。ただし、Visual Studio による補間機能などの支援があるので単純なエディターでプレーンテキストを編集するより少しは楽です。

### レイアウト

#### サイズ

### Messaging Center

Messaging Center はメッセージの送受信を行うためのシンプルなサービスです。メッセージングベースの設計にすることで、コードの結合を減らすことができます。

`MessagingCenter` は静的クラスであり、`Subscribe` メソッドと `Send` メソッドを持っています。

* Subscribe

  シグネチャーを指定してメッセージを待ち、受信したときに何らかの処理を行います。
  複数のサブスクライバーが同じメッセージを受信することもできます。

* Send

  サブスクライバーへメッセージを送ります。サブスクライバーが存在しない場合、そのメッセージは無視されます。

メソッドにはアドレスとなる `message` パラメーターを指定します。また、配信方法をより詳細に制御するためにジェネリックパラメーターも指定します。例え 2 つのメッセージが同じ `message` であっても、ジェネリックパラメーターが異なる場合はそれぞれ別のサブスクライバーに送られます。

`MessagingCenter` の API はシンプルです。

* Subscribe<TSender> (object subscriber, string message, Action<TSender> callback, TSender source = null)

* Subscribe<TSender, TArgs> (object subscriber, string message, Action<TSender, TArgs> callback, TSender source = null)

* Send<TSender> (TSender sender, string message)

* Send<TSender, TArgs> (TSender sender, string message, TArgs args)

* Unsubscribe<TSender, TArgs> (object subscriber, string message)

* Unsubscribe<TSender> (object subscriber, string message)

#### MessagingCenter の使い方

メッセージングはおそらくユーザーインタラクション (例えばボタンのタップ) やシステムイベント (例えばコントロールの状態の変化)、またはほかの事象 (例えば非同期ダウンロードの完了) として送ることになるでしょう。そしてサブスクライバーはたぶんユーザーインターフェースの見た目の変化やデータの保存、または他の操作などのタイミングを監視するでしょう。

##### シンプルなメッセージ

以下に `message` パラメーターに単純な文字列を渡す例を示します。この例では送信元が `MainPage` 型であることを期待しています。ソリューション内の任意のクラスは次のようにして監視することができます。

```csharp
MessagingCenter.Subscribe<MainPage> (this, "Hi", (sender) => {
    // do something whenever the "Hi" message is sent
});
```

`MainPage` クラスに次のような記述をすることで上記のサブスクライバーにメッセージを送ることができます。

```csharp
MessagingCenter.Send<MainPage> (this, "Hi");
```

上記のように書くことで、なにかのイベントのタイミング (アップロードが完了した場合など。この例だと `Hi` イベント😆) だけを知ることができます。

#### 引数を渡す

引数を渡す場合は `Subscribe` のジェネリックパラメーターに引数の型を指定します。

```csharp
MessagingCenter.Subscribe<MainPage, string> (this, "Hi", (sender, arg) => {
    // do something whenever the "Hi" message is sent
    // using the 'arg' parameter which is a string
});
```

送信元も同様に `Send` メソッドにジェネリックパラメーターで引数の型を指定します。

```csharp
MessagingCenter.Send<MainPage, string> (this, "Hi", "John");
```

この例では `string` 型を渡していますが C# のどんな型でも渡すことができます。

#### 監視の解除

`Unsubcribe` メソッドに対象のシグネチャー (アドレスとジェネリックパラメーター) を指定することで、一致する監視を解除することができます。

```csharp
MessagingCenter.Unsubscribe<MainPage> (this, "Hi");
MessagingCenter.Unsubscribe<MainPage, string> (this, "Hi");
```

**参考**

* [MessagingCenter - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/application-fundamentals/messaging-center/)

### トリガー

XAML 上で宣言的にイベントまたはプロパティーの変化と連動してコントロールの見た目を変更することが出来ます。

トリガーには 4 種類あります。

* プロパティートリガー

  コントロールのプロパティーが特定の値に変化したタイミングと連動することができます。

* データトリガー

  他のコントロールのプロパティーと連動させることができます。

* イベントトリガー

  コントロールのイベントが発生したタイミングと連動させることができます。

* マルチトリガー

  複数のトリガーを条件にすることができます。

#### プロパティートリガー

シンプルなトリガーは素の XAML で、対象のコントロールに `Trigger` 要素を追加することで表現できます。次の例ではフォーカスを受け取ったときに `Entry` の背景色を変更します。

```xml
<Entry Placeholder="enter name">
    <Entry.Triggers>
        <Trigger TargetType="Entry"
             Property="IsFocused" Value="True">
            <Setter Property="BackgroundColor" Value="Yellow" />
        </Trigger>
    </Entry.Triggers>
</Entry>
```

次にトリガーの定義で重要な部分を示します。

* TargetType

  トリガーを適用するコントロールの型を指定します。

* Property

  適用するコントロールが監視するプロパティーを指定します。

* Value

  監視するプロパティーがこの値になったタイミングで Setter 要素の内容が反映されます。

* Setter

  トリガーの条件を満たしたときに `Setter` 要素のコレクションが反映されます。`Property` と `Value` 属性を指定する必要があります。

* EnterActions と ExitActions

  Setter の代わり、もしくは追加で反映するコードを記述できます。詳しくは後述します。

##### スタイルでトリガーを使う

アプリの `ResourcesDictionary`、ページ、またはコントロールの `Style` 要素にもトリガーを適用することができます。次の例ではページ内のすべての `Entry` コントロールに対してスタイルを反映します。

```xml
<ContentPage.Resources>
    <ResourceDictionary>
        <Style TargetType="Entry">
            <Style.Triggers>
                <Trigger TargetType="Entry"
                         Property="IsFocused" Value="True">
                    <Setter Property="BackgroundColor" Value="Yellow" />
                </Trigger>
            </Style.Triggers>
        </Style>
    </ResourceDictionary>
</ContentPage.Resources>
```

#### データトリガー

他のコントロールのプロパティー値の変化を監視して、その変化に連動してトリガーを反映することが出来ます。プロパティートリガーでの `Property` 属性の代わりに `Binding` 属性に指定した値と連動します。

次の例の `{Binding Source={x:Reference entry}, Path=Text.Length}` の部分でどのようにバインディングすれば良いかわかると思います。`entry` (`x:Name` 属性が一致する要素) の `Text.Length` プロパティーの値が 0 になったときにトリガーが反映されます。つまり、入力欄が空になったときにボタンが無効化されます。

```xml
<!-- the x:Name is referenced below in DataTrigger-->
<!-- tip: make sure to set the Text="" (or some other default) -->
<Entry x:Name="entry"
       Text=""
       Placeholder="required field" />

<Button x:Name="button" Text="Save"
        FontSize="Large"
        HorizontalOptions="Center">
    <Button.Triggers>
        <DataTrigger TargetType="Button"
                     Binding="{Binding Source={x:Reference entry},
                                       Path=Text.Length}"
                     Value="0">
            <Setter Property="IsEnabled" Value="False" />
        </DataTrigger>
    </Button.Triggers>
</Button>
```

上記の例のような場合、監視対象のプロパティーにデフォルト値を指定してください。指定しない場合 null になってしまうためトリガーが反映さません。

`Setter` 要素を追加することにより `EnterActions` と `ExitActions` も適用することができます。

#### イベントトリガー

`EventTrigger` 要素は `Clicked` などの `Event` プロパティーのみ指定する必要があります。

```xml
<EventTrigger Event="Clicked">
    <local:NumericValidationTriggerAction />
</EventTrigger>
```

`Setter` 要素はありませんが、ページに `xmlns:local` を定義して `local:NumericValidationTriggerAction` を参照していることに注意してください。

```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:WorkingWithTriggers;assembly=WorkingWithTriggers"
```

`NumericValidationTriggerAction` クラスは `TriggerAction` クラスを implements し、トリガーイベントが発生するたびに呼ばれる `Invoke` メソッドを実装するべきです。

トリガーアクションは以下の処理を実装するべきです。

## パフォーマンス

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

Fast renderers は、ネイティブビューの階層を平坦化することにより Android 上の Xamarin.Forms コントロールの inflation とレンダリングコストを削減します。これによってビジュアルツリーの複雑さとメモリーの使用量を減らしパフォーマンスを改善します。Fast renderers の詳細については [Fast Renderers - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/under-the-hood/fast-renderers/) を参照してください。良いケースだとビューの数が半分程度になります。

**参考**

* [Layout Compression - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/user-interface/layouts/layout-compression/)

## コミュニティ

## 書籍

## デバッグ

### Xamarin.Android のデバッグビルドとデプロイ

### Xamarin.iOS のデバッグビルドとデプロイ

### iOS シミュレーター

### デバッグプレビュー

#### Live Inspector

#### Android Device Monitor
