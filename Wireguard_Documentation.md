### Digital Ocean
- I signed up for the digital ocean free trial
- Then I created a droplet, left the region default and chose Ubuntu 20.04 LTS as the operating system
- For the droplet I chose the Basic type with the regular 6$/month plan so that I would have enought storage
- Next I chose the password option and auto generated a random password to use
- Then I hit create droplet
### Installing Docker
- Once the droplet was created, I opened the console and followed [this article](https://thematrix.dev/install-docker-and-docker-compose-on-ubuntu-20-04/) to install docker
- Following the article, I used
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
apt-cache policy docker-ce
sudo apt install docker-ce -y
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
### Installing wireguard
- To install wireguard I followed [this article](https://thematrix.dev/setup-wireguard-vpn-server-with-docker/)
- To create my wireguard directory I used
```
mkdir -p wireguard/config
vim wireguard/docker-compose.yml
```
- Then I copied this into the docker-compose.yml file
```
version: '3.8'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Hong_Kong
      - SERVERURL=1.2.3.4
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
```
- I then changed a couple lines
```
TZ=Asia/Hong_Kong >> TZ=America/Chicago
SERVERURL=1.2.3.4 >> SERVERURL=143.198.73.231 #ipv4 from droplet
PEERS=pc1,pc2,phone1 >> PEERS=pc1,phone1
```
- Then to start wireguard, I used
```
cd wireguard
docker-compose up -d
```
- To see the QR codes to sign in on my phone I used
```
docker-compose logs -f wireguard
```
## Testing wireguard
- To use wireguard on my phone I used
	- +
	- Create from QR code
- To use wireguard on my computer I first used
	```
	vim config/peer_pc1/peer_pc1.conf
	```
	- Then I copied the contents into a new document on my desktop and named in wireguard.conf 
