usage: fzf [options]

  Search
     -x, --extended 拡張検索モード
                          (デフォルトでは有効。無効にするには+xまたは--no-extended)
    -e, --exact 厳密な一致を有効にする。
    --algo=TYPE ファジー・マッチング・アルゴリズム。[v1|v2] (デフォルト: v2)
    -i 大文字小文字を区別しないマッチ（デフォルト：スマートケースマッチ）
    +i 大文字小文字を区別するマッチ
    --literal ラテン文字を正規化せずに照合する。
    -n, --nth=N[,...] 検索範囲を限定するためのフィールド・インデックス式のカンマ区切りリスト。
                          検索範囲を制限するために それぞれ、ゼロ以外の整数または
                          整数または範囲表現（[BEGIN]...END）です。
    --with-nth=N[,...] フィールドインデックス式を使って、各行の表示を変換します。
                          フィールドインデックス表現
    -d, --delimiter=STR フィールドデリミタ正規表現 (デフォルト: AWKスタイル)
    +s, --no-sort 結果をソートしません。
    --tac 入力の順序を逆にする
    --phony 検索を行わない
    --tiebreak=CRI[,...] スコアが同点のときに適用するソート基準のカンマ区切りのリスト
                          スコアが同点のときに適用するソート基準のカンマ区切りリスト [length|begin|end|index]。
                          (デフォルト: length)

  Interface
    -m, --multi[=MAX] タブ/シフトタブによるマルチセレクトを有効にする
    --no-mouse マウスを無効にする
    --bind=KEYBINDS カスタムキーバインディング。manページを参照してください。
    --cycle サイクリックスクロールを有効にする
    --keep-right オーバーフロー時に行の右端を表示したままにします。
    --no-hscroll 水平スクロールを無効にします。
    --hscroll-off=COL ハイライトされた部分文字列の右側を維持する画面の列数 (デフォルト: 10)
                          強調表示された部分文字列の右側を維持する画面列数 (デフォルト: 10)
    --filepath-word パスの区切りを考慮した単語単位の移動を行います。
    --jump-labels=CHARS jump および jump-accept のラベル文字。

  Layout
    --height=HEIGHT[%] カーソルの下に、与えられた高さの fzf ウィンドウを表示します。
                          の高さで表示し、フルスクリーンにはしない。
    --min-height=HEIGHT --height をパーセントで指定したときの最小の高さ。
                          (デフォルト: 10)
    --layout=LAYOUT レイアウトを選択します。レイアウトの選択： [default|reverse|reverse-list].
    --border[=STYLE] ファインダーの周囲に境界線を表示します。
                          [ラウンド|シャープ|水平|垂直
                           top|bottom|left|right] となります。(default: round)
    --margin=MARGIN 画面のマージン（TRBL｜TB,RL｜T,RL,B｜T,R,B,L）を指定します。
    --padding=PADDING 境界線内のパディング (TRBL | TB,RL | T,RL,B | T,R,B,L)
    --info=STYLE ファインダー情報のスタイル [default|inline|hidden]を指定します。
    --prompt=STR 入力プロンプト (デフォルト: '> ')
    --pointer=STR 現在の行へのポインタ (デフォルト: '>')
    --marker=STR 複数選択マーカー(デフォルト: '>')
    --header=STR ヘッダーとして表示する文字列
    --header-lines=N 入力の最初のN行をヘッダーとして扱う。
	
  Display
     --ansi ANSIカラーコードの処理を有効にする
    --tabstop=SPACES タブ文字のスペース数 (デフォルト: 8)
    --color=COLSPEC ベーススキーム(dark|light|16|bw)および/またはカスタムカラー
    --no-bold 太字テキストを使用しません。

  History
    --history=FILE ヒストリーファイル
    --history-size=N ヒストリーエントリの最大数（デフォルト：1000）

  Preview
    --preview=COMMAND ハイライトされた行をプレビューするコマンド ({})
    --preview-window=OPT プレビューウィンドウのレイアウト (default: right:50%)
                          [up|down|left|right][:SIZE[%]]
                          [:[no]wrap][:[no]cycle][:[no]hidden]
                          [:rounded|sharp|noborder]
                          [:+SCROLL[-OFFSET]]
                          [:default]

  Scripting
   -q, --query=STR 指定されたクエリでファインダーを起動します。
    -1, --select-1 唯一のマッチを自動的に選択します。
    -0, --exit-0 一致するものがない場合は直ちに終了します。
    -f, --filter=STR フィルタモードです。インタラクティブなファインダーを起動しません。
    --print-query クエリを1行目に表示します。
    --expect=KEYS fzfを完成させるためのキーをカンマで区切ったリスト
    --read0 ASCII の NUL 文字で区切られた入力を読み込みます。
    --print0 ASCIIのNUL文字で区切られた出力の印刷
    --sync 多段階フィルタリングのための同期検索
    --version バージョン情報を表示して終了

  Environment variables
    FZF_DEFAULT_COMMAND 入力が tty のときに使用するデフォルトのコマンド
    FZF_DEFAULT_OPTS デフォルトのオプション
                          (例: '--layout=reverse --inline-info')