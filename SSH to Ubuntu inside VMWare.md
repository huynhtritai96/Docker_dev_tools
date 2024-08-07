To SSH into your Ubuntu VM in VMware, follow these steps:

### 1. Install OpenSSH Server
```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

### 2. Verify SSH Status
Check the status to ensure SSH is running:
```bash
sudo systemctl status ssh
```
**Output:**
```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-08-07 14:20:51 PDT; 31s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 9639 (sshd)
      Tasks: 1 (limit: 9371)
     Memory: 1.0M
     CGroup: /system.slice/ssh.service
             └─9639 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
```
- **Loaded:** Indicates the SSH service is correctly loaded from the system’s service directory.
- **Active:** Confirms the SSH service is currently running.
- **Main PID:** The process ID of the SSH daemon (sshd), which is handling SSH connections.
- **Server listening on 0.0.0.0 port 22:** Indicates the SSH server is listening for connections on all IPv4 interfaces on port 22.
- **Server listening on :: port 22:** Indicates the SSH server is also listening for connections on all IPv6 interfaces on port 22.
### 3. Find VM IP Address
Get the IP address of your VM:
```bash
ip addr show
```
**Output:**
```
3: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:16:7a:7c brd ff:ff:ff:ff:ff:ff
    inet 192.168.192.130/24 brd 192.168.192.255 scope global dynamic noprefixroute ens33
       valid_lft 1100sec preferred_lft 1100sec
    inet6 fe80::57eb:ab45:38ee:6e2f/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
- **ens33:** Network interface name used for the network connection.
- **inet 192.168.192.130/24:** IPv4 address assigned to the VM. This is the address you will use to SSH into the VM.
- **link/ether 00:0c:29:16:7a:7c:** MAC address of the network interface.
- **valid_lft 1100sec preferred_lft 1100sec:** The lease time for the IP address from the DHCP server.
### 4. Connect via SSH
From your host machine, open a terminal and connect to your VM using its IP address:
```bash
ssh htritai@192.168.192.130
```
**Explanation:**
- **ssh:** The command to initiate an SSH connection.
- **htritai:** Replace with your actual Ubuntu username.
- **192.168.192.130:** The IP address of your VM. This address is from the output of the `ip addr show` command.
Replace `htritai` with your actual Ubuntu username and enter your password when prompted. This establishes an SSH connection to your Ubuntu VM running in VMware.
