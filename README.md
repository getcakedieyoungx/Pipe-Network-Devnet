# Pipe Network Devnet Node

Join tg, I will post bots there too.
[Telegram](https://t.me/getcakedieyoungx)

## Introduction
Pipe Network Devnet node is open for all now. 

## Getting Started

Follow these steps to set up.

### 1. 1. Create directories

```bash
mkdir -p /root/pipe
mkdir -p /root/pipe/download_cache/
```
```bash
cd /root/pipe
```

### 2.  Download Pipe binaries


```bash
wget -O pop "https://dl.pipecdn.app/v0.2.8/pop"
```


### 3. Make pop executable
```bash
chmod +x pop
```

### 4. Create systemd file

We create a systemd file to run the node by entering the following command.

!! Please change your address etc.:

--ram 4: Replace 4 with your favorite Ram you want to allocate. (e.g., 4 for 8GB).

--max-disk 200: Replace 200 with the hard disk you want to allocate. (e.g., 200 for 200GB).

--pubKey SOLADDRESS: Your Solana Address


```bash
sudo tee /etc/systemd/system/pipe.service > /dev/null << EOF
[Unit]
Description=Pipe Node Service
After=network.target
Wants=network-online.target

[Service]
User=root
Group=root
WorkingDirectory=/root/pipe
ExecStart=/root/pipe/pop \
    --ram 4 \
    --max-disk 200 \
    --cache-dir /root/pipe/download_cache \
    --pubKey SOLADDRESS \
    --signup-by-referral-route d48023e348663b48
Restart=always
RestartSec=5
LimitNOFILE=65536
LimitNPROC=4096
StandardOutput=journal
StandardError=journal
SyslogIdentifier=dcdn-node

[Install]
WantedBy=multi-user.target
EOF
```

### 5. Start systemd

```bash
sudo systemctl daemon-reload
sudo systemctl enable pipe
sudo systemctl start pipe
```

### 5. Stop and restart using screen
After the node registered, if you keep running that systemd you'll get errors because that is a one time code for registering.

####Stop the node
```bash
sudo systemctl stop pipe
```
Create screen

```bash
screen -S pipe
```

Start pipe

```bash
sudo ./pop
```

After that, CTRL A+D detach screen



### 6. Check score

```bash
cd $HOME && cd pipe
./pop --status
```



### 6. Backup Files

Recommened to backup node_info.json in /root/pipe. It is linked to the IP address that registered the PoP node. It is no recoverable if lost.

node_info.json: Node configuration
download_cache: Cached content
You will not be able to create a new node and new node_info.json with the same IP


Check your node status on here:

https://dashboard.pipenetwork.com/


Ask me if you have questions.
