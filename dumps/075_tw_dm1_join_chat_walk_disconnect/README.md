# 075_tw_dm1_join_chat_walk_disconnect

This pcap was generated on my local machine (linux debian 13)
using the official teeworlds release for server and client.

- **client**: [official teeworlds 0.7.5 release for linux](https://downloads.teeworlds.com/teeworlds-0.7.5-linux_x86_64.tar.gz)
- **server**: [official teeworlds 0.7.5 release for linux](https://downloads.teeworlds.com/teeworlds-0.7.5-linux_x86_64.tar.gz)
- **map**: dm1 crc=64548818 sha256=491af17a510214506270904f147a4c30ae0a85b91bb854395be
- **version**: 0.7.5 (0.7 802f1be60a05665f)

The pcap captured the full cycle of a player joining, sending the chat message "hello"
walking left, shooting left and disconnecting.

![preview 0](./images/0.png)
![preview 1](./images/1.png)
![preview 2](./images/2.png)
![preview 3](./images/3.png)

## Setup

Download offical release for linux and make sure it uses local storage
to avoid user wide configs to interfere.

```
wget https://downloads.teeworlds.com/teeworlds-0.7.5-linux_x86_64.tar.gz
tar xvf teeworlds-0.7.5-linux_x86_64.tar.gz
cd teeworlds-0.7.5-linux_x86_64
printf '%s\n%s\n' 'add_path $CURRENTDIR' 'add_path $DATADIR' > storage.cfg
```

Start the server in one terminal tab.

```
./teeworlds_srv > server_log.txt
```

Start the traffic capture in another one.

```
sudo tcpdump -i lo "port 8303" -w 075_tw_dm1_join_chat_walk_disconnect.pcap
```

Connect the client.

```
./teeworlds "gfx_fullscreen 0;gfx_screen_width 1600;gfx_screen_height 900;cl_auto_demo_record 1;connect 127.0.0.1"
```

After the client disconnected stop the tcpdump and generate the tshark log.

```
tshark -r 075_tw_dm1_join_chat_walk_disconnect.pcap > tshark_libtw2.txt
```
