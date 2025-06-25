# アラートとダイアログ  
教科書P１３１～１３８
## showDialog関数について  
必要に応じて画面に現れるものにアラートやダイアログというものがある。  
設定するには呼び出すメソッドなどにコーディングする必要がある。  
以下のコードは以降勉強するうえで使いまわしていく_MyHomePageStateクラスの基礎コードである。  
>class _MyHomePageState extends State<MyHomePage> {  
    stateic var _message = 'ok.';  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body: new Center(  
            child: new Column(  
                mainAxisAlignment: MainAxisAlignment.start,  
                mainAxisSize: MainAxisSize.max,  
                crossAxisAlignment: CrossAxisAlignment.stretch,  
                children: <Widget>[  
                  new Padding(  
                    padding: const EdgeInsets.all(24.0),  
                    child: new Text(  
                      "_message",  
                        style: new TextStyle(  
                            fontSize:30.0,  
                            color: const Color(0xFF000000),  
                            fontWeight: FontWeight.w500,  
                            fontFamily: "Roboto"),  
                      ),  
                  ),  
                  new Padding(  
                    padding: const EdgeInsets.all(24.0),  
                  ),  
                  new Padding(  
                    padding: const EdgeInsets.all(24.0),  
                    child: new ElevatedButton(key:null,  
                    onPressed:buttonPressed,  
                        color: const Color(0xFFe0e0e0),  
                        child: new Text(  
                          "BUTTON 1",  
                            style: new TextStyle(fontSize:12.0,  
                            color: const Color(0xFF000000),  
                            fontWeight: FontWeight.w200,  
                            fontFamily: "Roboto"),  
                          )  
                        ),                      
                  )  
                ]  
              ),  
          ),  
      );  
    }  
    void buttonPressed(){  
        showDialog(  
            context: context,  
            builder: (BuildContext context) => AlertDialog(  
                title: Text("Hello!"),  
                content: Text("This is sample."),  
            )  
        );  
    }  
}  
### showDialogの基本  
`showDialog`はアラートなどを画面に表示する関数である。  
引数の`context`にはウィジェットのベースとなるBuildContextクラスのインスタンスを指定し、`builder`にはWidgetBuilderクラスというBuildContextのtypedef（関数型のエイリアス、関数を引数や戻り値などで利用するためのもの）で表示するウィジェットを生成する関数を指定する。  
今回のコードではcontextにはStateクラスに用意されているcontextをそのまま指定している。  
Stateクラスはウィジェットの状態を扱うもので単体で存在することは少なく、何らかのウィジェットに関連付けられている。この関連付けられたウィジェット（BuildContext=ウィジェットツリーにおけるウィジェットのハンドル）を保管しているのがcontextプロパティである。  
このStateにあるcontextをそのままshowDialogのcontextに代入すれば、ウィジェット上にアラート表示できる。  
### AlerDialogについて  
builderの`AlerDialog`ではタイトルとコンテンツを表示するウィジェットをそれぞれtitleとcontextに指定している。  
ほかにも`actions`というプロパティが用意されており、ウィジェットのリストを用意する。これはボタン関係のインスタンスが用いられる。詳細は下記にて記述する。  
## アラートにボタンを追加する  
アラートに様々な働きを用意するには（今回はボタン）`actions`というプロパティに対応するウィジェットを記述する必要がある。  
actionsにはウィジェットのリストを用意する。ここには今回でいうボタンをクリックしたときの処理を用意し、showDialog後にアラートを閉じた後の処理を記述する。  
アラートを閉じた後の処理はshowDialogの後に`then`というメソッドを用意し実行する処理を記述する。thenは非同期に実行されるメソッドであるshowDialogを実行された後の処理を`showDialogのコールバック関数`として用意されるものである。
アラートにボタンを追加するには基礎コードにbuttonPressedメソッドに以下の修正・追記に加えてresultAlertメソッドを追記する。
>void buttonPressed(){  
    showDialog(  
        context: context,  
        builder: (BuildContext context) => AlertDialog(  
            title: Text("Hello!"),  
            content: Text("This is sample."),  
            actions: <Widget>[  
                TextButton(  
                    child: const Text('Cancel'),  
                    onPressd: () => Navigator.pop<Stirng>(context,'Cancel')  
                ),  
                TextButton(  
                    child: const Text('OK'),  
                    onPressd: () => Navigator.pop<Stirng>(context,'OK')  
                )  
            ],  
        ),  
    ).then<void>((value) => resultAlert(value));  
}  
void resultAlert(String value) {  
    setState((){  
        _message = 'selected: $value';  
    });  
}  
### actionsとthen  
actionsのウィジェットの中にあるメソッドに`Navigator.pop`がある。これは表示されているアラートダイアログを消す働きをする。中身はContextとアラートを閉じる際に送られる値を引数にしている。そのため、事前に型の値を決めてコーディングする必要がある。  
thenメソッドの中ではresultAlertメソッドがコールバックとして呼び出されている。この時に渡されるNavigator.popの第二引数に指定されていたvalueをチェックすることでどのボタンを選んだかが判断できる。  
## SimpleDialogについて  
`SimpleDialogクラス`はAlertDialogと同じくDialogというクラスを継承して作られたユーザーに入力をしてもらえるダイアログである。引数のtitleにはタイトルのテキストなどを、childrenには選択肢として表示する項目のリスト`SimpleDialogOptionクラス`のインスタンスを用意する。    
`SimpleDialogOptionクラス`はSimpleDialogの選択肢の項目として使う専用のクラスである。引数のchildには項目内に表示するウィジェットを、onPressedには項目をクリックしたときの処理を用意する。  
書き方が変わるだけで、中の動きはAlertDialogとほぼ同じである。
利用するには基礎コードにbuttonPressedメソッドに以下の修正・追記に加えてresultAlertメソッドをそのまま利用する。そのためbuttonPressedメソッドのみを記述する。  
>void buttonPressed(){  
    showDialog(  
        context: context,  
        builder: (BuildContext context) => SimpleDialog(  
            title: const Text("Select assignment"),  
            actions: <Widget>[  
                SimpleDialogOption(  
                  onPressd: () => Navigator.pop<Stirng>(context,'One'),  
                  child: const Text('One'),  
                ),  
                SimpleDialogOption(  
                  onPressd: () => Navigator.pop<Stirng>(context,'Two'),  
                  child: const Text('Two'),  
                ),  
                SimpleDialogOption(  
                  onPressd: () => Navigator.pop<Stirng>(context,'Three'),  
                  child: const Text('Three'),  
                ),  
            ],  
        ),  
    ).then<void>((value) => resultAlert(value));  
}  
