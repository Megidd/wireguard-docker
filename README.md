# wireguard-docker

## Desktop client

Example: https://github.com/DefGuard/client

## Mobile clients

Official mobile clients are available by WireGuard.

## Some needed commands

```bash
mkdir -p ~/wireguard/config
cd ~/wireguard

vim docker-compose.yml

ls
/usr/local/bin/docker-compose up -d
/usr/local/bin/docker-compose ps
firewall-cmd --permanent --add-port=51820/udp
systemctl restart firewalld
firewall-cmd --reload
ls
ls -la ~/wireguard/config/peer*
ls -la ~/wireguard/config/
ls -la ~/wireguard/config*
ls
ls
/usr/local/bin/docker-compose logs
less /proc/version 
less /proc/version 
ls
/usr/local/bin/docker-compose down
vim docker-compose.yml 
/usr/local/bin/docker-compose up -d
vim docker-compose.yml 
/usr/local/bin/docker-compose up -d
ls -la ~/wireguard/config/
ls
```

### To upgrade CentOS Stream 8 kernel from 4.xx to 6.xx

Since WireGuard is added to newer Linux kernels, legacy Linux kernel won't work.

```bash
ls /etc/*elease
less /etc/os-release 
less /etc/redhat-release 
uname -sr
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm --import https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org
less /etc/redhat-release 
yum install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
yum --enablerepo=elrepo-kernel install -y kernel-ml
reboot
history |less
history > history.txt
```

# Allowed IPs

For some reason, I had to go inside the Docker container by:

```bash
sudo docker ps # See Docker container ID
sudo docker exec -t -i <container-ID>  /bin/bash # Go inside the container and access the shell command line
```

Now, inside the container, run:

```bash
cat /etc/wireguard/wg0.conf # Observe the allowed IPs for all peers
```

If Allowed IPs for peers are something like `AllowedIPs = 10.13.13.2/32`, then open the file with an editor line `vi`:

```bash
vi /etc/wireguard/wg0.conf
```

Edit and replace `AllowedIPs = 10.13.13.2/32`  with `AllowedIPs = 0.0.0.0/0` for all peers.

Restart the container:

```bash
sudo /usr/local/bin/docker-compose down
sudo /usr/local/bin/docker-compose up -d
```
