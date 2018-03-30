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
        - [マルチトリガー](#マルチトリガー)
            - [すべての入力を必須とするマルチトリガーを作成する](#すべての入力を必須とするマルチトリガーを作成する)
        - [EnterActions と ExitActions](#enteractions-と-exitactions)
    - [ジェスチャー](#ジェスチャー)
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

## Xamarin.Forms をはじめた人のための Tips

さらっと読んで頭の片隅にうろおぼえながらでも入ってると、後の開発中のハマりが少なくすむかもしれないです。

### StackLayout や Grid の子要素間にはデフォルトで余白が設定されている

### Device.BeginOnMainThread メソッドの実行順序はプラットフォームによって違う

### INotifyPropertyChanged がうざったいときは PropertyChanged.Fody という選択肢がある

### UI スレッドとワーカースレッド

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

`NumericValidationTriggerAction` クラスは `TriggerAction` クラスを implement し、トリガーイベントが発生するたびに呼ばれる `Invoke` メソッドを実装するべきです。

トリガーアクションは以下の実装を行ってください。

* `TriggerAction<T>` を implement する際に、トリガーを適用するコントロールの型を指定します。`VisualElement` を指定することでさまざまなコントロールで動作するトリガーアクションを作成したり、`Entry` のような特定のコントロールの型を指定することができます

* トリガーの条件が満たされるたびに呼ばれる `Invoke` メソッドをオーバーライドします

* 必要に応じて、XAML 上でトリガーを定義する際に設定できるプロパティーを公開します (この例に追加するとすれば、文字数を制限するために `MinLength` プロパティーを `public` で定義することになるでしょう)

```csharp
public class NumericValidationTriggerAction : TriggerAction<Entry>
{
    protected override void Invoke (Entry entry)
    {
        double result;
        bool isValid = Double.TryParse (entry.Text, out result);
        entry.TextColor = isValid ? Color.Default : Color.Red;
    }
}
```

上記の例では追加していませんが、もし `MinLength` プロパティーを公開した場合は次のようにトリガーアクションを定義します。

```xml
<EventTrigger Event="TextChanged">
    <local:NumericValidationTriggerAction MinLength="10" />
</EventTrigger>
```

ResourceDictionary で複数のコントロールにトリガーを適用した場合、すべてのコントロールに同じ変更が反映されてしまうので注意してください。

また、イベントトリガーでは `EnterActions` と `ExitActions` がサポートされていないので気をつけてください。

#### マルチトリガー

マルチトリガーは単一の条件のときはトリガーやデータトリガーに似ています。条件が複数ある場合はそれらすべてが満たされない限り反映されることはありません。

次の例では 2 つの入力 (email と phone) に対してボタンのトリガーをバインドしています。

```xml
<MultiTrigger TargetType="Button">
    <MultiTrigger.Conditions>
        <BindingCondition Binding="{Binding Source={x:Reference email},
                                   Path=Text.Length}"
                               Value="0" />
        <BindingCondition Binding="{Binding Source={x:Reference phone},
                                   Path=Text.Length}"
                               Value="0" />
    </MultiTrigger.Conditions>

  <Setter Property="IsEnabled" Value="False" />
    <!-- multiple Setter elements are allowed -->
</MultiTrigger>
```

`Conditions` コレクションは次のような `PropertyCondition` 要素を持つことができます。

```xml
<PropertyCondition Property="Text" Value="OK" />
```

##### すべての入力を必須とするマルチトリガーを作成する

マルチトリガーはすべての条件が満たされたときだけ反映されます。

すべての入力欄のテキストの長さが 0 かどうかを判定する場合、XAML では表現できないためコードで条件を書く必要があります。

その場合、`IValueConverter` を implement することになります。次のようにコンバーターでテキストの長さが 0 であるかどうかを `bool` に変換してください。

```csharp
public class MultiTriggerConverter : IValueConverter
{
    public object Convert(object value, Type targetType,
        object parameter, CultureInfo culture)
    {
        if ((int)value > 0) // length > 0 ?
            return true;            // some data has been entered
        else
            return false;           // input is empty
    }

    public object ConvertBack(object value, Type targetType,
        object parameter, CultureInfo culture)
    {
        throw new NotSupportedException ();
    }
}
```

マルチトリガーでこのコンバーターを使用する場合、次のようにリソースディクショナリーをページに追加してください (対応する `xmlns:local` 名前空間も)。

```xml
<ResourceDictionary>
   <local:MultiTriggerConverter x:Key="dataHasBeenEntered" />
</ResourceDictionary>
```

XAML は次のようになります (最初のマルチトリガーとして挙げた XAML の例とは少し違うことに注意してください)。

* ボタンはデフォルトで `IsEnabled="false` に設定されます

* マルチトリガーの条件として `Text.Length` を真偽値に変換するコンバーターを使用します

* すべての条件が満たされたとき、ボタンの `IsEnabled` プロパティーが `true` になります

```xml
<Entry x:Name="user" Text="" Placeholder="user name" />

<Entry x:Name="pwd" Text="" Placeholder="password" />

<Button x:Name="loginButton" Text="Login"
        FontSize="Large"
        HorizontalOptions="Center"
        IsEnabled="false">
  <Button.Triggers>
    <MultiTrigger TargetType="Button">
      <MultiTrigger.Conditions>
        <BindingCondition Binding="{Binding Source={x:Reference user},
                              Path=Text.Length,
                              Converter={StaticResource dataHasBeenEntered}}"
                          Value="true" />
        <BindingCondition Binding="{Binding Source={x:Reference pwd},
                              Path=Text.Length,
                              Converter={StaticResource dataHasBeenEntered}}"
                          Value="true" />
      </MultiTrigger.Conditions>
      <Setter Property="IsEnabled" Value="True" />
    </MultiTrigger>
  </Button.Triggers>
</Button>
```

#### EnterActions と ExitActions

EnterActions と ExitActions コレクションを追加し、`TriggerAction<T>` を実装したクラスを指定することで、トリガーが反映される際の変更内容をコードで表現することができます。

`EnterActions` と `ExitActions` と共に `Setter` も指定することができますが、`EnterActions` や `ExitAction` とは違って即座に実行されます (`EnterActions` や `ExitActions` の完了を待ちません)。とはいえ、`Setter` で出来ることはすべてコードで表現することができます。

```xml
<Entry Placeholder="enter job title">
    <Entry.Triggers>
        <Trigger TargetType="Entry"
                 Property="Entry.IsFocused" Value="True">
            <Trigger.EnterActions>
                <local:FadeTriggerAction StartsFrom="0" />
            </Trigger.EnterActions>

            <Trigger.ExitActions>
                <local:FadeTriggerAction StartsFrom="1" />
            </Trigger.ExitActions>
                        <!-- You can use both Enter/Exit and Setter together if required -->
        </Trigger>
    </Entry.Triggers>
</Entry>
```

XAML でクラスを参照する際は `xmlns:local` などのようにして使用する名前空間を指定する必要があります。

```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:WorkingWithTriggers;assembly=WorkingWithTriggers"
```

`FadeTriggerAction` の実装は次のようになります。

```csharp
public class FadeTriggerAction : TriggerAction<VisualElement>
{
    public FadeTriggerAction() {}

    public int StartsFrom { set; get; }

    protected override void Invoke (VisualElement visual)
    {
            visual.Animate("", new Animation( (d)=>{
                var val = StartsFrom==1 ? d : 1-d;
                visual.BackgroundColor = Color.FromRgb(1, val, 1);

            }),
            length:1000, // milliseconds
            easing: Easing.Linear);
    }
}
```

`EnterActions` と `ExitActions` はイベントトリガー上では無視されることに注意してください。

**参考**

* [Triggers - Xamarin](https://developer.xamarin.com/guides/xamarin-forms/application-fundamentals/triggers/#enterexit)

### ジェスチャー

Xamarin.Forms が提供している Gesture Recognizer はイベントのバブリングがうまく行われません。例えば、子孫要素にハンドラーを指定すると親要素のハンドラーは実行されないため、共通的な処理が書きにくいです。必ずバブリングさせたい場合、有償の MR.Gestures というライブラリーの使用を検討してみてください。このライブラリーではきちんとバブリングしてくれます (宣伝したいわけじゃないですが、それしか 2018-03-17 時点では選択肢がないようにみえます)。

## パフォーマンス

### Layout Compression

#### 概要

Xamarin.Forms 2.5 から導入された Layout Compression を使うことで、ビジュアルツリーから指定されたレイアウトを削除し、ページレンダリングのパフォーマンスが改善されます。この機能は iOS と Android の両方で効果があります。

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
試してみた感じ、`VerticalOptions`、`HorizontalOptions`、`Spacing` はあっても問題なく動いてるように見えます。

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

Windows から Mac Agent 経由でデバッグしてる場合、Mac 側にも同じバージョンの Live Inspector をインストールする必要があります。

#### Android Device Monitor

### ビルドエラー

#### The name 'InitializeComponent' does not exist in the current context

XAML のコンパイルがうまくいってないようです。PCL プロジェクトを Unload してから、Clean、Build すると直ります。

#### The "User7ZipPath" parameter is not supported by the "XamarinDownloadArchives" task. Verify the parameter exists on the task, and it is a settable public instance property.

ビルドタスクのバージョンが古いと色々問題があるらしいです。NuGet でソリューションにインストールされた Xamarin.Build.Download をアップデートし、Visual Studio を再起動すると直ります。
