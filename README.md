## WSL2 Networking fix.


	echo -e "[network]\ngenerateResolvConf = false" | sudo tee -a /etc/wsl.conf

	sudo unlink /etc/resolv.conf

	echo nameserver 8.8.8.8 | sudo tee /etc/resolv.conf


## Fix Systemd


	sudo apt-get update && sudo apt-get install -yqq daemonize dbus-user-session fontconfig

	echo 'sudo daemonize /usr/bin/unshare --fork --pid --mount-proc /lib/systemd/systemd --system-unit=basic.target  exec sudo nsenter -t $(pidof systemd) -a su - $LOGNAME' >> ~/.bashrc
	
	
## Systemd second way to do it

	cd /tmp

	wget --content-disposition   "https://gist.githubusercontent.com/djfdyuruiry/6720faa3f9fc59bfdf6284ee1f41f950/raw/952347f805045ba0e6ef7868b18f4a9a8dd2e47a/install-sg.sh"
	
	chmod +x /tmp/install-sg.sh

	/tmp/install-sg.sh && rm /tmp/install-sg.sh
## In cmd
	

	wsl --shutdown
	wsl genie -s
	ctrl +c // incase it takes too long
	wsl genie -s 

#System in now booted with systemd#


#System will now boot with systemd everytime#


## Docker Install Inside WSL2.


	sudo apt install --no-install-recommends apt-transport-https ca-certificates curl software-properties-common gnupg2

	sudo update-alternatives --config iptables

	. /etc/os-release //get OS ready

	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

	echo "deb [arch=amd64] https://download.docker.com/linux/${ID} ${VERSION_CODENAME} stable" | sudo tee /etc/apt/sources.list.d/docker.list

	sudo apt update

	sudo apt install docker-ce docker-ce-cli containerd.io

	sudo usermod -aG docker $USER

Incase docker doesnt start just run.

	sudo dockerd

	or

	systemctl start docker.service


## Update iptables for docker networking.


	sudo update-alternatives --set iptables /usr/sbin/iptables-legacy

	sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy


## Portainer Install.


	docker volume create portainer_data

	docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.11.1
