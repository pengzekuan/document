## 自动

```
wget --no-check-certificate -O shadowsocks.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2> 1 | tee shadowsocks.log
```

## 手动

- pip

```
 curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
 python get-pip.py
```

- ss

```
pip install --upgrade pip
pip install shadowsocks
```

- config

```
vi /etc/shadowsocks.json

{
"server": "0.0.0.0",
"server_port": 2018,
"password": "12345678",
"method": "aes-256-cfb"
}

or

{
"server": "0.0.0.0",
"port_password": {
"8381": "password1",
"8382": "password2",
"8383": "password3",
"8384": "password4"
},
"timeout": 300,
"method": "aes-256-cfb"
}
```

- firewall

```
配置防火墙
systemctl stop firewalld.service
```

- ss op

```
ssserver -c /etc/shadowsocks.json -d start
ssserver -c /etc/shadowsocks.json -d stop
```