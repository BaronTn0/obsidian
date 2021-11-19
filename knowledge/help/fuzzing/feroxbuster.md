feroxbuster 2.4.0
Ben 'epi' Risher (@epi052)
A fast, simple, recursive content discovery tool written in Rust

USAGE:
    feroxbuster [FLAGS] [OPTIONS] --url <URL>...

FLAGS:
    -f, --add-slash        各リクエストに / を付ける
        --auto-bail        過剰なエラーが発生した場合は、自動的にスキャンを停止します。
        --auto-tune        過剰なエラーが発生した場合、自動的にスキャンレートを下げます。
    -D, --dont-filter      ワイルドカードの回答を自動フィルタリングしない
    -e, --extract-links レスポンスボディ（html、javascriptなど）からリンクを抽出し、それに基づいて新しいリクエストを行う。
                           に基づいて新しいリクエストを行います。
    -h, --help ヘルプ情報を表示します。
    -k, --insecure TLS 証明書の検証を無効にします。
        --json 通常のテキストではなく、JSON形式のログを --output および --debug-log に出力します。
    -n, --no-recursion 再帰的にスキャンしない。
    -q, --quiet プログレスバーやバナーを非表示にします（tmuxのウィンドウに通知を表示する場合に有効です）。
    -A, --random-agent ランダムなユーザーエージェントを使用します。
    -r, --redirects リダイレクトを追う
        -silent URLを表示するだけ＋ログをオフにする（URLのリストを他のコマンドに渡すのに適しています）。
        --stdin STDINからURLを読み込みます。
    -V, --version バージョン情報を表示します。
    -v, --verbosity 冗長度を上げる（-vv以上を使うとより効果的です。[注意] 4 -v's はおそらく多すぎます)

OPTIONS:
       --debug-log <FILE> ログエントリを書き込むための出力ファイル (JSONエントリの場合は--jsonを使用)
    -d, --depth <RECURSION_DEPTH>
            最大再帰の深さ、深さが0の場合は無限再帰(デフォルトは4)

    -x, --extensions <FILE_EXTENSION>...          検索するファイルの拡張子（複数可）（例：-x php -x pdf js）
    -N, --filter-lines <LINES>...                 特定の行数のメッセージを除外する (例: -N 20 -N 31,30)
    -X, --filter-regex <REGEX>...
            正規表現を使ってメッセージを除外します (例: -X '^ignore me$')

        --filter-similar-to <UNWANTED_PAGE>...
            指定されたページに類似したページをフィルタリングします (例: --filter-similar-to http://site.xyz/soft404)

    -S, --filter-size <SIZE>...                   特定のサイズのメッセージを除外する(例: -S 5120 -S 4927,1970)
    -C, --filter-status <STATUS_CODE>...          ステータスコード(拒否リスト)をフィルタリングする(例：-C 200 -C 401)
    -W, --filter-words <WORDS>...                 特定の単語数のメッセージを除外する(例: -W 312 -W 91,82)
    -H, --headers <HEADER>...                     HTTP ヘッダを指定する (例: -H Header:val 'stuff: things')
    -o, --output <FILE> 結果を書き込む出力ファイル (JSON形式の場合は --json を使用)
        --parallel <PARALLEL_SCANS> (例)
            feroxbusterのインスタンスを並列に実行します(標準入力で渡されるURLごとに1つの子プロセスを実行)

    -p, --proxy <PROXY> (プロキシ)
            リクエストに使用するプロキシ (例: http(s)://host:port, socks5(h)://host:port)

    -Q, --query <QUERY>...                        URL のクエリパラメータを指定します (例: -Q token=stuff -Q secret=key)
        --rate-limit <RATE_LIMIT> ...
            ディレクトリごとに1秒あたりのリクエスト数を制限する（デフォルト：0、つまり制限なし

    -R, --replay-codes <REPLAY_CODE>...
            リプレイ・プロキシが見つかったときに送信するステータス・コード(デフォルト: --status-codesの値)

    -P, --replay-proxy <REPLAY_PROXY>...
            すべてのリクエストではなく、フィルタリングされていないリクエストのみをリプレイ・プロキシ経由で送る

        --resume-from <STATE_FILE>
            部分的に完了したスキャンを再開するためのステートファイル (例: --resume-from ferox-1606586780.state)

    -L, --scan-limit <SCAN_LIMIT> 同時スキャンの総数を制限します（デフォルト：0、つまり制限なし）
    -s, --status-codes <STATUS_CODE>...
            含めるステータスコード（許可リスト）（デフォルト：200 204 301 302 307 308 401 403 405）

    -t, --threads <THREADS> 同時接続可能なスレッド数 (デフォルト: 50)
        --time-limit <TIME_SPEC> すべてのスキャンの総実行時間を制限する（例：--time-limit 10m）。
    -T, --timeout <SECONDS> リクエストがタイムアウトするまでの秒数 (デフォルト: 7)
    -u, --url <URL>...                            対象となるURL（複数可）（--stdinが使用されていない場合は必須）
        --dont-scan <URL>...                      再帰/スキャンから除外するURLまたはRegexパターン（複数可
    -a, --user-agent <USER_AGENT> ユーザーエージェントを設定します(デフォルト: feroxbuster/VERSION)
    -w, --wordlist <FILE> ワードリストへのパスを設定します。

NOTE:
    複数の値を取るオプションは非常に柔軟性があります。 次のような指定の仕方を考えてみましょう。
    拡張子を指定する方法を考えてみましょう。
        ./feroxbuster -u http://127.1 -x pdf -x js,html -x php txt json,docx

    上記のコマンドは、各URLに.pdf、.js、.html、.php、.txt、.json、.docxを追加します。

    上記のすべての方法（複数のフラグ、スペース区切り、カンマ区切りなど）が有効であり
    互換性があります。 また、URL、ヘッダー、ステータスコード、クエリー、サイズフィルターについても同様です。

EXAMPLES:
    Multiple headers:
        ./feroxbuster -u http://127.1 -H Accept:application/json "Authorization: Bearer {token}"

    IPv6, non-recursive scan with INFO-level logging enabled:
        ./feroxbuster -u http://[::1] --no-recursion -vv

    Read urls from STDIN; pipe only resulting urls out to another tool
        cat targets | ./feroxbuster --stdin --silent -s 200 301 302 --redirects -x js | fff -s 200 -o js-files

    Proxy traffic through Burp
        ./feroxbuster -u http://127.1 --insecure --proxy http://127.0.0.1:8080

    Proxy traffic through a SOCKS proxy
        ./feroxbuster -u http://127.1 --proxy socks5://127.0.0.1:9050

    Pass auth token via query parameter
        ./feroxbuster -u http://127.1 --query token=0123456789ABCDEF

    Find links in javascript/html and make additional requests based on results
        ./feroxbuster -u http://127.1 --extract-links

    Ludicrous speed... go!
        ./feroxbuster -u http://127.1 -t 200
