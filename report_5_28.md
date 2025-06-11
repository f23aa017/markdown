# ボタン・ウィジェット  
教科書P98~131(Chapter3)  
## TextButtonについて
特徴を持たない平面のボタンであるテキストボタンは`TextButtonクラス`として用意されてる。  
配置するには「Material」にある`FlatButton`からドラッグ＆ドロップ。  
また、FlutterStudioでは古いバージョンのため`FlatButton`となっている。そのためコードを一部変更する必要がある。今回は基本的な使い方がほとんど同じなため**クラス名の変更のみ**している。  
以下は単純な処理を持ったボタンを配置した_MyHomePageStateクラスのコードである。  
> class _MyHomePageState extends State<MyHomePage> {  
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
                crossAxisAlignment: CrossAxisAlignment.center,  
                children: <Widget>[  
                  new Padding(  
                    padding: const EdgeInsets.all(24.0),  
                  ),  
                  new FlatButton(key:null, onPressed:buttonPressed,  
                    child:  
                      new Text(  
                      "Button",  
                        style: new TextStyle(fontSize:40.0,  
                        color: const Color(0xFF000000),  
                        fontWeight: FontWeight.w500,  
                        fontFamily: "Roboto"),  
                      )  
                    )  
                ]  
              ),  
          ),  
      );  
    }  
    void buttonPressed(){}  
}  
教科書９９ページを見て補完する