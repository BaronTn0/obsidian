Nmap 7.80 ( https://nmap.org )

Usage: nmap [Scan Type(s)] [Options] {target specification}

TARGET SPECIFICATION:
  ホスト名、IPアドレス、ネットワークなどを渡すことができます。
  例：scanme.nmap.org、microsoft.com/24、192.168.0.1、10.0.0～255.1～254
  -iL <inputfilename>：ホスト/ネットワークのリストからの入力
  -iR <num hosts>: ホスト/ネットワークのリストから入力します。ランダムなターゲットを選択
  --exclude <host1[,host2][,host3],...>: ホスト/ネットワークを除外します。
  --excludefile <exclude_file>: ファイルからリストを除外します。
	
HOST DISCOVERY:
  -sL: List Scan - スキャンするターゲットを単純にリストアップします。
  -sn: Ping Scan - ポートスキャンを無効にする
  -Pn: Pn: すべてのホストをオンラインとして扱う -- ホスト発見をスキップする
  -PS/PA/PU/PY[ポートリスト]: PS/PA/PU/PY[portlist]: 指定されたポートに対するTCP SYN/ACK、UDPまたはSCTPの検出
  -PE/PP/PM: PE/PP/PM: ICMP echo, timestamp, netmask request discovery probes
  -PO[プロトコルリスト]: IPプロトコルのPing
  -n/R: DNS解決を行わない/常に解決する [デフォルト: 時々]。
  --dns-servers <serv1[,serv2],...>: カスタム DNS サーバーを指定します。
  -system-dns: OSのDNSリゾルバを使用
  --traceroute 各ホストへのホップパスを追跡する
	
SCAN TECHNIQUES:
  -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon スキャン
  -sU UDPスキャン
  -sN/sF/sX: TCP Null、FIN、Xmasの各スキャン
  -scanflags <flags>: TCPスキャンフラグのカスタマイズ
  -sI <ゾンビのホスト[:probeport]>: アイドル スキャン
  -sY/sZ: SCTP INIT/COOKIE-ECHOスキャン
  -sO: IPプロトコルスキャン
  -b <FTP relay host>: FTPバウンススキャン
	
PORT SPECIFICATION AND SCAN ORDER:
  -p <ポートの範囲>を指定します。指定したポートのみをスキャン
    例: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
  --exclude-ports <port ranges>：指定したポートをスキャン対象外にする。
  -F: Fast mode - デフォルトのスキャンよりも少ない数のポートをスキャンします。
  -r: r: 連続してポートをスキャン - ランダム化しません。
  --top-ports <number>: <number>個の最も一般的なポートをスキャンします。
  --port-ratio <ratio>：<ratio>よりも多いポートをスキャンします。
	
SERVICE/VERSION DETECTION:
  -sV: 開いているポートを調査して、サービス/バージョン情報を確認します。
  --version-intensity <level>: 0（軽い）から9（すべてのプローブを試す）まで設定します。
  --version-light: 最も可能性の高いプローブに限定します（強度2）。
  --version-all: すべてのプローブを試す（強度9）。
  --version-trace: バージョンスキャンの詳細な動作を表示（デバッグ用）
	
SCRIPT SCAN:
  -sC：-script=defaultと同等です。
  -script=<Lua scripts>を指定します。<Lua scripts> は、ディレクトリ、スクリプト・ファイル、スクリプト・カテゴリーをカンマで区切ったリストです。
           ディレクトリ、スクリプト ファイル、またはスクリプト カテゴリのコンマ区切りリストです。
  -script-args=<n1=v1,[n2=v2,...]>：スクリプトに引数を与える。
  -script-args-file=filename: NSEスクリプトの引数をファイルで提供する。
  -script-trace: 送受信したすべてのデータを表示する
  -script-updatedb: スクリプトのデータベースを更新する。
  -script-help=<Lua scripts>：スクリプトに関するヘルプを表示します。
           <Lua scripts> は、script-files または script-categories をカンマで区切ったリストです。
           script-categoriesのコンマ区切りリストです。
			   
OS DETECTION:
  -O: OSの検出を有効にする
  --osscan-limit: OS の検出を有望なターゲットに限定する
  --osscan-guess: より積極的にOSを推測します。
			   
TIMING AND PERFORMANCE:
  <time>を取るオプションは、秒単位、または'ms'(ミリ秒)を追加します。
  ms」（ミリ秒）、「s」（秒）、「m」（分）、「h」（時間）のいずれかを値に追加します（例：30m）。
  -T<0-5>：タイミングテンプレートの設定（大きいほど速い）。
  --min-hostgroup/max-hostgroup <size>: 並列ホストスキャングループのサイズ
  --min-parallelism/max-parallelism <numprobes>: プローブの並列化。プローブの並列化
  --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>: プローブの往復時間を指定します。
      プローブのラウンドトリップタイムを指定します。
  --max-retries <tries>：プローブの往復時間を指定します。ポートスキャンプローブの再送回数の上限を指定します。
  --host-timeout <time>。この時間が経過するとターゲットをあきらめる
  --scan-delay/--max-scan-delay <time>：プローブ間の遅延を調整します。プローブ間の遅延を調整します。
  --min-rate <number>: 1秒間に<number>より遅くならないようにパケットを送信します。
  --max-rate <number>: 1秒間に<number>より速くないパケットを送信します。
			   
FIREWALL/IDS EVASION AND SPOOFING:
 -f; --mtu <val>: パケットをフラグメント化します (オプションで MTU を指定できます)。
  -D <decoy1,decoy2[,ME],...>: デコイでスキャンを隠蔽
  -S <IP_Address>: 送信元アドレスを偽装する。
  -e <iface>：指定されたインターフェースを使用します。指定されたインターフェイスを使用
  -g/--source-port <portnum>：指定されたポート番号を使用します。与えられたポート番号を使用
  --proxies <url1,[url2],...>：指定されたポート番号を使用します。HTTP/SOCKS4 プロキシを使って接続を中継します。
  --data <hex string>: 独自のペイロードを送信パケットに追加します。
  --data-string <string>：カスタムのペイロードを送信パケットに追加します。独自のASCII文字列を送信パケットに追加する
  --data-length <num>：送信されるパケットにランダムなデータを追加します。送信されるパケットにランダムなデータを追加する
  --ip-options <options>: 指定されたIPオプションでパケットを送信する。
  --ttl <val>: IPのtime-to-liveフィールドを設定する。
  --spoof-mac <mac address/prefix/vendor name>: MACアドレスを偽装して送信します。
  --badsum: 偽のTCP/UDP/SCTPチェックサムを持つパケットを送信する
	  
OUTPUT:
  -oN/-oX/-oS/-oG <file>: スキャン結果を通常、XML、s|<rIpt kIddi3,
     およびGrepable形式で、それぞれ与えられたファイル名に出力する。
  -oA <basename>: 3つの主要な形式で一度に出力します。
  -v: 冗長性レベルを上げる（-vv以上を使うとより効果的）
  -d: デバッグレベルを上げる (-dd 以上を使うとより効果的)
  --reason ポートが特定の状態にある理由を表示します。
  --open。開いている（または開いている可能性のある）ポートのみを表示
  --packet-trace: 送受信されたすべてのパケットを表示します。送受信されたすべてのパケットを表示
  --iflist ホストのインターフェースとルートを表示（デバッグ用）
  --append-output: 指定された出力ファイルを破壊するのではなく、追加する。
  --resume <filename>: 中断されたスキャンを再開します。中止されたスキャンを再開します。
  --stylesheet <path/URL>: XML出力をHTMLに変換するためのXSLスタイルシートです。
  --webxml: Nmap.Orgのスタイルシートを参照して、よりポータブルなXMLを作成する。
  --no-stylesheet: XSLスタイルシートを関連付けない。no-stylesheet: XSLスタイルシートとXML出力との関連付けを防ぐ。
	  
MISC:
  -6：IPv6のスキャンを有効にする
  -A: OS検出、バージョン検出、スクリプトスキャン、およびトレースルートを有効にする
  --datadir <dirname>: カスタムNmapデータファイルの場所を指定する
  -send-eth/--send-ip。生のイーサネットフレームまたはIPパケットを使って送信する。
  --privileged ユーザーが完全に特権を持っていると仮定する
  --unprivileged: unprivileged: ユーザーが生のソケット権限を持っていないと仮定します。
  -V: V: バージョン番号を表示
  -h: このヘルプの要約ページを印刷します。
	  
例を挙げてみましょう。
  nmap -v -A scanme.nmap.org
  nmap -v -sn 192.168.0.0/16 10.0.0.0/8
  nmap -v -iR 10000 -Pn -p 80
その他のオプションや例については、manページ（https://nmap.org/book/man.html）を参照してください。
