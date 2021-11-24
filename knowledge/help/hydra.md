Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - 軍隊やシークレットサービスの組織、または違法な目的で使用しないでください（これは拘束力がありません、これらの***はとにかく法律や倫理を無視します）。

Syntax: hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e nsr] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-f] [-s PORT] [-x MIN:MAX:CHARSET] [-c TIME] [-ISOuvVd46] [-m MODULE_OPT] [service://server[:PORT][/OPT]]

Options:
  -L LOGIN または -L FILE LOGIN 名でログインするか、FILE から複数のログイン名を読み込む。
  -P PASSまたは-P FILE PASSを試すか、複数のパスワードをFILEから読み込む。
  -L/Pオプションの代わりに、コロンで区切られた "login:pass "形式のファイルを使用する。
  -M FILE 攻撃するサーバのリスト（1行に1エントリ）、':'でポートを指定します。
  -t TASKS run TASKS ターゲットごとの並列接続数 (デフォルト: 16)
  -U サービスモジュールの使用法の詳細
  -m モジュールに固有の OPT オプション、詳細は -U 出力を参照
  -h その他のコマンド ライン オプション (完全なヘルプ)
  server ターゲットを指定します。DNS、IP、192.168.0.0/24 のいずれか（-M オプションとの組み合わせ）。
  service クラックするサービス（サポートされているプロトコルについては後述）
  OPT 一部のサービスモジュールでは、追加入力をサポートしています（-Uでモジュールのヘルプが表示されます）。
  
Supported services: adam6500 asterisk cisco cisco-enable cvs firebird ftp[s] http[s]-{head|get|post} http[s]-{get|post}-form http-proxy http-proxy-urlenum icq imap[s] irc ldap2[s] ldap3[-{cram|digest}md5][s] memcached mongodb mssql mysql nntp oracle-listener oracle-sid pcanywhere pcnfs pop3[s] postgres radmin2 rdp redis rexec rlogin rpcap rsh rtsp s7-300 sip smb smtp[s] smtp-enum snmp socks5 ssh sshkey svn teamspeak telnet[s] vmauthd vnc xmpp

Hydraは、有効なログイン/パスワードのペアを推測/クラックするツールです。
AGPL v3.0でライセンスされています。最新バージョンは常に以下の場所で入手可能です。
https://github.com/vanhauser-thc/thc-hydra
軍やシークレットサービスの組織での使用や、違法な目的での使用はご遠慮ください。
違法な目的で使用しないでください。(これは希望であり、拘束力はありません-そのような人々の多くは、法律や倫理を気にせず
これは希望であり、拘束力はありません。）

Example:  hydra -l user -P passlist.txt ftp://192.168.0.1
