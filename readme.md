# 🔰Pythonを触ってみる(環境構築からHelloWorldまで)

Pythonで環境のインストールからhelloWorldまでをやってみたメモ。

- pythonのバージョンは3.6
- windows10
- vscodeを利用

## 🔰Pythonの公式サイト

- [Python](https://www.python.org/)

## 🔰Pythonの環境構築

Pythonはv2.x or v3.xで色々あるようですが、今回はv3.6を選択。

windowsのパッケージ管理ソフトchocolateyに

- Python3.6

があったのでインストール。

- choco install python

[choco - python](https://chocolatey.org/packages/python)

※chocolatey自体のインストールについては下記

[choco Installation](https://chocolatey.org/install)

chocolateを利用しない場合は公式ドキュメントの[3. Using Python on Windows](https://docs.python.org/3/using/windows.html#installing-python)をみてインストールして下さい。

なおPythonのパッケージ管理ツールpipはPython V3.4から標準インストールされているらしいので今回個別にインストール等はしません。
(実際pythonをインストールしたディレクトリのscriptsフォルダの中にpip.exeが入ってる)

python2.x系をインストールする場合は下記とかかからインストールして下さい。

[choco - pip](https://chocolatey.org/packages/pip)

## 🔰VSCodeのインストール

- [Visual Studio Coce](https://code.visualstudio.com/)からダウンロードしてインストール
- [chocolatey - vscode](https://chocolatey.org/packages/VisualStudioCode)でインストール

お好きな方法でインストールして下さい。

## 🔰VSCodeの拡張機能インストール

VSCodeにPython向けの拡張機能が用意されているのでインストールする。

[vscode extension - Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)

![](image/vscode.extension.python.png)

## 🔰pylintのインストール

拡張機能をインストルしてvscodeでpyファイルをコーディングしようとすると。

![](image/vscode.pylint.notfound.png)

というメッセージが出てくるかと思います。

pylintはPythonのコーディングを採点をしてくれるパッケージで。

pythonの拡張機能をインストールした後に基本設定でpythonの所をみると、pylintを標準で利用するユーザ設定になっている様子。

![](image/vscode.lint.setting.png)

なのでpylintが入っていないと上記のようなエラーが出るのだと思われる。

なおエラメッセージの横に出ているinstall pylintボタンを押すと、pip install pylintコマンドが発行されて、pylintがインストールされる。

他のlintが使いたい場合は、適宜インストールして基本設定のパラメータを調整すれば良い。

もちろんpyファイルをコーディングする前にコマンドラインより **pip install pylint** でインストールしてもOK。

## 🔰VSCodeでHelloWorldのコーディング

ファイル -> 新規ファイル作成 (ctrl+N)からファイルを作成して下記をコーディング。

```Python
#!/usr/bin/python3.6
# -*- coding: utf-8 -*-

#HelloWorldを表示するSampleプログラム
print("Hello World!")

```

pythonをコーディングする時の注意点

- pythonは処理ブロックをインデントで記述するのでインデントを省略したり適当にやると動かなくなる。
- コメントは#以降から行末まで

### 🔰Pythonのshebang

一行目の

> `#!/usr/bin/python`

は[shebang](https://ja.wikipedia.org/wiki/%E3%82%B7%E3%83%90%E3%83%B3_(Unix))を表していて。

一行目かつ#!で始まるとshebangと認識する。

LINUXやらUNIXやらで意味するものかと思いきや、Using Python on Windowsの[3.4.2. Shebang Lines](https://docs.python.org/3/using/windows.html#shebang-lines)に

> To allow shebang lines in Python scripts to be portable between Unix and Windows, this launcher supports a number of ‘virtual’ commands to specify which interpreter to use.

と書いてありThe supported virtual commandsは

- /usr/bin/env python  
- /usr/bin/python  
- /usr/local/bin/python  
- python

と書いてある。さらに

> Any of the above virtual commands can be suffixed with an explicit version (either just the major version, or the major and minor version) - for example /usr/bin/python2.7 - which will cause that specific version to be located and used.

と記載があるのでバージョン指定もできる。

今回はPython3.6でしか動かして無いので#!/usr/bin/python3とshebangを設定。
shebangを#!/usr/bin/python3.6とかにしてもいいが、Pythonをバージョンが上がって3.6とかでなくなると動かなくなるので#!/usr/bin/python3とした。(HelloWorldだし……)

### 🔰ソースファイルのエンコーディング

2行目の

> `# -*- coding: utf-8 -*-`

[2.2.1. Source Code Encoding](https://docs.python.org/3/tutorial/interpreter.html#source-code-encoding)にあるソースコードのエンコーディング指定。

Pythonソースファイルはデフォルトでutf-8[(PEP 3120)](https://www.python.org/dev/peps/pep-3120/)だが、明示的に記載している。

余談ですがPEP263をみるとPythonのソースファイルにunicodeのBOMがついているとUFT-8だと判断するみたいです。

[PEP 263](https://www.python.org/dev/peps/pep-0263/)

> To aid with platforms such as Windows, which add Unicode BOM marks to the beginning of Unicode files, the UTF-8 signature \xef\xbb\xbf will be interpreted as 'utf-8' encoding as well (even if no magic encoding comment is given).
> If a source file uses both the UTF-8 BOM mark signature and a magic encoding comment, the only allowed encoding for the comment is 'utf-8'. Any other encoding will cause an error.

また[Issue1503789](http://bugs.python.org/issue1503789)をみるとPythonのソースコードはuft16ではコーディングできないようです。

## 🔰ファイルの保存

VSCode画面右下の赤枠の文字コードを確認。
uft-8以外の場合は赤枠の所をクリックするとエンコーディングを選択できるのでuft-8を選択

![](image/vscode.encoding.step001.png)

![](image/vscode.encoding.step002.png)

名前を付けて保存で適当な場所にソースを保存して下さい。

![](image/vscode.savefile.png)

## 🔰pylintでコード採点

せっかくなので保存したファイルをpylintで採点してみる。

pylint ソースコード

![](image/vscode.pylint.helloworld.png)

|Global evaluation|
|-----------------|
|Your code has been rated at 10.00/10 (previous run: 10.00/10, +0.00)|

VSCodeの問題画面(ctrl+shift+m)にチェック結果が常に表示されていた。
コーディングするたびに動的にチェックしている様子。
（だから前述するpyファイルをコーディングする時にpylintが入ってないってエラーが言われてそう）

## 🔰コマンドラインから実行

コマンドラインから**python プログラム名** としても実行できる。

![](image/helloworld.startCommand.step001.png)

プログラ名のみでも実行できる。

![](image/helloworld.startCommand.step002.png)

なお、上記の例だといちいちpowershellを起動して実行していますが。

VSCodeのctrl+@で統合ターミナルに画面遷移するのでそちらで実行するのが手早い感じ。

## 🔰pythonを対話モードで起動してみる

pythonとコマンド叩くと対話モードで起動する。(処理を抜けるにはexit() or Ctrl-Z）
対話式で逐次処理を実行できる。

![](image/python.interactivemode.png)

## 🔰vscodeからデバック実行

デバックからデバックの開始　もしくはデバック画面(ctrl+shift+d)のデバックの開始を押すとデバックが始まる。

![](image/helloworld.vscode.debug.step001.png)

続行（F5)で処理がデバック実行されていき。

![](image/helloworld.vscode.debug.step002.png)

最後まで実行するとデバックコンソールに **Hello World!** と表示される。

![](image/helloworld.vscode.debug.step003.png)

ちなみにvscodeではlanch.jsonというファイルを作って、高度なデバック設定をすることができるが本資料では説明しない。

[vscode - debugging](https://code.visualstudio.com/docs/editor/debugging)をみれば書いてある。

以上

## 🔰所感

処理ブロックをインデントで管理するというコード記法は最初見慣れなかったが、わりかしなれると思う。
