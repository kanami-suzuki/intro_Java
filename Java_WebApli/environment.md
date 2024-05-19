## Macでの環境構築

### JDK
- Java Development Kitの略
- Javaのプログラムを作る(動かす)時に必要な、あると便利なツールを一つにまとめたパッケージ。
- Eclipse Temurin JDKを使用する
1. [https://adoptium.net/](https://adoptium.net/)から最新のバージョンをダウンロード
2. パッケージファイルがダウンロードフォルダにあることを確認し、ファイルをダブルクリック
3. インストーラーを特にいじらずにインストールを完了させる
4. 問題なくインストールされているか確認するために、ターミナルで「javac -version」または「java -version」とコマンドを入力する。バージョンが表示されたらOK
5. 環境変数であるJAVA_HOMEの設定をする。今回は講座に出てきた通りに設定する
  - 環境変数：コンピュータの環境に関する情報を格納する変数。プログラムが動作する環境に情報を提供する。とりあえず利便性をよくする変数
  - JAVA_HOME：他のアプリがJavaを使うためにインストールしたJDKのフォルダをすぐに特定できるようにする設定
```
//ターミナルで入力
echo export JAVA_HOME=`/usr/libexec/java_home` >> ~/.zshenv
source ~/.zshenv

//入力後に確認のコマンドを入力
echo $JAVA_HOME

//問題なければjdkがインストールされているフォルダが表示される
```

### Eclipse
- アメリカのIBM社が開発したオープンソースの統合開発環境(IDEのこと)。主にJavaの開発に使用されるが、プラグインを利用することでJavaScriptやPHP、Rubyなどの言語を用いた開発環境でも使用可能
  - 統合開発環境：開発に必要な便利なツールを統合した環境のこと
1. [https://willbrains.jp/](https://willbrains.jp/)から最新版をクリック
2. 対象OSのJAVAのダウンロードボタンをクリックしてダウンロード
3. 手順に従ってインストール
4. エラーが出て開かない場合は、finderのapp画面からEclipseを右クリック→開くでアプリケーションを開く。この時にも警告が出るが、特に問題はない
5. また、jdkの場所に関するエラーが出た場合は、finderのapp画面からEclipseを右クリック→「パッケージの中身を表示」→「Contents」フォルダの中の「Info.plist」ファイルをエディタで開く
6. 「Info.plist」ファイルの下の方にJava_Homeが記述されている部分があるので、そこに下記のコードを追記し、保存してファイルを閉じてからもう一度起動する
```
<array>

//ここから
<string>-vm</string>
<string>/Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home</string>
//ここまで

<string>-keyring</string>
<string>~/.eclipse_keyring</string>
</array>
```
7. アプリが開くとワークスペースのディレクトリ選択画面が開く。デフォルトではeclipseをインストールしたフォルダの中になっている。そのままで起動しても問題ない。ドキュメントを選ぶ画面は毎回表示されるので、表示させたくない時は下の「この選択をデフォルトとして〜」にチェックを入れ、「起動」をおす