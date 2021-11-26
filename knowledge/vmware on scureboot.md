セキュアモードが有効になっているLinuxホストでは、署名されていないドライバーをロードすることはできません。このため、vmmonやvmnetなどのVMwareドライバーをロードできず、仮想マシンの電源をオンにできません。

 ### セキュアブートが有効になっているかどうかを確認します

1 `sudo` `mokutil --sb-state?`

2 `# output when enabled`

3 `SecureBoot enabled`

### mokutilが欠落している場合

1 `sudo` `apt` `install` `mokutil

### vmwareモジュールに署名するための秘密鍵と公開鍵を作成します

`openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -nodes -days 36500 -subj "/CN=VMware/"`

# sign the compiled modules DO THIS AFTER COMPILING THE MODULE (i.e. after you click the install button and it says it failed to insert the kernel modules)

`sudo /usr/src/linux-headers- `uname -r `/scripts/sign-file sha256 .`/MOK .priv .`/MOK .der $(modinfo -n vmmon)`

`sudo` `/usr/src/linux-headers-``` ` ```uname` ``-r` ```/scripts/sign-file` `sha256 .``/MOK``.priv .``/MOK``.der $(modinfo -n vmnet)`

`# install public key`

`mokutil --import MOK.der`