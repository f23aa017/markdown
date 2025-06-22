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
配置するには「Input」ジャンルから対象のものをドラッグ。右側にはフォント名、カラーパレット、Size、Weightのプロパティが表示される。  
次のコードはテキストを入力し、ボタンをクリックするとメッセージが表示される_MyHonePageStateクラスのソースコードである。（以降このコードに変更を加えて学習を進めるため、`変更点のみを追記していく`）  
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
## Checkboxについて  
二者択一の値を入力する「チェックボックス」は`Checkboxクラス`として用意されている。Checkboxではチェックの部分のみを表示するため、テキストを表示させたい場合は別途で追加する必要がある。  
配置するには「Input」ジャンルから対象のものをドラッグ。プロパティにはTop、Bottom、Left、RightのPaddingの値のみ表示される。  
以下のコードの変更点は`static final _controller = TextEditingController();からstatic var _checked = false;への変更`、`2つ目のPadding(略)がRow、Checkbox、Textへの変更`、`buttonPressed()からvoid checkChanged(bool? value){}への変更`となっている。  
>static var _checked = false;  
(略)  
  new Padding(  
    padding: EdgeInsets.all(10.0),  
    child: new Row(  
      mainAxisAlignment: MainAxisAlignment.start,  
      mainAxisSize: MainAxisSize.max,  
      crossAxisAlignment: CrossAxisAlignment.end,  
      children: <Widget>[  
        new Checkbox(key:null,  
        onChanged: checkChanged,  
        value:_cheked  
        ),  
        new Text(  
          "qWerty1",  
          style: new TextStyle(fontSize:22.0,  
            color: const Color(0xFF000000),  
            fontWeight: FontWeight.w400,  
            fontFamily: "Roboto"),  
        )  
      ]  
    ),  
  )  
(略)  
void checkChanged(bool? value){  
  setState(() {  
    _checkd = value!;  
    _message = value ? 'checked!' : 'not checked...';  
  });  
}  
### Checkboxの基本  
`value`はチェック状態を示すものでbool値で指定する。true=ON、false=OFF。`onChanged`はチェック状態が変更された際に発生するイベントの処理を指定する。今回はcheckChangedメソッド。  
メソッドでは受け取ったbool値によって_messageつまり、Textのメッセージを変更している。そしてこのメソッドのようにチェック状態の変更はプログラマが明示的に処理をする必要がある。  
## Switchについて  
Checkboxと見た目が違うだけで基本的な機能はほぼ同じものに「スイッチ」がある。  
配置するには「Input」から対象のものをドラッグ。プロパティにはテキスト関連の値が表示されるがすべて関係なく、Swich特有のプロパティは表示されない。  
以下のコードの変更点は`Checkbox(略)をSwitch(略)へ変更`のみで中身のコードも変更なしとなっている。  
>Switch(  
  value:_checked,  
  onChanged: checkChanged,  
),  
## Radioについて  
複数の項目から一つを選ぶラジオボタンもある。  
配置するには「Input」から対象のものをドラッグ。プロパティは何もなく、手作業デコーディングしていく必要がある。  
以下のコードの変更点は`static final _controller = TextEditingController();からstatic var _selected = 'A';への変更`、`二つ目のPaddingの中身がpadding:（略）のみ`、`Row、Radio、Textのセットを二つ追加`、`呼び出しメソッドをcheckChanged(String? value){略}への変更`となっている。  
>static var _selected = 'A';  
(略)  
new Padding(  
  padding: const EdgeInsets.all(24.0),  
),  
new Row(  
  mainAxisAlignment: MainAxisAlignment.start,  
  mainAxisSize: MainAxisSize.max,  
  crossAxisAlignment: CrossAxisAlignment.center,  
  children: <Widget>[  
    new Radio<String>(key:null,    
    groupValue: _selected,    
    value: 'A',  
    onChanged: checkChanged),  
    new Text(  
      "1",  
      style: new TextStyle(fontSize:21.0,  
        color: const Color(0xFF000000),  
        fontWeight: FontWeight.w400,  
        fontFamily: "Roboto"),  
      )  
  ]  
),  
new Row(  
  mainAxisAlignment: MainAxisAlignment.start,  
  mainAxisSize: MainAxisSize.max,  
  crossAxisAlignment: CrossAxisAlignment.center,  
  children: <Widget>[  
    new Radio<String>(key:null,    
    groupValue: _selected,    
    value: 'B',  
    onChanged: checkChanged),  
    new Text(  
      "2",  
      style: new TextStyle(fontSize:21.0,  
        color: const Color(0xFF000000),  
        fontWeight: FontWeight.w400,  
        fontFamily: "Roboto"),  
      )  
  ]  
),  
(略)  
void checkChanged(String? value){  
  setState(() {  
    _selected = value ?? 'nodata';  
    _message = 'select: $_selected';  
  });  
}  
### Radioの基本 
Radioではどの型も扱うことができるが、`型を決めるとすべてのRadioで同じ型をvalueとして扱う`必要がある。  
その後の`groupValue`はグループで選択された値を示す。例コードでは_selectedというString型のフィールドを用意することで、変更されたvalueの値を受け取ることができ、Radioが選択された状態に変わる。  
選択状態が変更されると、onChangedイベントが発生する。今回のcheckChangedメソッドではvalueの値がnullの場合（選択なし）「nodata」を代入し、_messageと合わせるとなっている。  
## DropdownButtonについて  
ドロップダウンボタンはクリックするとメニューが現れ、そこから項目を選ぶとそれが表示されるウィジェットである。  
配置するには「Material 2」から対象のものをドラッグ。右側のプロパティにはテキストの表示に関するプロパティが表示されるが、メニューに表示される項目などの設定は用意されていない。  
以下のコードの変更点は`static final _controller = TextEditingController();からstatic var _selected = 'One';への変更`、`二つ目のPaddingの中身がpadding:（略）のみ`、`DropdownButton<String>()の追加`、`呼び出しメソッドをvoid popupSelected(String? value){略}`となっている。  
>static var _selected = 'One';  
(略)  
new Padding(  
  padding: const EdgeInsets.all(24.0),  
),  
(略)  
new DropdownButton<String>(  
  onChanged: popupSelected,  
  value: _selected,  
  style: new TextStyle(fontSize:31.0,  
    color: const Color(0xFF202020),  
    fontWeight: FontWeight.w500,  
    fontFamily: "Roboto"),  
  items: <DropdownMenuItem<String>>[  
    const DropdownMenuItem<String>(value: "One",  
      child: const Text("One")),  
    const DropdownMenuItem<String>(value: "Two",  
      child: const Text("Two")),  
    const DropdownMenuItem<String>(value: "Three",  
      child: const Text("Three")),  
  ],  
),  
(略)  
void popupSelected(String? value) {  
  setState(() {
    _selected = value ?? 'not selected...';  
    _message = 'select: $_selected';  
  });  
}  
### DropdownButtonの基本  
DropdownButtonではどの型も扱うことができるが、`型を決めると同じ型をvalueとして扱う`必要がある。onChangedは、値が変更された時のイベント処理、valueは選択された値、itemsには、表示する項目の情報をまとめておく。  
### DropdownMenuItemについて  
メニュー項目は、`DropdownMenuItem`というクラスのインスタンスとして作成します。このインスタンスの配列（リスト）を作成し、itemsに設定する。また、itemsに用意するメニュー項目の情報も「型」が重要になり、引数のvalueでは「指定された型」でDropdownMenuItemの値を指定する。childではこのメニュー項目内に組み込まれるウィジェットを指定する。通常はTextを使い、メニュー項目に表示されるテキストを設定する。  
## PopupMenuButtonについて  
ドロップダウンボタンと似たようなものに「PopupButton」があり、これはポップアップメニューを呼び出すボタンである。  
配置するには「Material 2」から対象のものをドラッグ。  
以下のコードの変更点は`new DropdownButton<String>(略)を以下のコードに書き換え`となっている。  
>Align(alignment: Alignment.centerRight,  
  child: new PopupMenuButton(  
    onSelected: (String value)=> popupSelected(value),  
    itemBuilder: (BuildContext context) =>  
    <PopupMenuEntry<String>>[  
      const PopupMenuItem( child: const Text("One"),  
        value: "One",),  
      const PopupMenuItem( child: const Text("Two"),  
        value: "Two",),  
      const PopupMenuItem( child: const Text("Three"),  
        value: "Three",),  
    ],  
  ),  
),  
### PopupMenuEntryとPopupMenuItem  
ここでは`itemBuilder`にメニューの項目がまとめられており、形としては`BuildContext`というクラスのインスタンスを引数として渡す形で`PopupMenuEntry`のリストを用意している。BuildContextはウィジェット類のベースとなっているクラスで、用意したリストのPopupMenuEntryには`PopupMenuItem`というPopupMenuEntryのサブクラスを使っている。PopupMenuItemの形は引数のvalueではPopupMenuItemの値を指定する。childではこのメニュー項目内に組み込まれるウィジェットを指定する。通常はTextを使い、メニュー項目に表示されるテキストを設定する。  
### Alignについて  
`Align`はウィジェットの中に組み込んで配置するウィジェットの位置揃えを調整するコンテナである。  
alignmentには、`Alignment`というクラスを指定する。このクラスの中に主な位置揃えの値がまとめられているので、それを値として指定すれば左右中央の好みの位置にウィジェットを配置することができる。  
## Slider  
スライダーは数値をアナログ的に入力するのに用いらられるウィジェットで、ドラッグして動かすノブがあり、それを左右（上下）にスライドして値を設定するものである。  
配置するには「Input」から対象のものをドラッグ。右側のプロパティには上下左右の余白を指定するプロパティのみが表示されるが独自のプロパティは表示できないためコーディングする必要がある。  
以下のコードの変更点は`static final _controller = TextEditingController();からstatic var _value = 0.0;への変更`、`二つ目のPaddingの中身がpadding:（略）のみ`、`Slider()の追加`、`呼び出しメソッドをvoid sliderChanged(double value){略}`となっている。  
>static var _value = 0.0;  
(略)  
new Padding(  
  padding: const EdgeInsets.all(24.0),  
),  
new Slider(  
  onChanged: sliderChanged,  
  min: 0.0,  
  max: 100.0,  
  divisions: 20,  
  value:_value,  
),  
(略)  
void sliderChanged(double value) {  
  setState(() {  
    _value = value.floorToDouble();  
    _message = 'set value: $_value';  
  });  
}  
### Sliderの基本  
Sliderには多くのプロパティがあるが一般的に利用されるプロパティは以下のものである。  
- onChanged  
変更時のイベント処理。ドラッグ中、値が変わるたびに呼び出される  
- min  
最小値  
- max  
最大値  
- divisions  
分割数。min0,max10,dibisions10ならば1ずつ値が選択される。省略すると実数のまま滑らかに値が変化していく
- value  
現在選択されている値  
divisionsは実数で値を取り出し利用する場合は必要なく、整数の値だけを取り出す場合に用いられる。しかしdivisionsを指定してもvalueはdoubleである。  
sliderChangedメソッドではvalueをfloorToDoubleで整数か（値はdouble）して_valueに代入している。