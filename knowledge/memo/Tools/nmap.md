# Nmapターゲッティング
単一のIPをスキャンする
$ nmap 192.168.1.1
ホスト名のスキャン
$ www.example.com 
IPアドレス範囲指定
$ 192.168.1.1-100
CIDR表記を使用してスキャン
$ 192.168.1.0/24 
リストからスキャン
$ nmap -lR list.txt 
ランダムスキャン
$ nmap -lR "ターゲット数"

# ポートの指定
単一のポート指定
$ nmap -p 22 192.168.1.1 
ポートを範囲選択
$ namp -p 1-20 192.168.1.1 
複数のポート指定
$ nmap -p 22,80 192.168.1.1
TCPとUDPポートを複数指定してスキャン
$ nmap -p U:53, T:21-25,80 192.168.1.1
高速モード - スキャン対象ポートを100箇所まで減らす(デフォルトは1000)
$ nmap -F 192.168.1.1
すべてのポートをスキャン
$ nmap -p- 192.168.1.1

# スキャンモード
Connect スキャン
$ nmap -sT 192.168.1.1
SYN スキャン
$ nmap -sS 192.168.1.1
UDP スキャン
$ nmap -sU 192.168.1.1
No ping スキャン
$ namp -Pn 192.168.1.1
Host Discovery(ポートスキャンはしない)
$ nmap -sn 192.168.1.1
>(CIDR表記でネットワーク帯スキャン可)

# OS、サービスバージョン検出
バージョンスキャン
$ nmap -sV 192.168.1.1
バージョンスキャンの検出強度を指定
$ namp -sV -version-intensity <0-9> 192.168.1.1
OS検出
$ nmap -o 192.168.1.1
OS検出、バージョン検出
$ nmap -A 192.168.1.1

# タイミングオプション(0から５にかけて順に早くなる)
非常に遅い(職人)
$ nmap -t0 192.168.1.1
かなり遅い(ナメクジ)
$ nmap -t1 192.168.1.1
ゆっくり(亀)
$ nmap -t2 192.168.1.1
いつもの
$ nmap -t3 192.168.1.1
せっかち
$ nmap -t4 192.168.1.1
電撃
$ nmap -t5 192.168.1.1

# NSEスクリプトオプション
デフォルトスクリプト
$ nmap -sC 192.168.1.1
$ nmap -sV sC 192.168.1.1
one script
$ nmap --script=<script_name> | <script_category> | <script_dir> 192.168.1.1
>(コンマで区切れば複数のスクリプトを選択できる。)
ワイルドカードを使う
$ nmap --script=<script_name.*> 192.168.1.1
スクリプトヘルプ
$ nmap --script-help=<script_name> | <script_category> 
スクリプト検索
$ grep "ftp" /usr/share/nmap/scripts/script.db

# ファイヤーウォール/IDSの回避となりすまし
パケットの断片化
$ nmap -f 192.168.1.1
オフセットサイズの指定
$ nmap -ntu <num> 192.168.1.1
囮を使う
$ namp -D decoy_ip_a, decoy_ip_b, own_ip, decoy_ip_c 192.168.1.1
なりすまし
$ namp -S <ip_addr> 192.168.1.1


Nmapでポートスキャンを行う場合、3つの基本的なスキャンタイプがある。これらは
 TCPコネクトスキャン(-sT)
 SYN「ハーフオープン」スキャン(-sS)
 UDPスキャン(-sU)
さらに、あまり一般的ではないポートスキャンの種類がいくつかあり、そのうちのいくつかは(あまり詳しくはないが)ここでも取り上げている。以下はその例である。

 TCP Nullスキャン(-sN)
 TCP FINスキャン(-sF)
 TCP クリスマススキャン(-sX)
これらのほとんど（UDPスキャンを除く）は、非常に似た目的で使用されますが、その動作方法は各スキャンによって異なります。つまり、ほとんどの場合、最初の3つのスキャンのいずれかを使用することになるが、他のスキャンタイプが存在することを覚えておくとよいだろう。

 ### ICMP Network scanning(-sn)
ブラックボックスの割り当てで対象となるネットワークに初めて接続したとき、最初の目的はネットワーク構造の「マップ」を取得することです。言い換えれば、どのIPアドレスにアクティブなホストが含まれていて、どのIPアドレスには含まれていないかを確認することです。

これを行う一つの方法は、Nmapを使っていわゆる「ping sweep」を行うことです。これは、その名が示すとおりの方法である。Nmapは、指定されたネットワークで考えられる各IPアドレスにICMPパケットを送信する。Nmapは、指定されたネットワークの可能性のあるIPアドレスにICMPパケットを送信し、応答を受信すると、応答したIPアドレスを生存しているとマークする。後のタスクで説明するように、これは必ずしも正確ではない。しかし、ベースラインのようなものを提供することはできるので、取り上げてみる価値はある。

ping を実行するには、-sn スイッチと、ハイフン（-）または CIDR 記法で指定できる IP 範囲を組み合わせて使用します。

nmap -sn 192.168.0.1-254
または

nmap -sn 192.168.0.0/24

この-snスイッチは、Nmapにポートをスキャンしないように指示するもので、ターゲットを特定するのに、主にICMPエコーパケット(または、sudoで実行するか、rootユーザとして直接実行する場合は、ローカルネットワーク上のARPリクエスト)に依存せざるを得ない。ICMPエコー要求に加えて、-snスイッチを指定すると、nmapはターゲットのポート443にTCP SYNパケットを送信し、ターゲットのポート80にTCP ACK(rootとして実行しない場合はTCP SYN)パケットを送信する。

 NSE
Nmap Scripting Engine(NSE)は、Nmapに非常に強力な機能を追加し、その機能を大幅に拡張している。NSEスクリプトは、Luaプログラミング言語で書かれており、脆弱性のスキャンからその悪用の自動化まで、さまざまなことに使用することができる。NSEは特に偵察に役立ちますが、スクリプトライブラリがどれだけ充実しているかを覚えておくと良いでしょう。

多くのカテゴリーが用意されています。有用なカテゴリーには次のようなものがあります。

safe:ターゲットに影響を与えないもの
intrusive:安全ではないが、ターゲットに影響を与える可能性がある。
vuln:- 脆弱性のスキャン
exploit:- 脆弱性を悪用しようとする行為
auth:- 実行中のサービスの認証をバイパスしようとする（例：FTPサーバーに匿名でログインする）。
brute:実行中のサービスの認証情報をブルートフォース（総当り）で取得しようとします。
discovery：実行中のサービスにネットワークに関する詳細情報を照会しようとする（例：SNMPサーバーへの照会）。
より詳細なリストはこちらをご覧ください。

次のタスクでは、NSEとのやりとりや、これらのカテゴリのスクリプトを利用する方法を見ていきます。

特定のスクリプトを実行するには、-script=<script-name>を使用します（例：-script=http-fileupload-exploiter）。

この方法では、コンマで区切ることにより、複数のスクリプトを同時に実行することができる。例：-script=smb-enum-users,smb-enum-shares.

スクリプトの中には、引数を必要とするものがある(例えば、認証された脆弱性を悪用している場合は、認証情報)。これらは、-script-args Nmapスイッチで指定できる。例えば、http-putスクリプト(PUTメソッドを使ってファイルをアップロードするときに使用)の場合がある。このスクリプトは、ファイルをアップロードするためのURLと、ディスク上のファイルの場所という2つの引数を取る。 例えば、以下のようになります。

$ nmap -p 80 -script http-put -script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'

引数はカンマで区切られ、対応するスクリプトにはピリオドで接続されていることに注意してください（例：<script-name>.<argument>）。

スクリプトとそれに対応する引数の一覧（使用例を含む）は、こちらをご覧ください。

さて、Nmapのスクリプトの使い方はわかったが、そのスクリプトを見つける方法はまだわからない。

これには2つの方法があり、それぞれを組み合わせて使うのが理想的だ。1つ目は、(前のタスクで述べた)NmapのWebサイトのページで、すべての公式スクリプトのリストが掲載されている。2つ目は、攻撃用マシンのローカルストレージである。Nmapは、Linux上の/usr/share/nmap/scriptsにスクリプトを保存している。すべてのNSEスクリプトは、デフォルトでこのディレクトリに格納されている。Nmapは、スクリプトを指定すると、ここでスクリプトを探すことになる。

インストールされたスクリプトを検索するには、2つの方法がある。1つは、/usr/share/nmap/scripts/script.dbファイルを使用する方法。拡張子が付いているが、これは実際にはデータベースではなく、利用可能な各スクリプトのファイル名とカテゴリを含むフォーマットされたテキストファイルである。
