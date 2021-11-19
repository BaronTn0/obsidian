XLMMacroDeobfuscator(v0.1.9) - https://github.com/DissectMalware/XLMMacroDeobfuscator

usage: xlmdeobfuscator [-h] [-c FILE_PATH] [-f FILE_PATH] [-n] [-x] [--sort-formulas] [--defined-names] [-2] [--with-ms-excel] [-s] [-d DAY] [--output-formula-format OUTPUT_FORMULA_FORMAT]
                       [--extract-formula-format EXTRACT_FORMULA_FORMAT] [--no-indent] [--export-json FILE_PATH] [--start-point CELL_ADDR] [-p PASSWORD] [-o OUTPUT_LEVEL] [--timeout N]

optional arguments:
  -h, --help このヘルプメッセージを表示して終了する。
  -c FILE_PATH, --config-file FILE_PATH
                        設定ファイルを指定します(有効なJSONファイルである必要があります)
  -f FILE_PATH, --file FILE_PATH
                        XLSMファイルのパスを指定
  -n, --noninteractive 対話型シェルを無効にします。
  -x, --extract-only エミュレーションを行わずにセルのみを抽出します。
  -sort-formulas 抽出された数式をセルのアドレスに基づいてソートします（-x が必要）。
  --定義済みの名前 すべての定義済みの名前を抽出
  -2, --no-ms-excel [非推奨] XLS ファイルの処理に MS Excel を使用しません。
  --with-ms-excel MS Excel を使用して XLS ファイルを処理します。
  -s, --start-with-shell
                        入力のマクロを解釈する前に XLM シェルを開きます。
  -d DAY, --day DAY 月の日を指定します。
  --出力式のフォーマット OUTPUT_FORMULA_FORMAT
                        出力形式 ([[CELL-ADDR]]、[[INT-FORMULA]]、[[STATUS]]の形式を指定します。
  --extract-formula-format EXTRACT_FORMULA_FORMAT
                        抽出された数式（[[CELL-ADDR]]、[[CELL-FORMULA]]、[[CELL-VALUE]]）のフォーマットを指定します。
  --no-indent 数式の前にインデントを表示しない。
  --export-json FILE_PATH
                        出力をJSONに書き出す
  --開始点 CELL_ADDR
                        特定のセルアドレスから解釈を開始する
  -p PASSWORD, --password PASSWORD
                        保護された文書を復号するためのパスワード
  -o OUTPUT_LEVEL, --output-level OUTPUT_LEVEL
                        表示する詳細のレベルを設定します(0:全てのコマンド、1:ジャンプしないコマンド 2:重要なコマンド 3:重要なコマンド内の文字列)。
  --timeout N N秒後にエミュレーションを停止する(0:中断しない N>0:N秒後にエミュレーションを停止する)