# 複雑な構造のウィジェット  
教科書P１４０～１６９
## AppBarについて  
appBarにはアプリケーションバーを、bodyにコンテンツをセットしていた。しかし、AppBarには用意されているプロパティがほかにもある。  
以下はインスタンス作成の基本形と各項目の説明であり、コードでは各プロパティにウィジェットを配置した_MyHomePageStateクラスの例である。  
>AppBar(  
    title: ウィジェット,  
    leading: ウィジェット,  
    actions: <Widget>[ウィジェットのリスト],  
    bottom: 《PreferredSize》,  
)  
- title  
タイトル表示部分。通常はTextを用意。  
- leading  
左端に表示される。通常はボタン化アイコンを用意。  
- actions  
上記の下に追加表示される部分。PreferredSizeインスタンスを用意。  
>class _MyHomePageState extends State<MyHomePage> {  
    statec var _message = 'ok';  
    statec var _stars = '☆☆☆☆☆';  
    statec var _star = 0;  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          leading: BackButton(  
            color: Colors.white,  
          ),  
          actions: <Widget>[  
            IconButton(  
                icon: Icon(Icons.android),  
                tooltip: 'add star...',  
                onPressed: iconPressedA,  
            ),  
            IconButton(
                icon: Icon(Icons.favorite),  
                tooltip: 'subtract star...',  
                onPressed: iconPressedB,  
            ),  
          ],  
          bottom: PreferredSize(  
            preferredSize: const Size.fromHeight(30.0),  
            child: Center(  
                child: Text(_stars,  
                    style: TextStyle(  
                        fontSize: 22.0,  
                        color: Colors.white,  
                    ),  
                ),  
            ),  
          ),  
        ),  
        body: Center(  
            child: Text(  
                _message,  
                style: const TextStyle(  
                    fontSize: 28.0,  
                ),  
            )  
        ),  
      );  
    }  
    void iconPressedA() {  
        _message = 'tap "android".';  
        _star++;  
        update();  
    }  
    void iconPressedB() {  
        _message = 'tap "favorite".';  
        _star--;  
        update();  
    }  
    void update() {  
        _star = _star < 0 ? 0 : _star > 5 ? 5 : _star;  
        setState(() {  
            _stars = '★★★★★☆☆☆☆☆'.substring(5 - _star, 5 - _star + 5) ;  
            _message = _message + '[$_star]';  
        });  
    }  
}  
### BackButton(leading)について  
BackButtonは前に戻る専用のボタンで、プロパティはcolorによるアイコンの色の指定のみ。
### actionsのアイコンについて  
actionsはタイトルの右側の限られたエリアに表示するAppBarで最も活用される部分。範囲が狭いためアイコンなど小さいスペースで表示内容が分かるものを使う。
### bottomの表示  
`PreferredSize`はサイズを示すpreferredSizeと中に組み込むchildを用意する。preferredSizeには、Sizeクラスの「fromHeight」を使い、childには画面に表示するテキストを用意している。  
## BottomNavigationBarについて  
`BottomNavigationBar`は画面下部にバーを表示するウィジェットである。これを配置するには「Material」から対象のものをドラッグ。そして追加したバーに「BotoomNabigationBarItem」をドラッグすると、項目が追加され、ぷぉぱてぃらんにアイコンとタイトルを設定する表示が追加される。  
以下のコードはBottomNabigationBarを利用した_MyHomePageStateクラスの例である。  
>class _MyHomePageState extends State<MyHomePage> {  
    statec var _message = 'ok';  
    statec var _index = 0;  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body:new Center(   
            child: new Text(  
              _message,  
                style: const TextStyle(  
                    fontSize:29.0,  
                ),  
            )  
          ),  
        bottomNavigationBar: new BottomNavigationBar(  
            currentIndex: _index,  
            backgroundColors.lightBlueAccent,  
            items: <BottomNabigationBarItem>[  
                BottomNabigationBarItem(  
                    label: 'Android',  
                    icon: Icon(Icons.android,color: Colors.black, size: 50),  
                ),  
                BottomNabigationBarItem(  
                    label: 'Favorite',  
                    icon: Icon(Icons.favorite,color: Colors.red, size: 50),  
                ),  
                BottomNabigationBarItem(  
                    label: 'Home',  
                    icon: Icon(Icons.android,color: Colors.white, size: 50),  
                ),  
            ],  
            onTap: tapBottomIcon,  
        ),  
      );  
    }  
    void tapBottomIcon(int value){  
        var items = ['Android','Heart','Home'];  
        setState(() {  
            _index = value;  
            _message = 'you tapped: "' + items[_index] + '".';  
        });  
    }  
}  
### BottomNavigationBarの仕組み  
疲れた