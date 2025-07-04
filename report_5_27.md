# ウィジェットの基本レイアウト（教科書P74～95）
今回Flutterのレイアウトを考えるにあったって以下のリンクから`Flutter Studio`にとんで学習していく。  
[Flutter Studio](https://flutterstudio.app/)  
Flutter Studioの画面では左側から必要なウィジェットをドラッグ＆ドロップし、ウィジェット選択後に出てくる右側のプロパティの設定によりレイアウトの作成が可能。  
レイアウト作成後は下のタブにある`source code`に切り替えることで、作成したレイアウトのコードを見書きすることができる。
## レイアウトの基本ソースコード
以下のコードはテキストウィジェットを１つだけ使ったコード（以降基礎コード）である
>import 'package:flutter/material.dart';
>>void main() {  
  runApp(new MyApp());  
}

>>class MyApp extends StatelessWidget {  
  @override  
  Widget build(BuildContext context) {  
    return new MaterialApp(  
      title: 'Generated App',  
      theme: new ThemeData(  
        primarySwatch: Colors.blue,  
        primaryColor: const Color(0xFF2196f3),  
        accentColor: const Color(0xFF2196f3),  
        canvasColor: const Color(0xFFfafafa),  
      ),  
      home: new MyHomePage(),  
    );  
  }  
}  

>>class MyHomePage extends StatefulWidget {  
  MyHomePage({Key? key}) : super(key: key);  
  @override  
  _MyHomePageState createState() => new _MyHomePageState();  
}  

>>class _MyHomePageState extends State<MyHomePage> {  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Text(  
          "Hello Flutter!",  
            style: new TextStyle(fontSize:32.0,  
            color: const Color(0xFF000000),  
            fontWeight: FontWeight.w700,  
            fontFamily: "Roboto"),  
          ),  
      );  
    }  
}  

**現在MyHomePageクラスのMyHomePage({Key key}) : super(key: key);でエラーが発生する。**
これを解消するためには`MyHomePage({Key? key}) （略）`と書き換える必要がある。  
Textウィジェットの追加により変更が加えられたのは
**_MyHomePageState**である。  
Textウィジェットはstyleという値を使って５つの項目が設定できる。  
- fontSize  
フォントサイズ。double値で指定。
- color  
テキスト色。Colorクラスで指定。  
Colorクラスでは引数に６，８桁の１６進数でRGB、ARGBを表現する。   別の表現で`Color.fromARGB(アルファ、赤、緑、青)`と記述することができ、各値に０～２５５で指定する。  
Colorを使用する際は、メモリ節約にもなるため`const`で定数としていることが基本である。   
また、Colors.blueのように用意されているプロパティを指定することによる設定もできる。
- fontWeight  
フォントの太さ。FontWeightというクラスのw１００～w９００、またはblodという定数で指定。
- fontFamily  
フォントファミリー。テキスト（String）で指定。
- fontStyle  
フォントスタイル。FontStyle列挙型のnomal、italicという値で指定。  
## テーマ（見た目）を指定する
テーマは画面表示のベースとなるウィジェットで設定する。  今回は基礎コードの`MyApp`内で作成される`MaterialAppインスタンス`で指定する。また、基礎コードではMaterialAppを作成する際、themeに`ThemeData`が設定されテーマ関連の色の値がまとめられている。  
以下はテーマ関連のプロパティとなる。  
- Dark Theme  
ダークテーマをON/OFFするもの。通常の表示はOFFに、暗い背景をベースにした表示にしたければONにしておく。
- Primary Swatch  
テーマの基本的な色を指定する。
- Primary Color  
標準のテキストなどの色
- Accent Color  
アクセントの色
- Devider Color  
仕切り線の色
- Canvas Color  
キャンバス（グラフィック描画の部品）の色
- Background Color  
背景色として表示を作る際に使われる色
- FontFamily  
使用するフォントファミリーの指定
## Centerによる中央揃え  
中央揃えにすると大きさが変わっても大体同じような表示になる。  
サイドバーから`Layout`を選択し`Center`を画面にドラッグ＆ドロップ。そのうえからTextウィジェットを配置すると画面中央へ移動する。（web上ではうまく動かない）  
以下は上記の動作を実行し変更があった`_MyHomePageStateクラス`のコードである。
>class _MyHomePageState extends State<MyHomePage> {  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Center(  
            child:  
              new Text(  
              "qWerty1",  
                style: new TextStyle(fontSize:47.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
          ),  
      );  
    }  
}  
### Centerクラスの基本形  
今まで用意していたTextウィジェットの周りを`Center`で囲みchildという値に記述する形となっている。  
## Containerクラスについて  
Containerクラスとはウィジェットの細かい配置の設定を行えるクラス。コンテナ（ほかのウィジェットを自身の中に格納できるウィジェット）の最も基本的なクラスである。  
配置方法はCenterと同じでLayoutから目的のものをドラッグ＆ドロップ。すると右側に以下のプロパティが表示される。
- Color  
色の指定。ONにするとコンテナ独自の背景色を設定できる。
- Alignment  
配置場所の指定。上下左右を9か所に分け、選択する。
- Sized  
表示サイズを最大化するためのもの
- Padding  
余白幅の設定。上下左右の余白を整数で指定する。  
以下は上記の動作を実行し変更があった`_MyHomePageStateクラス`のコードである。
>class _MyHomePageState extends State<MyHomePage> {  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Container(  
            child:  
              new Text(  
              "qWerty1",  
                style: new TextStyle(fontSize:42.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
            padding: const EdgeInsets.all(0.0),  
            alignment: Alignment.bottomCenter,  
          ),  
      );  
    }  
}  
### Containerクラスの基本形  
Center同様、中に組み込むウィジェット（今回Text）をchildに指定した。ほかに`padding`と`alignment`が用意されており、これはそれぞれ余白と位置揃えを設定している。また、ColorのチェックをONにし、色を指定した場合はconst Colorインスタンスに手色の値が指定される。  
### EdgeInsetsについて（padding）  
paddingは周辺の余白を指定していて、`EdgeInsetsクラス`を使っている。  
EdgeInsetsクラスは上下左右の余白幅を設定するためのものでいくつかのメソッドを使ってインスタンスを作成する。用意されている主なメソッドが以下のとおりである。
- 全方向指定  
allは引数で指定した値に上下左右全ての余白幅を設定する。
>EdgeInsetes.all(《double》)  
- 個別に設定  
fromLTRBは左・上・右・下の順に余白幅を数値で指定する。全部で４つの引数を用意する必要がある。
>EdgeInsetes.fromLTRB(左,上,右,下)  
- 個別に設定  
onlyは上下左右のうち、必要な項目だけを指定するもの。省力した場合ゼロが指定。  
>const EdgeInsetes.only(left:左,top:上,right:右,bottom:下)  
- シンメトリック  
symmetricは横（左右）と縦（上下）にそれぞれ同じ値を設定する。引数には横の余白幅と縦の余白幅をそれぞれ指定する。  
>const EdgeInsetes.symmetric(横,縦)  
### Alignmentについて  
alignmentは配置場所を示していて、`Alignmentクラス`を使っている。Alignmentクラスは用意されている定数、もしくは-1.0~1.0の範囲で全体の位置を指定する。  
定数と公式は以下のとおりである。  
- topLeft → 左上  
- topCenter → 中央上  
- topRight → 右上  
- centerLeft → 左中央  
- centerCenter → 中央  
- centerRight → 右中央  
- bottomLeft → 左下   
- bottomCenter → 中央下  
- bottomRight → 右下  
数値は左・上に行くほど値が小さくなり、右・下に行くほど値が大きくなる。  
> const Alignment(横,縦)  
# 複数ウィジェットの配置  
## Columnを使う  
実際のデザインでは複数のウィジェットを使って作る。そのため複数のウィジェットを組み込めるコンテナが必要。その中でも`Column`は複数のウィジェットを `縦`に並べて配置するものである。配置の仕方はCenter,Containerと同様のため割愛（Textは追加された縦棒より左側へ）。  
以下はColumnに用意されたプロパティである。  
- Main Axis Alignment  
Columnウィジェットの配置場所を指定する。値はMainAxisAlignmentクラスのatart、center、endのどれか。  
- Cross Axis Alignment  
Columnに組み込まれたウィジェットの吐いて場所を指定する。値は、CrossAxisAlignmentクラスのstart,cente,end,baseline,stertchのどれか。  
- Main Axis Size  
ウィジェットのサイズを指定する。値はMainAsixSizeのmin、maxのどれか。  
> MainAxisAlignmentとCrossAxisAlignmentは、コンテナによって並び方が異なる場合もあるため、ウィジェットがコンテナ内に配置された最初の位置かコンテナの一番後の位置という形で配置場所を決める。  

Column追加後変更があった_MyHomePageStateクラスのコード  。
> class _MyHomePageState extends State<MyHomePage> {  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Column(  
            mainAxisAlignment: MainAxisAlignment.start,  
            mainAxisSize: MainAxisSize.max,  
            crossAxisAlignment: CrossAxisAlignment.center,  
            children: <Widget>[  
              new Text(  
              "one",  
                style: new TextStyle(fontSize:41.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
              new Text(  
              "two",  
                style: new TextStyle(fontSize:43.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
              new Text(  
              "three",  
                style: new TextStyle(fontSize:38.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              )  
            ]  
          ),  
      );  
    }  
}  

### Columnの基本形  
Columnクラスを見ると先ほど箇条書きで挙げた`mainAxisAlignment`、`mainAxisSize`、`crossAxisAligment`の3つに加えてColumnに組み込まれるウィジェットを用意する`children`といった値があるのが分かる。Columnはchildrenのリストから順にウィジェットを表示しているため、リストの並びが変われば表示されるぃジェットの順番も変わる。  
## Rowを使う  
Columnの横バージョン。配置の仕方も用意されているプロパティも同じ。以下はRow追加後変更のあったMyHomePageStateクラスのコード。  
> class _MyHomePageState extends State<MyHomePage> {  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Row(  
            mainAxisAlignment: MainAxisAlignment.start,  
            mainAxisSize: MainAxisSize.max,  
            crossAxisAlignment: CrossAxisAlignment.center,  
            children: <Widget>[  
              new Text(  
              "one",  
                style: new TextStyle(fontSize:43.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
              new Text(  
              "two",  
                style: new TextStyle(fontSize:43.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              ),  
              new Text(  
              "three",  
                style: new TextStyle(fontSize:41.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w500,  
                fontFamily: "Roboto"),  
              )  
            ]  
          ),  
      );  
    }  
}  
### Main Axis と Cross Axis  
複数のウィジェットを並べて配置するコンテナでは並ぶ方向を以下のように指定して考える。  
- Main Axis  
ウィジェットが順に並ぶ方向。Columnは縦方向、Rowは横方向。  
- Cross Axis  
並んだウィジェットと交差する方向。Columnは横方向、Rowは縦方向。