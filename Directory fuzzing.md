Tools like [dirb](http://dirb.sourceforge.net/) (C), [dirbuster](https://sourceforge.net/projects/dirbuster/) (Java), [gobuster](https://github.com/OJ/gobuster) (Go), [wfuzz](https://github.com/xmendez/wfuzz) (Python) and [ffuf](https://github.com/ffuf/ffuf) (Go) can do directory fuzzing/bruteforcing. Burp Suite can do it too. Depending on the web application, one will be better suited than another and additional options will be needed.

Directory fuzzing needs to be slowed down when testing production instances as it could lead to an unintended denial of service.

gobuster dir --useragent "PENTEST" -w /usr/share/seclists/Discovery/Web-Content/common.txt -u $URL

wfuzz --hc 404,403 -H "User-Agent: PENTEST" -c -z file,/usr/share/seclists/Discovery/Web-Content/common.txt $URL/FUZZ

ffuf -H "User-Agent: PENTEST" -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -u $URL/FUZZ

Another great tool named [feroxbuster](https://github.com/epi052/feroxbuster) (Rust) can do really fast recursive content discovery. The tools mentioned above don't recurse in found directories.

feroxbuster -H "User-Agent: PENTEST" -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://192.168.10.10/

In order to fuzz more accurately, there are many dictionaries adapted for many situations. The ultimate combo is [ffuf](https://github.com/ffuf/ffuf) + [fzf](https://github.com/junegunn/fzf) + [seclists](https://github.com/danielmiessler/SecLists).

In the following command, [fzf](https://github.com/junegunn/fzf) is used to print a file fuzzer prompt allowing the user to quickly choose the perfect wordlist for content discovery.

feroxbuster -H "User-Agent: PENTEST" -w \`fzf-wordlists\` -u http://192.168.10.10/

In this case, `fzf-wordlists` is an alias to the following command using fzf and find to fuzz wordlists from specific directories.

find /usr/share/seclists /usr/share/wordlists /usr/share/dirbuster /usr/share/wfuzz /usr/share/dirb -type f | fzf