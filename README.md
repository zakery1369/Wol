## Wake On Lan on Debian

![Wol](https://raw.githubusercontent.com/zakery1369/pics/master/Wol.png)

1.Install ethtool :

```bash
sudo apt install ethtool
```

2.Checking the Interface :

```bash
ip a
```

3.Select the interface you want to use. For Example :

```bash
enp3s0
```

4.Turn wake on lan On Temporarily :

```bash
sudo ethtool --change enp3s0 wol g
```

5.Check the WOL status of the interface with the following command :

```bash
sudo ethtool enp3s0
```

6.Find the bellow section :

```bash
Wake-on: g
```

### Making wake on lan Permanent

7.Find ethtool directory :

```bash
which ethtool
```

in my os : /usr/sbin/ethtool

8.Create wol.service in /etc/systemd/system/ with the following content.

```bash
[Unit]
Description=Enable Wake On Lan

[Service]
Type=oneshot
ExecStart =/usr/sbin/ethtool --change enp3s0 wol g

[Install]
WantedBy=basic.target
```

9.Enable the service :

```bash
sudo systemctl daemon-reload
sudo systemctl enable wol.service
```
