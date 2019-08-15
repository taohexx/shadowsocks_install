- Origional Author: Twitter [@qiushuiyibing](https://twitter.com/qiushuiyibing)

- Download the Client from the [release](https://github.com/charlieethan/shadowsocks_install/releases/download/V1.0/Shadowsocks.zip)

- A successful example for `shadowsocks-libev` install on `CentOS 7` with `"Simple-Obfs"(Use Xshell 6 on Windows10)`,here's the steps.

```bash
yum update
yum install -y git wget vim
wget --no-check-certificate -O shadowsocks-libev.sh https://raw.githubusercontent.com/charlieethan/shadowsocks_install/master/shadowsocks-libev.sh && chmod +x shadowsocks-libev.sh && ./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log
cd /usr/src
sudo yum install gcc autoconf libtool automake make zlib-devel openssl-devel asciidoc xmlto
git clone https://github.com/charlieethan/simple-obfs.git
cd simple-obfs
git submodule update --init --recursive
./autogen.sh
./configure --disable-documentation
make && make install
vim /etc/shadowsocks-libev/config.json
```
*Then,you can see the config like this below:*
   {
    "server":"0.0.0.0",
    "server_port":9000,
    "password":"password",
    "timeout":300,
    "user":"nobody",
    "method":"aes-256-gcm",
    "fast_open":false,
    "nameserver":"8.8.8.8",
    "mode":"tcp_and_udp"
   }
*Add the code below:*
```bash
"plugin":"obfs-server",
"plugin_opts":"obfs=http"
```
*The **Final Config** like this:*
   {
    "server":"0.0.0.0",
    "server_port":9000,
    "password":"password0",
    "timeout":300,
    "user":"nobody",
    "method":"aes-256-gcm",
    "fast_open":false,
    "nameserver":"8.8.8.8",
    "mode":"tcp_and_udp",
    "plugin":"obfs-server",
    "plugin_opts":"obfs=http"
   }
*Type `:wq` for saving.If All the things above you have done,you can do the remains.*
```bash
/etc/init.d/shadowsocks restart
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/charlieethan/BBR-Accerate/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
*Press the number `1` to install the core,and then press `y` for VPS restarting.After that,enter the code below.*
```bash
cd /usr/src && ./tcp.sh
```
*Press the number `5` to install the script.*

**Client Setting**

**plugin program： `obfs-local`**

**plugin options： `obfs=http;obfs-host=www.github.com`**

- Tips: If you meet the case `"-bash permission denied"` on CentOS when you run script like `*.sh` from this page,please 
  try to use this command `"chmod 777 *.sh"` before you run the script.
  
  e.g: If you wanna run `"shadowsocks-libev.sh"` but meet the `"permission denied"`,use the command `"chmod 777 shadowsocks-libev.sh"`,and 
  then,you can run `"shadowsocks-libev.sh"` without any problems.
