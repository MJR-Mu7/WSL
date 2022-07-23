
## WSL2 Networking fix.


echo -e "[network]\ngenerateResolvConf = false" | sudo tee -a /etc/wsl.conf

sudo unlink /etc/resolv.conf

echo nameserver 8.8.8.8 | sudo tee /etc/resolv.conf


## Docker Install Inside WSL2.


sudo apt install --no-install-recommends apt-transport-https ca-certificates curl software-properties-common gnupg2

update-alternatives --config iptables

. /etc/os-release //get OS ready

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu `lsb_release -cs` test"

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io


## Add Docker to sudo group.


sudo usermod -aG docker $USER


## Update iptables for docker networking to Legacy.


sudo update-alternatives --set iptables /usr/sbin/iptables-legacy

sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy

## Portainer Install.


docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.11.1
