## Wire Guard Tunnel

Two Terms to remember Client and Host,
Client is the device that is connecting to the host.
Also, thank you to [Dan](https://danbot.host) for the help with this.

# Example:
 - Host - VPS
 - Client - Dedi

# Host Setup
- Install Wire Guard 
```bash
  curl -O https://raw.githubusercontent.com/angristan/wireguard-install/master/wireguard-install.sh
  chmod +x wireguard-install.sh
  ./wireguard-install.sh
```
- Copy client file info to your client device
- Setup IpTables 
```bash
iptables -t nat -A PREROUTING -d PublicIP -p tcp -j DNAT --to-dest 10.66.66.2 
```
- Install Persistant IpTables
```bash
 sudo apt-get install iptables-persistent 
 sudo netfilter-persistent save
 sudo netfilter-persistent reload
```

# Client Setup
- Install Wire Guard & Supporting Packages
```bash
apt install resolvconf
apt-get install wireguard
```
- Setup systemctl to start on boot [click me](https://www.ivpn.net/knowledgebase/linux/linux-autostart-wireguard-in-systemd/)
- Copy the previous client file from the host to your device
```bash
sudo nano /etc/wireguard/wg0.conf
```
- ReStart Wire Guard
```bash
systemctl restart wg-quick@wg0
```
- Check if the connection is working
```bash
ping 10.66.66.1
service wg-quick@wg0 status
```
