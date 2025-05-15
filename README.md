# wireguard-docker

## Desktop client

Example: https://github.com/DefGuard/client

## Mobile clients

Official mobile clients are available for WireGuard.

## Some needed commands

A history of commands used:

```bash
mkdir -p ~/wireguard/config
cd ~/wireguard

vim docker-compose.yml

ls
/usr/local/bin/docker-compose up -d
/usr/local/bin/docker-compose ps
ls
/usr/local/bin/docker-compose logs
ls
/usr/local/bin/docker-compose down
vim docker-compose.yml 
/usr/local/bin/docker-compose up -d
ls
```

### Config files

QR code images for clients/peers:

```bash
ls -la ~/wireguard/config/peer*
ls -la ~/wireguard/config/
ls -la ~/wireguard/config*
```

### Firewall

Just in case:

```bash
# Clear any existing rules for port 51820
sudo firewall-cmd --permanent --remove-port=51820/udp
sudo firewall-cmd --permanent --remove-port=51820/udp --zone=docker

# Add the port to the public zone with masquerade
sudo firewall-cmd --permanent --zone=public --add-port=51820/udp
sudo firewall-cmd --permanent --zone=public --add-masquerade
sudo firewall-cmd --reload
```

### Verify

Verify it's working:

```bash
# Check container logs
docker logs -f wireguard

# Verify connectivity
curl -s ifconfig.me
```

## To upgrade CentOS Stream 8 kernel from 4.xx to 6.xx

Since WireGuard is added to newer Linux kernels, legacy Linux kernels won't work.

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
```

