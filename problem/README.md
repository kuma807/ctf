# 目次

[crackme-py](#crackme-py)  
[Magikarp Ground Mission](#magikarp-ground-mission)  
[tunn3l v1s10n](#tunn3l-v1s10n)  
[Easy Peasy](#easy-peasy)  
[Cookies](#cookies)  
[Insp3ct0r](#insp3ct0r)  
[Scavenger Hunt](#scavenger-hunt)  
[Glory of the Garden](#glory-of-the-garden)  
[Lets Warm Up](#lets-warm-up)  
[vault-door-training](#vault-door-training)  
[Warmed Up](#warmed-up)  
[2Warm](#2warm)  
[PW Crack 1](#pw-crack-1)  
[Wireshark doo dooo do doo...](#wireshark-doo-dooo-do-doo...)  
[Who are you?](#who-are-you?)  
[where are the robots](#where-are-the-robots)  
[dont-use-client-side](#dont-use-client-side)  
[logon](#logon)  
[Inspect HTML](#inspect-html)  
[login](#login)  
[Includes](#includes)  
[Local Authority](#local-authority)  
[Some Assembly Required 1](#some-assembly-required-1)  
[picobrowser](#picobrowser)  
[Power Cookie](#power-cookie)  
[Forbidden Paths](#forbidden-paths)  
[It is my Birthday](#it-is-my-birthday)  
[Client-side-again](#client-side-again)  
[Irish-Name-Repo 1](#irish-name-repo-1)  
[Secrets](#secrets)  
[Roboto Sans](#roboto-sans)  
[caas](#caas)  
[SQLiLite](#sqlilite)  
[findme](#findme)  
[MatchTheRegex](#matchtheregex)  
[Irish-Name-Repo 2](#irish-name-repo-2)  
[Web Gauntlet](#web-gauntlet)  
[Irish-Name-Repo 3](#irish-name-repo-3)  
[SOAP](#soap)  
[A little something to get you started](#a-little-something-to-get-you-started)  
[Some Assembly Required 2](#some-assembly-required-2)  
[Sanity Check Round 44](#sanity-check-round-44)  
[kaiser](#kaiser)  
[Sleepy](#sleepy)  
[More SQLi](#more-sqli)  
[Filters](#filters)  
[Find the flag](#find-the-flag)  
[Ultimate spider man](#ultimate-spider-man)  
[eH lvl1](#eh-lvl1)  
[eH lvl2](#eh-lvl2)  
[Operation Ultra](#operation-ultra)  
[Warmup_rev](#warmup_rev)  
[Ocean_Enigma](#ocean_enigma)  
[Participant Survey](#participant-survey)  
[Feedback](#feedback)  
[Welcome to ShaktiCTF'24](#welcome-to-shaktictf'24)

# 解いた問題

# crackme-py

site: picoCTF  
contest: picoCTF 2021  
category: Reverse Engineering

## 解き方

crackme.py を読んで内容を理解する。flag を出力する関数が呼び出されていないためそれを呼び出すようにコードを変える。

## 学び

特になし

# Magikarp Ground Mission

site: picoCTF  
contest: picoCTF 2021  
category: General Skills

## 解き方

cd,ls,cat などの linux コマンドを使ってマシン内にある flag を探す。

## 学び

特になし

# tunn3l v1s10n

site: picoCTF  
contest: picoCTF 2021  
category: Forensics

## 解き方

1.まず与えられらバイナリファイルが何のファイルなのかを特定するために exiftool を使うとファイルの形式が BMP であることがわかる。あとはファイルの先頭(マジックナンバー)から BMP であることも特定できる。

2.Hex エディタでデータを見て、BMP の形式で間違っているところを探すとオフセットと情報ヘッダサイズが間違っているので修正する。

3.すると画像が表示されるが必要な情報が載ってない。やけに横に長い画像のため画像の height を Hex エディタで編集すると flag が見つかる。

## 学び

- file コマンドでバイナリファイルがどんなファイルだかわかるらしい（今回はデータが壊れてたのでダメだった）
- exiftool で色々ファイルの情報が見れる
- ファイル復元するときはファイルタイプのデータ形式を wiki で調べて壊れてないか確認するの典型ぽいかも？
- 画像の height,weidth を変えて追加情報探すのも典型かも？
- photopea ていうサイト使うと壊れた写真そのまま開けたらしい
- マジックナンバーの存在を知った

# Easy Peasy

site: picoCTF  
contest: picoCTF 2021  
category: Cryptography

## 解き方

1.コードを読むと暗号化の key の長さが 50000 しかなくて、すべて使い切るとまた最初から使い回す方式になっている。そのため 50000 文字を使い切って適当な文字列を再度送ることで flag を暗号化した key を特定できる、この key を使って暗号化された flag を解読すれば良い。

2.とりあえず 50000 文字使い切って"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"をサーバーに送る。サーバーから帰ってきた暗号を元にローカルで key を復元。復元した key を使って flag を復号した。

## 学び

- key を使い回すのは危ない
- python で 16 進数の文字列扱うのむずい
- 今回は 50000 文字使い切るために手作業で文字を送ったけど python を使って次のように送れる。また python だと"aaaaaaaaaaaaa"じゃなくて\x00 を送れるため key を復号する必要がなくなる。

```bash
python3 -c "print('\x00'*(50000-32)+'\n'+'\x00'*32)" | nc mercury.picoctf.net 36981
```

# Cookies

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

問題の名前からして cookie が怪しいので見に行くと name っていうものが保存されている。この name の value がデフォルトだと-1 になってるのでそれを適当に 1 に変更するとサイトに表示される内容が変わる。value を 1 から 18 まで試すと 18 で flag が出てくる。

## 学び

- cookie は変えられるため cookie だけをみてユーザー承認などをすると良くない

# Insp3ct0r

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

サイトを開いて管理者ツールを開くだけ html,css,js に flag が隠されている

## 学び

特になし

# Scavenger Hunt

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

サイトを開いて管理者ツールを開くと html,css,js に flag と次のフラグのヒントが隠されている。
`How can I keep Google from indexing my website?`  
このヒントから/robots.txt にアクセスすると flag と次のヒントが見つかる。
`I think this is an apache server... can you Access the next flag?`
apache サーバーなので/.htaccess,/.htpasswd,/server-status にアクセスすると/.htaccess に flag とヒントがある。
`I love making websites on my Mac, I can Store a lot of information there.`
mac なので/.DS_Store にアクセスすると最後の flag が見つかる

## 学び

- robots.txt は外部からアクセスすることが想定されていてクローラーとかが index 化して良いページの指定などをしている。
- /.htaccess は url リダイレクト、アクセス制限、キャッシュ制御などさまざまな設定を行うファイル。重要な設定に関わるファイルでセキュリティ的に外部から見れてはいけない。/.htaccess ないで外部から見れないように設定ができる。
- /.DS_Store は macOS の Finder によって作成される隠しファイルで、フォルダ内のファイルの表示方法(アイコンの位置、選択されたビューの種類、ウィンドウのサイズ、背景色や背景画像など）を記録します。/.DS_Store は macos 以外では不要なファイルで web サーバーなどにアップロードしてしまうと デレクトリ構造などがバレてしまう。git で/.DS_Store は含まないように気をつけよう。

# Glory of the Garden

site: picoCTF  
contest: picoCTF 2019  
category: Forensics

## 解き方

exiftool で追加情報を見る。特に何もなし
binwalk でなかにファイルないか確認。何もなし
strings でファイル内に文字ないか確認 -> Here is a flag "picoCTF{more_than_m33ts_the_3y3eBdBd2cc}"

## 学び

特になし

# Lets Warm Up

site: picoCTF  
contest: picoCTF 2019  
category: General Skills

## 解き方

x70 を ascii に変換するだけ
https://www.rapidtables.com/convert/number/hex-to-ascii.htmlで変換

##　学び
答えは picoCTF{}の中に入れよう

# vault-door-training

site: picoCTF  
contest: picoCTF 2019  
category: Reverse Engineering

## 解き方

コードの中に flag が書いてある

## 学び

特になし

# Warmed Up

site: picoCTF  
contest: picoCTF 2019  
category: General Skills

## 解き方

16 進数を 10 進数に変換する

## 学び

特になし

# 2Warm

site: picoCTF  
contest: picoCTF 2019  
category: General Skills

## 解き方

10 進数を 2 進数に変換するだけ

## 学び

特になし

# PW Crack 1

site: picoCTF  
contest: Beginner picoMini 2022  
category: General Skills

## 解き方

python コードを読んで入力するパスワードを探す

## 学び

特になし

# Wireshark doo dooo do doo...

site: picoCTF  
contest: picoCTF 2021  
category: Forensics

## 解き方

wireshark でファイルを開いて通信を解読していく。tcp 通信はコネクション型プロトコルで通信のコネクションを確立する役割を持つ、そのため実際のデータの通信では http 通信が利用される。通信内容を見るために wireshark の info 絞り込みで http リクエストのみを見ると Gur synt vf cvpbPGS{c33xno00_1_f33_h_qrnqorrs}という文字列が見るかる。これをシーザー暗号解読機にかけると flag が出てくる。

## 学び

- tcp 通信はコネクションのためであり、実際の内容を通信してない
- wireshark で info 絞り込みをすると http 通信を絞り込みやすい
- シーザー暗号（cvpbPGS{c33xno00_1_f33_h_qrnqorrs}みたいにローマ字をずらすやつ）を解読するのに http://www.net.c.dendai.ac.jp/crypto/caesar2.html?# が便利

# Who are you?

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

curl を使って使ってるウェブブラウザ、日付、追跡されない設定、どのサイト経由で来たか、どの国からアクセスしてるか、どの言語を使っているかなどを指定できる。

## 学び

- curl を使うと http ヘッダを操作できる

# where are the robots

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

robots.txt にアクセスして disallow になってるページに行くと flag がある

## 学び

- robots.txt とは、収集されたくないコンテンツをクロールされないように制御するファイル
- robots.txt は User-Agent、Disallow、Sitemap を指定する。User-Agent は、どのクローラーの動きを制御するかを指定、Disallow は、クローラーのアクセスを制御するファイルを指定、Sitemap は、sitemap.xml の場所をクローラーに伝える。
- Sitemap は Web サイト内の各ページ情報（URL や優先度、最終更新日、更新頻度などの情報）を検索エンジン向けに記載した XML 形式のファイル

# dont-use-client-side

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

js を読むだけ

## 学び

特になし

# logon

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

適当な username でログインを試すと成功して flag っていうページに飛ぶ。ただ権限の問題か flag が表示されない。cookie を見ると admin という項目と username の項目があるので admin=True,username=Joe にすると flag が見れる。  
username は変える必要がなかったらしく、admin=True だけで flag は表示される。

## 学び

- cookie の情報だけで処理を変えるのは良くない

# Inspect HTML

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

html を見るだけ

## 学び

特になし

# login

site: picoCTF  
contest: picoMini by redpwn  
category: Web Exploitation

## 解き方

js を見ると base64 エンコードされたパスワードが見つかからそれをデコードする

## 学び

- base64 とはすべてのデータをアルファベット(a~z, A~z)と数字(0~9)、一部の記号(+,/)の 64 文字で表すエンコード方式

# Includes

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

js,css を見るだけ

## 学び

特になし

# Local Authority

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

js を読んでログインパスワードをゲットする

## 学び

特になし

# Some Assembly Required 1

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

js 解読してたけど wasm ファイルに flag 書いてあった。

## 学び

- すぐ js の解読開始するのではなく全体を一回見るの大切かも

# picobrowser

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

curl でアクセスしてるブラウザを picobrowser にすると flag が見れる。

## 学び

- curl でブラウザ変更するの典型ぽい

# Power Cookie

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

cookie を変更するだけ

## 学び

特になし

# Forbidden Paths

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

現在のパスと行きたい場所のパスがわかるので相対パスを入力する

## 学び

- 特になし

# It is my Birthday

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

md5 で衝突するデータを見つけてきたそれを pdf に保存する
https://www.softel.co.jp/blogs/tech/archives/7212

## 学び

- md5 とは、任意の長さの原文を元に 128 ビットの値を生成するハッシュ関数（要約関数）の一つ。生成された値はハッシュ値（MD5 ハッシュ）と呼ばれる。
- md5 はハッシュの衝突する値が見つけられるようになって最近は SHA-256 が代わりに使われる

# Client-side-again

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

html に書いてある配列を元に flag を予想した。正規手順としては js を実際に動かして if 文で比較されてる文字を見るのがいいかも

## 学び

- html,js を解析するときは実際に動かそう

# Irish-Name-Repo 1

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

サイトの support ページを見ると sql が実行されてるのがわかるので、sql インジェクションをする
password に ' OR '1'='1 を入れるか、username に ' or 1 == 1 -- を入れるといける

## 学び

- sql に -- を入れるとその行のそれ以降の文字がコメントアウトされる
- sql の and は or より早く確認される

# Secrets

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

開発者モードで source を見ると css が secret っていうファイルにあるため/secret/にアクセスするとページが現れる。移行繰り返しで flag が見つかる。

## 学び

- http://saturn.picoctf.net:62050/secret と http://saturn.picoctf.net:62050/secret/ では大きな違いがある。この形式の URL は、secret という名前のディレクトリにアクセスしようとしていることを示しています。この場合、ウェブサーバーは通常、そのディレクトリ内のデフォルトのインデックスファイル（例: index.html や index.php など）を返します。

# Roboto Sans

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

robots.txt に行くと base64 の文字があるのでデコードするとアクセスできそうなデレクトリが見つかる。アクセスすると flag

## 学び

- base64 とは、64 進数を意味する言葉で、すべてのデータをアルファベット(a~z, A~z)と数字(0~9)、一部の記号(+,/)の 64 文字で表すエンコード方式です。またパディングのために=が末尾に使用されることがある。

# caas

site: picoCTF  
contest: picoMini by redpwn  
category: Web Exploitation

## 解き方

与えられた js のコードを見るとコマンドを実行してるのでコマンドインジェクションをする。cowsay hi & ls, cowsay hi & cat falg.txt の二つのコマンドを実行して flag を取得した

## 学び

- コマンドインジェクションで&とか;が使える
- ユーザーの入力を元にコマンド実行するの危険かも

# SQLiLite

site: picoCTF  
contest: picoCTF 2022  
category: Web Exploitation

## 解き方

sql インジェクションをするとログインできる。' OR '1'='1

## 学び

特になし

# findme

site: picoCTF  
contest: picoCTF 2023  
category: Web Exploitation

## 解き方

サイトに redirected されたという情報があるので curl でアクセスしてリダイレクトがどうなてるか調べる。するとリダイレクトする前のページの id に flag が含まれてる。
burp を使うと簡単に redirect の経路とかがわかる。

## 学び

- burp が神と話題
- 通信で何が行われてるか確認した方がいい

# MatchTheRegex

site: picoCTF  
contest: picoCTF 2023  
category: Web Exploitation

## 解き方

js に正規表現があるのでそれにマッチする文字を送信すると flag がもらえる。

## 学び

- ^は正規表現の始まりを表し、.は任意の文字を表す

# Irish-Name-Repo 2

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

' OR '1' = '1 だと sql インジェクションがバレるので admin' --をやるとうまく行く。

## 学び

- 色々な sql インジェクションを学んで対策をすり抜けるのが大事

# Web Gauntlet

site: picoCTF  
contest: picoCTF 2020 Mini-Competition  
category: Web Exploitation

## 解き方

さまざまな sql インジェクションをする。

## 学び

- ;がそこで sql 文を修了できて良い
- union を使って複数クエリの結合や||を使った文字列の結合が便利

# Irish-Name-Repo 3

site: picoCTF  
contest: picoCTF 2019  
category: Web Exploitation

## 解き方

burp で送ったリクエストを見ると debug っていう項目があるので debug=1 にして送り直す。このとき変更したいリクエストを右クリックして send to repeater を選択、左上から repeater を選択するとリクエストを編集・送信できるようになる。編集したリクエストを送ると rot13 で送った文字が変更されてるので、rot13 された' or '1'='1 を送ると flag がもらえる

## 学び

- burp をうまく使うとリクエストの編集ができる。burp を常に使って送ったリクエストの確認をしよう
- send to repeater もリクエストを編集できて便利
- intersept = true にすると送る前にリクエストを編集できる

# SOAP

site: picoCTF  
contest: picoCTF 2023  
category: Web Exploitation

## 解き方

送信されてる xml を見て xml インジェクションを行う。外部ファイルを参照するために<!DOCTYPE foo [

<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>を書いて&xxe;でアクセスする。

## 学び

- xml インジェクションについて学んだ
- xml は外部のファイルの参照とかができる、json みたいなデータ形式

# A little something to get you started

## 解き方

hacker101  
network の通信を見ると画像があるのでそれを開くと flag

## 学び

- 特になし

# Some Assembly Required 2

site: picoCTF  
contest: picoCTF 2021  
category: Web Exploitation

## 解き方

chatgpt でコードの意味を調べていくと strcmp が flag と入力を比較して、ascii でのズレを出力しているぽい。strcmp 関数を console から使って strcmp 関数の出力を見た。wasm ファイルにある flag ぽい文字を入力に入れると 8 という数字が出てくる。
8 ずれていることがわかるので ascii で"xakgK\5cNs9=8:9l1?im8i<89?00>88k09=nj9kimnu\00\00"の 8 ずらしてみると x が p になって flag ぽい。以降の数字を-8,+8,-8,+8 ってやると picoCTF{まで綺麗に出てくる。それ以降が綺麗に出ないのでこの法則は間違ってそう。wasm のコード内で"8"で検索をかけると近くに xor っていう文字があるので"xakgK\5cNs9=8:9l1?im8i<89?00>88k09=nj9kimnu\00\00"に 8 を xor してみると flag が出てくる。

### 別解

https://github.com/Dvd848/CTFs/blob/master/2021_picoCTF/Some_Assembly_Required_2.md  
おそらく想定解だけどめっちゃむずいし学びが多い。  
js を読むと wasm を利用してることがわかる。wasm ファイルがどこにあるかは WebAssembly.instantiate("wasm の中身")という構造のため WebAssembly.instantiate 付近を見ればいい。  
以下のコードは chatgpt に読みやすくしてもらった js からの抜粋。

```js
let response = await fetch("./aD8SvhyVkb");
let wasm = await WebAssembly.instantiate(await response.arrayBuffer());
```

今回は aD8SvhyVkb というところにファイルがあるため http://mercury.picoctf.net:7319/aD8SvhyVkb にアクセすることでファイルを取得できる。ダウンロードした wasm ファイルは次のコマンドで人間にも読める wat に変換することができる。

```bash
wasm2wat aD8SvhyVkb.wasm -o aD8SvhyVkb.wat
```

今回の問題だと/wasm/3e1a8b4a にあるファイルが変換後の wat になっている（なぜ？）

> [!TIP]
> サーバーからは wasm が送られてくるがブラウザがディスアセンブリして wat に変換している。開発者モードの network を見ればサーバーから wasm が送られてきていることがわかる。

wat だと読みづらいので疑似コードに変換する（じゃあなんでさっき wat にした？最初から疑似コードにすればいいじゃん）

```bash
wasm-decompile aD8SvhyVkb.wasm -o aD8SvhyVkb.dcmp
```

こうするとかなり読みやすくなって 8 の xor が使われてることとかがわかって flag が導ける。

## 学び

- 難読化されたコードを chatgpt に入れるといい感じに読みやすくしてくれる
- こんな大変なことしなくても"xakgK\5cNs9=8:9l1?im8i<89?00>88k09=nj9kimnu\00\00"を cyberchef に入れて magic の intensive mode を使うと解ける
- サイトで使われてるファイルは hppts://mercury.picoctf.net:7319/ファイル名　みたいな感じで取得・ダウンロードできる。開発者モードの network からもサーバーから送られてるファイルの確認・ダウンロードができる。
- wasm はより読みやすい wat、c 言語、疑似コード に変換できる
- wasm は高速な実行を目的としたバイナリ命令形式のプログラミング言語、wat は wasm のテキスト形式版

# Sanity Check Round 44

site: imaginaryCTF  
contest: imaginaryCTF Round 44  
category: General Skills

## 解き方

問題文に flag が書いてある

## 学び

特になし

# kaiser

site: imaginaryCTF  
contest: imaginaryCTF Round 44  
category: Cryptography

## 解き方

シーザー暗号の key=7。なぜ 7 なのかは不明だし復元した flag も意味のない文字列で不服

## 学び

特になし

# Sleepy

site: imaginaryCTF  
contest: imaginaryCTF Round 44  
category: Reverse Engineering

## 解き方

コードを読むと sleep が無駄に入ってるので削除すると高速に flag がもとまる。

## 学び

特になし

# More SQLi

site: picoCTF  
contest: picoCTF 2023  
category: Web Exploitation

## 解き方

ログイン画面が表示されて適当に入力すると sql が表示される。

```
username: a
password: a
SQL query: SELECT id FROM users WHERE password = 'a' AND username = 'a'
```

今回の sql は password が先にあるため password に ' OR '1' = '1'; と入力するとログインできる。  
次は検索画面バーが表示されるのでどんなテーブルがあるかの情報を得るために次の sql を使う。sql の出力が 3 列じゃないと表示されないので NULL を使って 3 列にする。

```
' UNION SELECT group_concat(sql), NULL, NULL FROM sqlite_master;
```

この結果から more_table っていう table に flag という列があるためそれを取得する。

```
' UNION SELECT flag, NULL, NULL FROM more_table;
```

## 学び

- sql インジェクションでテーブルの情報を取得できる
- 列の数が合わなかったら NULL で埋めれば良い
- https://blog.hamayanhamayan.com/entry/2021/12/05/115923 このサイトに sql インジェクションの例がいっぱい載ってて良い

# Filters

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Web Exploitation

## 解き方

画面にアクセスすると次のことが画面に表示される。

```
<?php
highlight_file(__FILE__);
$command = $_GET['command'] ?? '';

if($command === '') {
    die("Please provide a command\n");
}

function filter($command) {
    if(preg_match('/(`|\.|\$|\/|a|c|s|require|include)/i', $command)) {
        return false;
    }
    return true;
}

if(filter($command)) {
    eval($command);
    echo "Command executed";
} else {
    echo "Restricted characters have been used";
}
echo "\n";
?>
Please provide a command
```

このコードを chatgpt に入れると url パラメーターの command を eval で実行してることがわかる。eval を実行する前に filter で'/(`|\.|\$|\/|a|c|s|require|include)/i' が command に含まれていないか確認し、含まれている場合は command が実行されない。今回は使えない文字を生成するために文字同士の xor を利用した。

### ダメだったパターン

- system('cat flag.txt');を示す'101000MM100M0100L000MMM' ^ 'BIBDU]ejRQDmV]QWbDHDjdv';を command として送信
- system('ls');を表す'101000MM10MMM' ^ 'BIBDU]ej]Bjdv'の送信

ダメだった理由  
'101000MM10MMM' ^ 'BIBDU]ej]Bjdv'が実行されて system('ls');ていう文字列自体は生成されるものの文字列のため実行されない。再起的に生成された文字をコマンドとして扱うわけじゃない。

### 良いパターン

- print_r(file('flag.txt'));を表す print_r(file('0100L000' ^ 'V]QWbDHD'));を送信。文字の xor が先実行されそのあと file,print_r コマンドが実行される。再起的な構造になっていない。

- print_r(('system')('cat flag.txt')) を表す print_r(("111114"^"BHBETY")("111q1411w111"^"RPEQWXPVYEIE"))を送信。まず文字の xor が実行されて print_r(('system')('cat flag.txt'))形になる。このあと('system')('cat flag.txt')は system('cat flag.txt')として実行される（php の文法ぽい)

## 学び

- php インジェクションっていうものがあるらしい
- php インジェクションで使える文字を制限されてたら文字列の xor とか色々なコマンド調べるのが良い
- 文字列の xor で作られたものは文字列でコマンドとして実行されない
- ('a' ^ 'b')('c' ^ 'd')みたいな形で('command')('引数')を作ればコマンド名も xor で作れる
- このサイトが php インジェクションまとまっててよかった https://blog.hamayanhamayan.com/entry/2021/12/18/132236

# Find the flag

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Web Exploitation

## 解き方

付属のファイルを読むとリクエストパラメータの test が os.popen(command)で実行されてる。command = f"find {test}"と定義されているため test に; cat flag.txt を入れると flag が得られる。

## 学び

特になし

# Ultimate spider man

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Web Exploitation

## 解き方

画面に表示されてる 4 つ目の商品を買えば良さそうだけどお金が足りない。他の商品を買うときの処理を burp で見ると post request ではお金足りるかの処理をローカルで行って、お金足りたら post id=3 みたいな感じで送信してる。なので burp で id=4 でリクエストを送ると商品 4 を買ったときのリスポンスが帰ってくる。
商品 4 を買った時に取得できる cookie がわかるのでそれをブラウザで設定して checkout すると flag がもらえる。

## 学び

特になし

# eH lvl1

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Cryptography

## 解き方

```
from Crypto.Util.number import*
from gmpy2 import *
from secret import e,b,hint,msg,d
p = getPrime(512)
q = getPrime(512)
n = p*q
m = bytes_to_long(msg)
h = bytes([i^b for i in hint])
print(f"h = {hex(bytes_to_long(h))}")
ct = pow(m,e,n)
de = pow(ct,d,n)
assert(m == de)
print("ct = ",ct)
print("p = ",p)
print("q = ",q)
```

h,ct,p,q が既知の値。hint が各バイトごとに b で xor されてる。バイトごとの xor のため b は 0-255 のどれかのため全探索すれば良い。

```
from Crypto.Util.number import long_to_bytes

# 与えられた16進数の文字列
h_hex = 0x6f535e1b5e1b061b0c020f0b0b10134f535e1b4852555c575e1b59424f5e1b4f535a4f1b4c5a481b4354495e5f121b0112

# 16進数をバイト列に変換
h_bytes = long_to_bytes(h_hex)

# 各バイトに3をXOR
for i in range(2 ** 10):

    try:
        result = bytes([b ^ i for b in h_bytes])
        print(result.decode())
    except:
        pass
```

全探索すると The e = 79400+(the single byte that was xored) :)という文字が得られる。これより e の値がわかり flag が復元できる。

```
temp_e = 79400
for i in range(2 ** 8):
  for j in range(20):
    e = temp_e ^ (i * (2 ** (j * 4)))
    phi_n = (p - 1) * (q - 1)
    try:
      d = pow(e, -1, phi_n)
      de = pow(ct,d,n)
      byte_length = (de.bit_length() + 7) // 8  # 整数を表現するのに必要なバイト数を計算
      byte_order = 'big'  # バイトオーダーを指定（'big'または'little'）
      bytes_value = de.to_bytes(byte_length, byte_order)
      string_value = bytes_value.decode('ascii')
      print(string_value)
    except:
      pass
```

復元すると Here is your reward 'vvrkxuqgi{r0i43m0r_f0_hu3_u3gtu3!!!}' You can ask 'Doraemon' to help you with this. Bye!!という文字が得られる。どうやらこれがヴィシュネル暗号らしく Doraemon という key を使うと flag が得られる。

## 学び

- ヴィシュネル暗号の存在を知った
- https://www.dcode.fr/vigenere-cipher が便利

# eH lvl2

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Cryptography

## 解き方

```
from Crypto.Util.number import*
from gmpy2 import *
from secret import flag,hint,p,q,n,e

m = bytes_to_long(flag)
h = [i^n for i in hint]
print(f"h = {(h)}")
ct = pow(m,e,n)
print("ct = ",ct)
print("p = ",p)
print("q = ",q)
```

h, ct, p, q が既知で n も n=p \* q で導ける。そのため hint が復元できる。The e = 46307 :)ヒントから e がわかるため ct から flag が復元できる。

## 学び

特になし

# Operation Ultra

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Reverse Engineering

## 解き方

与えられたコードでは flag に対して xor して並び替えるという暗号化を行っている。並び替えを戻して xor を再度行うと flag がもらえる。

## 学び

特になし

# Warmup_rev

site: Shakti CTF  
contest: Shakti CTF 2024  
category: Reverse Engineering

## 解き方

strings コマンドでファイルの可読文字を見ると flag が入ってる。

## 学び

- こんなことしなくても ghidra を使って binary からコードを復元するのがよかったぽい

# Ocean_Enigma

site: Shakti CTF
contest: Shakti CTF 2024
category: osint

## 解き方

画像を検索すると船の名前がわかるの wiki を見ると flag がわかる。

## 学び

特になし

# Participant Survey

site: Shakti CTF  
contest: Shakti CTF 2024  
category: General Skills

## 解き方

アンケートに答えるだけ。賞金対象者かを判別してるっぽい。

## 学び

こんな問題もあるんですね。

# Feedback

site: Shakti CTF  
contest: Shakti CTF 2024  
category: General Skills

## 解き方

コンテスのフィードバックを google フォームで送るだけ。

## 学び

特になし

# Welcome to ShaktiCTF'24

site: Shakti CTF  
contest: Shakti CTF 2024  
category: General Skills

## 解き方

discord に貼ってある画像をクリックすると flag が見れる。

## 学び

特になし
