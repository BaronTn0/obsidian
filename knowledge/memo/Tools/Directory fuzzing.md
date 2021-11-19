[dirb](http://dirb.sourceforge.net/) (C), [dirbuster](https://sourceforge.net/projects/dirbuster/) (Java), [gobuster](https://github.com/OJ/gobuster) (Go), [wfuzz](https://github.com/xmendez/wfuzz) (Python), [ffuf](https://github.com/ffuf/ffuf) (Go)などのツールは、ディレクトリファジングやブルートフォースを行うことができます。Burp Suiteでもできます。ウェブアプリケーションによっては、どれかが他よりも適していて、追加のオプションが必要になるでしょう。

ディレクトリ・ファジングは、意図しないサービス拒否につながる可能性があるため、本番環境のインスタンスをテストする際には、速度を落とす必要があります。

gobuster dir --useragent "PENTEST" -w /usr/share/seclists/Discovery/Web-Content/common.txt -u $URL

wfuzz --hc 404,403 -H "User-Agent: PENTEST" -c -z file,/usr/share/seclists/Discovery/Web-Content/common.txt $URL/FUZZ

ffuf -H "User-Agent: PENTEST" -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -u $URL/FUZZ

また、[feroxbuster](https://github.com/epi052/feroxbuster) (Rust)という素晴らしいツールは、再帰的なコンテンツ発見を非常に高速に行うことができます。上記のツールは、検索されたディレクトリ内を再検索しません。

feroxbuster -H "User-Agent: PENTEST" -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://192.168.10.10/

より正確にfuzzするために、様々な状況に対応した辞書があります。究極のコンボは、[fuff](https://github.com/ffuf/ffuf) + [fzf](https://github.com/junegunn/fzf) + [seclists](https://github.com/danielmiessler/SecLists)です。

次のコマンドでは、[fzf](https://github.com/junegunn/fzf)を使用して、ファイルファザーのプロンプトを表示し、ユーザーがコンテンツ発見に最適なワードリストをすばやく選択できるようにしています。

feroxbuster -H "User-Agent: PENTEST" -w \`fzf-wordlists\` -u http://192.168.10.10/

この場合、`fzf-wordlists`は、fzfとfindを使って、特定のディレクトリからワードリストをファジングする次のコマンドのエイリアスです。

find /usr/share/seclists /usr/share/wordlists /usr/share/dirbuster /usr/share/wfuzz /usr/share/dirb -type f | fzf