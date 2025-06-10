# ウィジェットの基本レイアウト（教科書P74～95）
今回Flutterのレイアウトを考えるにあったって以下のリンクから`Flutter Studio`にとんで学習していく。  
[Flutter Studio](https://flutterstudio.app/)  
Flutter Studioの画面では左側から必要なウィジェットをドラッグ＆ドロップし、ウィジェット選択後に出てくる右側のプロパティの設定によりレイアウトの作成が可能。  
レイアウト作成後は下のタブにある`source code`に切り替えることで、作成したレイアウトのコードを見書きすることができる。
## レイアウトの基本ソースコード
以下のコードはテキストウィジェットを１つだけ使ったコードである
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
## テーマを指定する  
