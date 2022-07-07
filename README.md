# WSL
WSL-Notes

## Portainer Install.


docker volume create portainer_data

docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.11.1


## Fix WSL2 Networking.


echo -e "[network]\ngenerateResolvConf = false" | sudo tee -a /etc/wsl.conf

sudo unlink /etc/resolv.conf

echo nameserver 8.8.8.8 | sudo tee /etc/resolv.conf


## Docker Install.


sudo apt install --no-install-recommends apt-transport-https ca-certificates curl gnupg2

curl -fsSL https://download.docker.com/linux/${ID}/gpg | sudo tee /etc/apt/trusted.gpg.d/docker.asc

echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

update-alternatives --config iptables



## Update iptables for docker networking.


sudo update-alternatives --set iptables /usr/sbin/iptables-legacy

sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
