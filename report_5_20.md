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

この中で学習する際にメインでいじっていくフォルダーは**libフォルダのmain.dart**


