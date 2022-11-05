### Installing Docker
- To install Docker on my linux machine I used:
```
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyrings.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] httpes://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker sysadmin
```
- To install Docker Compose:
```
sudo apt update
sudo apt install docker-compose-plugin
```
[Pi-Hole Documentation](https://github.com/pi-hole/docker-pi-hole/#quick-start)
- I used this to edit docker-compose.yml
```
vim docker-compose.yml
```
- Then I copied [this](https://github.com/pi-hole/docker-pi-hole/blob/b9f3aada94d8602cc4b3f31c63e63d417a10c1d9/examples/docker-compose.yml.example) into the file and replaced the "ports:" section with:
```
network_mode: "host"
```
- Then, to build the docker I used:
```
docker compose up -d
```
<img width="461" alt="image" src="https://user-images.githubusercontent.com/90875690/200099250-57e0b99e-dd86-4af7-a2e8-91de592cb987.png">
- Then I checked my local pihole on pi.hole/admin/

<img width="960" alt="image" src="https://user-images.githubusercontent.com/90875690/200099236-30e3074f-29c1-45e3-9379-2179c9a23207.png">
