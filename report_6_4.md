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
`BottomNavigationBar`は画面下部にバーを表示するウィジェットである。これを配置するには「Material」から対象のものをドラッグ。そして追加したバーに「BotoomNabigationBarItem」をドラッグすると、項目が追加され、プロパティ欄にアイコンとタイトルを設定する表示が追加される。  
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
BottomNavigationBarインスタンスの作成は以下の引数によって行っている。  
- currentIndex  
現在、選択されている項目のインデックス。これに設定されたインデックスのアイコン（BottomNavigationBarItem）が選択状態で表示される。  
- items  
表示する項目。BottomNavigationBarItemインスタンスのリストとして用意。  
- onTap  
バーに表示されるアイコンをクリックしたときに出される処理。  
`BottomNavigationBar`はいくつかのアイコンを表示するが気見込まれているウィジェット（BottomNavigationBarItem）個々のイベント処理を設定することができない。まとめて渡すイベント処理はBottomNavigationBarの`onTap`からメソッドに渡される。  
`onTap`に指定するメソッドは引数にクリックした項目のインデックス番号であるint値が渡され処理を行う。  
### アイコンカラーとサイズ  
BottomNavigationBarItemで記述したようにcolor引数にColorを指定することでアイコンの色を変更することができ、sizeにdouble値を指定することでアイコンを大きさを指定することができる。  
## ListViewについて  
`ListView`はリストを表示するためのウィジェットである。  
これを配置するには「Scrolling」から対象のものをドラッグ。右側のプロパティには上下左右のスペースを調整するプロパティのみが表示されるため、表示する項目などのプロパティはコーディングする必要がある。  
以下のコードはListViewを利用した_MyHomePageStateクラスの例である。  
>class _MyHomePageState extends State<MyHomePage> {  
    static var _message = 'ok.';  
    @override  
    Widget build(BuildContext context) {  
      return new Scaffold(  
        appBar: new AppBar(  
          title: new Text('App Name'),  
          ),  
        body: new Column(  
            mainAxisAlignment: MainAxisAlignment.start,  
            mainAxisSize: MainAxisSize.max,  
            crossAxisAlignment: CrossAxisAlignment.center,  
            children: <Widget>[  
              new Text(  
              _message,  
                style: new TextStyle(fontSize:32.0,  
                color: const Color(0xFF000000),  
                fontWeight: FontWeight.w100,  
                fontFamily: "Roboto"),  
              ),  
              new ListView(  
                shrinkWrap: true,  
                padding: const EdgeInsets.all(20.0),  
                children: <Widget>[  
                    new Text(  
                    "First item",  
                    style: new TextStyle(fontSize:24.0,  
                    color: const Color(0xFF000000),  
                    fontWeight: FontWeight.w200,  
                    fontFamily: "Roboto"),  
                    ),  
                    new Text(  
                    "Second item",  
                    style: new TextStyle(fontSize:24.0,  
                    color: const Color(0xFF000000),  
                    fontWeight: FontWeight.w200,  
                    fontFamily: "Roboto"),  
                    ),  
                    new Text(  
                    "Third item",  
                    style: new TextStyle(fontSize:24.0,  
                    color: const Color(0xFF000000),  
                    fontWeight: FontWeight.w200,  
                    fontFamily: "Roboto"),  
                    ),  
                ],  
              ),  
            ],  
          ),  
      );  
    }  
}  
### ListViewの仕組み  
`shrinkWrap`は追加された項目に応じて大きさの自動調整をする設定。trueにすると表示項目に応じて大きさが自動調整される。  
リストに表示される項目はchildrenに用意する。これは次にやる`ListTile`などのウィジェットのリストである。  
## ListTileで項目を用意する。  
`ListTile`はListView用に用意されている専用のウィジェットでListViewの項目となる。インスタンスの作成は以下の引数によって行っている。  
- leading  
項目の左端に表示するアイコン。Iconインスタンスで指定。  
- title  
項目に表示する内容。  
- selected  
その項目の選択状態。trueならば選択されている。  
- onTap  
クリックされた際のイベント処理。必要時のみ。  
- onLongPress  
ロングクリックされた際のイベント処理。必要時のみ。  
以下のコードはListViewを利用したコードから`static var _index = 0;の追加`、`ListViewのchildrenをTextからListTileへ変更`、`tapTileメソッドの追加`を加えたListTileの例である。
>(略)  
 static var _index = 0;  
 (略)  
 ListTile(  
    leading: const Icon(Icons.android, size:32),  
    title: const Text('first item',  
        style: TextStyle(fontSize: 28)),  
    selected: _index == 1,  
    onTap: () {  
        _index = 1;  
        tapTile();  
    },
 ),  
 ListTile(  
    leading: const Icon(Icons.favorite, size:32),  
    title: const Text('second item',  
        style: TextStyle(fontSize: 28)),  
    selected: _index == 2,  
    onTap: () {  
        _index = 2;  
        tapTile();  
    },
 ),  
 ListTile(  
    leading: const Icon(Icons.home, size:32),  
    title: const Text('third item',  
        style: TextStyle(fontSize: 28)),  
    selected: _index == 3,  
    onTap: () {  
        _index = 3;  
        tapTile();  
    },
 ),  
 (略)  
 void tapTile() {  
    setState(() {  
        _message = 'you tapped: No, $_index.';  
    });  
 }  
 ### ListTileの基本形  
 leadingではIconインスタンスを作成し設定、titleはTextを設定。選択状態を示すselectedは_indexとListTileに割り当てた番号が等しいかどうかをチェックした結果を代入している。_indexの値を操作することで特定の項目だけを選択できるようにしている。onTapは_indexの値を設定した後、tapTileメソッドを呼び出し、呼び出した先でsetStateを呼び出して表示を更新している。