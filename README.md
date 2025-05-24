# wireguard-Server with UI docker-compose
### Install
```
git clone https://github.com/cokacolaa/wireguard-manager.git && cd ./wireguard-manager && sudo docker-compose up -d 
```

### Login
Login http://ip_host:5000

- Port forwarding: 51820/UDP on UI
- user: admin
- pass: admin
- Post Up Script: iptables -A FORWARD -i %1 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth+ -j MASQUERADE
- Post Down Script: iptables -D FORWARD -i %1 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth+ -j MASQUERADE
  ![image](https://github.com/user-attachments/assets/48eb44be-ffd5-487a-88a1-e0254a4d63be)
## Config file template to change port listen endpoint
```
vi ./config/template/peer.conf
```
```
[Interface]
Address = ${CLIENT_IP}
PrivateKey = $(cat /config/${PEER_ID}/privatekey-${PEER_ID})
ListenPort = 51820
DNS = ${PEERDNS}

[Peer]
PublicKey = $(cat /config/server/publickey-server)
PresharedKey = $(cat /config/${PEER_ID}/presharedkey-${PEER_ID})
# Change endpoint = ${WGUI_ENDPOINT_ADDRESS}
Endpoint = ${WGUI_ENDPOINT_ADDRESS}
AllowedIPs = ${ALLOWEDIPS}```
