# GitとVSCodeの結びつけ・プロジェクトの構成

### 動画参考（0520）
***  
**まず今後作成するプロジェクトを保存するフォルダーを作成する**  
- フォルダーを好きなところに作成  
- フォルダーのパスをコピーする  
- コピーしたパスをVSCodeのフォルダー選択に張り付ける
> Ctrl + @でターミナルが開ける  
 
 **次にflutterが学習できる環境を作っていく**  
- 作成したフォルダーをVSCodeで開いたままターミナルに以下のコマンドを入力する  
> flutter create sample  
>> sampleは好きな名前（半角英字）  

**GitとVSCodeを結びつける**
- ソース管理からGithubに公開をクリック
- Gitに公開したいフォルダ、ファイルを選択
***
### 教科書P50~58追加参考
***
**以降はインストールしたflutterのプロジェクト構成になる**  
- プロジェクトのファイル構成（フォルダ類）
    - .dart_tool →Dart言語が自動生成するファイル類を保管するところ
    - .idea →IntelliJ IDEA開発ツールの設定情報
    - bulid →ビルドして生成されるファイル類
    - android、ios、linux、windows、web →各アプリ生成に必要なファイル類
    - lib →Dartのスクリプトが保持される
    - test →ユニットテスト関連のファイル類
- プロジェクトのファイル類
    - （重要）.gitignore →Gitに上げるファイルを指示するファイル
    - .metadata →Flutterツールが利用するファイル
    - .packages →利用しているパッケージ情報
    - anarysis_options.yaml →Dartの分析に関するファイル
    - flutter_app.iml →モジュール定義ファイル
    - pubspec.lock →Pubが利用するファイル
    - pubspec.yaml →Pubが利用するファイル
    > Pub →Dartのパッケージマネージャ
    - （重要）README.md →このプロジェクトの説明書（自分で改ざんしていく）

この中で学習する際にメインでいじっていくフォルダーは`libフォルダのmain.dart`である

***
**fluterのアプリ画面とウィジェットツリー**  
　Flutterの画面表示では、画面を表示するパーツや文字を表示するパーツなど様々なパーツによって画面を作成する。このパーツを`ウィジェット`と呼ぶ。  
　Flutterのアプリの画面は画面を表示するウィジェットの中に文字を表示するウィジェットを入れるようにウィジェットを階層的に組み込んで作成していく。この組み込み構造を`ウィジェットツリー`と呼ぶ。
>Flutterの特徴としてウィジェットを作成することができる

***
**基礎プログラムの説明**
- １行目_import  
１行目には以下のように記述されている  
これはパッケージ（事前に決められているもの）をインポートする（このプログラムにも引き継ぐ）ことを意味する
>import 'package:flutter/material.dart';  
- ３～５行目_実行  
３行目に記述されている`main関数`は１番最初に実行される関数。４行目に記述されている`runApp`によりMyAppを起動するという意味。
>void main() {  
runApp(const MyApp());  
}  
- ７～１２行目_クラス  
　ウィジェットを作成するうえで基礎となるものを継承する必要がある。それが`StatelessWidgetクラス`。これは、ステート（状態を表す値）を持たない、ウィジェットのベースとなるクラス。  
　このクラスに用意されているメソッドに一つに`build`がある。これはウィジェットを生成する際に呼び出すものである。  
　ウィジェットをデザインするので使われるのが`MaterialApp`。これによりウィジェットに「何か」を表示させることができる。
>class MyApp extends StatelessWidget {  
  @override  
  Widget build(BuildContext context) {  
   return MaterialApp();  
　 }  
  }
  - `MaterialApp`の構成  + Textウィジェット  
　MaterialAppクラスは引数に様々な情報を載せることができる。  
　以下の例文では`title`と`home`の二つの引数を使用している。それぞれ`title`はアプリケーションのタイトルを、`home`はアプリケーションに組み込まれるウィジェットを表す。   
　homeで指定されている`Text`はテキストを表示するウィジェットである。  
　第１引数に表示するテキストを、第２引数に`style`でテキストスタイルを設定している。（`TextStyle`は決まっているものを引っ張ってきているだけ）
> return MaterialApp(  
   title: 'Flutter Demo',  
   home: Text(  
    'Hello, Flutter World!!',  
     style: TextStyle(fontSize:32.0),  
   )  
);  

**まとめ**  
1.プログラムはmain関数から開始するため、`mainにアプリを起動するrunApp関数を記述する。`  
2.`runApp関数はStatelessWidgetクラスを継承したインスタンスを引数に指定する。`これがアプリ本体のUI。  
3.上記を継承したインスタンスには`buildメソッドを用意する`ここでMaterialAppインスタンスをreturnする。  
4.MaterialAppの引数`homeにアプリ内に表示するウィジェットを設定する`。

**マテリアルデザインとFlutter**  
まずMaterialAppは、マテリアルデザインによるウィジェットを作成するためのベースである。`マテリアルデザイン`とはGllgleが提唱する`あらゆるデバイスで共通したルック&フィールを構築した視覚的デザイン言語`。  
Flutterではデフォルトでマテリアルデザインのパッケージ`material.dart`が読み込まれている。（iOS独自性のクパティーノデザイン、`cupertino.dart`も用意されている。）  

**アプリケーションバーと内容**  
スマートフォンのアプリには上部にタイトルを表示するアプリケーションバーがありその下に内容が表示される形である。その形を作るのが`Scaffold`（建築の「足場」）。  
Scafflodにはマテリアルデザインの基本的なデザインとレイアウトが組み込まれており、アプリ作成の土台となる部分を担当する部品である。
> MyAppクラスのところだけ書き換える  
return MaterialApp(  
    title: 'Flutter Demo',  
    home: Scaffold(  
      appBar: AppBar(  
       title: Text('Hello Flutter!'),  
    )  
    body: Text(  
      'Hello, Flutter World!!',  
       style: TextStyle(fontSize:32.0),  
    ),  
    ),  
);  
- Scafflodの構成  
  - appBar  
  ここではアプリケーションバーに値を設定する。  
  また、AppBarというクラスのインスタンスが設定されており、これはアプリケーションバーのウィジェットクラスになる。  
  - body  
  アプリケーションバーの下のク泊エリア全体の表示を担当する。実際のアプリの表示場所。
