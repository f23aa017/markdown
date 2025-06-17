# ボタン・ウィジェット  
教科書P98~131(Chapter3)  
## TextButtonについて
特徴を持たない平面のボタンであるテキストボタンは`TextButtonクラス`として用意されてる。  
配置するには「Material」にある`FlatButton`からドラッグ＆ドロップ。  
また、FlutterStudioでは古いバージョンのため`FlatButton`となっている。そのためコードを一部変更する必要がある。今回は基本的な使い方がほとんど同じなため**クラス名の変更のみ**している。  
以下は単純な処理を持ったボタンを配置した_MyHomePageStateクラスのコードである。  
> class _MyHomePageState extends State<MyHomePage> {  
  static var _message = 'ok.';  
  static var _janken = <String>['グー','チョキ','パー'];  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:  
          new Center(  
            child:  
              new Column(  
                mainAxisAlignment: MainAxisAlignment.start,  
                mainAxisSize: MainAxisSize.max,  
                crossAxisAlignment: CrossAxisAlignment.stretch,  
                children: <Widget>[  
                  new Padding(  
                    padding: const EdgeInsets.all(24.0),  
                      child: Text(  
                      _message,  
                      style: TextStyle(  
                        fontSize: 32.0,  
                        fontWeight: FontWeight.w400,  
                        fontFamily: "Roboto"),  
                    ),  
                  ),  
                  new TextButton(key:null,  
                    onPressed: buttonPressed,  
                    child: Padding(  
                      padding: EdgeInset.all(10.0),  
                      child: new Text(  
                        "Button",  
                          style: new TextStyle(  
                          fontSize:40.0,  
                          color: const Color(0xFF000000),  
                          fontWeight: FontWeight.w500,  
                          fontFamily: "Roboto"),  
                        )  
                      )
                    )  
                ]  
              ),  
          ),  
      );  
    }  
    void buttonPressed(){  
      setState(() {  
        _message = (_janken..shuffle()).first;  
      });
    }  
}  

このコードはグー、チョキ、パーをランダムに表示するサンプルでぽ端を押すとじゃんけんの手が表示される。  
_messageに_janken..shuffle()でシャッフルしたListの最初の項目を取り出しているが、shuffleに返り値はないため**カスケード記法（..演算子）** を使いfirstで最初の要素を取り出している。  
### TextButtonの基本形  
`onPressed`は、TextButtonをクリックしたときに実行される処理を指定する値。通常では関数やメソッドが指定される。  
`child`は内部に組み込むウィジェットでクリックするボタンのテキストやアイコンなどを表示することができる。  
>new TextButton(key:null,  
  onPressed: buttonPressed,  
  child: Padding(  
      (略)  
  )  
)  
### Paddingについて  
`Padding`は余白（パディング）を表示するためのコンテナでウィジェットを組み込むと、その周囲に余白を作成する。余白は`paddingプロパティ`にEdgeInsetsを使って設定する。使用したいウィジェットにpaddingプロパティがある場合は使用する必要がない。  
## ElevatedButtonについて  
`ElebatedButton`はTextButtonと同じ働きをするがこちらはボタンが少し立体的に表示されている。  
配置するにはMaterial内にある`RaisedButton`をドラッグ。またTextButton同様古いバージョンになっているが基本的な使い方はほぼ同じためウィジェット名を置き換えて利用する方向とする。  
配置すると右側にフォント、カラーパレット、Size、Weightのプロパティが用意される。  
以下はElebatedButtonのみのコードである。  
>new RaisedButton(key:null,  
  onPressed:buttonPressed,  
  padding: EdgeInsets.all(10.0),  
  child:  
    new Text(  
      "BUTTON 1",  
        style: new TextStyle(fontSize:42.0,  
        color: const Color(0xFF000000),  
        fontWeight: FontWeight.w500,  
        fontFamily: "Roboto"),  
    )  
)  
## IconButtonについて  
`IconButton`はすでにあるアイコンの中から表示するものを選んで作成するボタンで、クリックして利用することは変わらない。  
配置するにはMaterial2からドラッグ。右側にはカラーパレット、アイコンの種類、Sizeのプロパティが表示される。  
以下はIconButtonのみのコードである。  
>new IconButton(  
  icon: const Icon(Icons.insert_emoticon),  
  onPressed:iconButtonPressed,  
  iconSize: 88.0,  
  color: const Color(0xFF000000),  
)  

IconButtonインスタンスを作成する際、以下の値が用意される。  
- icon  
表示するアイコン。Iconインスタンスとして用意する  
- onPressed  
クリックしたときに実行するメソッド  
- iconSize  
アイコンサイズ。double値で指定  
- color  
アイコンの色  
`icon`ではIconインスタンスを使用するが、constすると引数にIconsクラスの値を使って使用アイコンを指定する。  
また、IconButtonはコンテナではないため、中にウィジェットを組み込むことはできない。  
## FloatingActionButtonについて  
`FloatingActionButton`は画面右下に自動的にアイコンのボタンを表示するウィジェット。これは普通のボタンとしてウィジェットに組み込んで使うことができる。  
以下はFloatingActionButtonのみのコードである。  
>floatingActionButton: new FloatingActionButton(  
  child: new Icon(Icons.add_circle),  
  onPressed: fabPressed)  
## RawMaterialButtonについて  
`RawMaterialButton`はテーマなどによる初期値の設定の影響を受けずに自身で使用する色をすべて設定できる。  
以下はRawMaterialButtonのみのコードである。  
>RawMaterialButton(  
  fillColor: Colors.white,  
  elevation: 10.0,  
  padding: EdgeInsets.all(10.0),  
  child: new Text(  
      "Button",  
      style: new TextStyle(  
      fontSize:40.0,  
      color: const Color(0xFF000000),  
      fontWeight: FontWeight.w500,  
      fontFamily: "Roboto"),  
  ),  
  onPressed: buttonPressed  
)  

RawMaterialButtonには主に以下の表示に関する値が用意されている。  
- fillColor  
背景色  
- highlightColor  
クリックしてハイライトした時の色  
- splashColor  
クリックされたことを表す効果として使われる色  
- elevation  
ボタンの高さ（影の幅）  
- highlightElevation  
クリックしたときのボタンの高さ（影の幅）  
# 入力のためのUI  
## TextFieldについて  
`TextField`はテキストを入力するUIウィジェット。  
次のコードはテキストを入力し、ボタンをクリックするとメッセージが表示される_MyHonePageStateクラスのソースコードである。  
>class _MyHomePageState extends State<MyHomePage> {  
  static var _message = 'ok.';  
  static final _controller = TextEditingController();
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:new Center(  
          new Column(  
            mainAxisAlignment: MainAxisAlignment.start,  
            mainAxisSize: MainAxisSize.max,  
            crossAxisAlignment: CrossAxisAlignment.stretch,  
            children: <Widget>[  
              new Padding(  
                padding: const EdgeInsets.all(24.0),  
                child: Text(  
                  _message,  
                  style: TextStyle(  
                    fontSize: 32.0,  
                    fontWeight: FontWeight.w400,  
                    fontFamily:  "Roboto"),
                ),
              ),  
              new Padding(  
                padding: const EdgeInsets.all(24.0),  
                child: new TextField(  
                  controller: _controller,  
                  style: new TextStyle(  
                    fontSize: 38.0,  
                    color: const Color(0xFF000000),  
                    fontWeight: FontWeight.w500,  
                    fontFamily: "Roboto"),  
                ),  
              ),  
              new ElevatedButton(key:null,  
                child: new Text(  
                  "BUTTON 2",  
                    style: new TextStyle(  
                      fontSize:40.0,
                      color: const Color(0xFF000000),  
                      fontWeight: FontWeight.w500,  
                      fontFamily: "Roboto"),  
                ),  
              onPressed: buttonPressed),
            ],  
          ),  
        ),
      );  
    }  
    void buttonPressed(){  
      setState(() {  
        _message = 'you said: ' + _controller.text;  
      });  
    }   
}  
## TextFieldとController  
TextFieldでは`controller`と`style`という引数があり、styleはテキストスタイルを設定するものである。  
>child: new TextField(  
  controller: <TextEditingController>,  
  style:<TextStyle>  
)  
### Controllerとは  
`Controller`はウィジェットの値を管理するための専用のクラス。各Controllerには各_controllerというフィールドを用意する。  
今回のコードでは`static final _controller = TextEditingController();`でインスタンスを作成し、`_message = 'you said: ' + _controller.text;`で入力したテキストをほかのものと組み合わせて設定するとなっている。  
## onChangedイベントの利用  
`onChanged`とはTextFieldウィジェットに用意されているイベントでテキストが修正されると発生する。これを利用することで、リアルタイムに入力値を利用した処置を行うことができる。  
以下のコードの変更点は`TextFieldにonChanged: textChanged,  の追加`、`ElevatedButton()の削除`、`buttonPressed()からvoid textChanged(String val){}への変更`でそれ以外は割愛。
>child: new TextField(  
  onChanged: textChanged,  
  controller: _controller,  
  style: new TextStyle(  
    fontSize: 38.0,  
    color: const Color(0xFF000000),  
    fontWeight: FontWeight.w500,  
    fontFamily: "Roboto"),  
),  
(略)  
void textChanged(String val){  
  setState((){  
    _message = val.toUpperCase();
  });  
}  
### onChangedメソッドの定義  
onChangedイベントに指定されているtextChangedメソッドではsetStateが用意されている。StatefulWidgetのステートを操作する場合は常にsetStateを使う。