# virtualbox
Virtualbox Drag &amp; Drop Setting

Network Setup on Virtual Box VM	ping google.com
nmcli device connect enp0s3	ip addr
	nmcli device status
	nmcli connection show
	nmcli connection show enp0s3
	nmcli connection modify enp0s3 connection.autoconnect yes
	ip addr show enp0s3
	nmcli connection up enp0s3
	ip addr show enp0s3
	cat /etc/resolv.conf
	systemctl restart NetworkManager
	nmcli connection up enp0s3
	ping google.com
	
**Enable Drag & Drop on Virtual Box VM	Change clipboard and drag & drop Bidirectional**
	
	lsmod | grep vboxguest
	
	sudo dnf install -y gcc make perl elfutils-libelf-devel kernel-devel-$(uname -r) bzip2
	 
	VM window menu: Devices → Insert Guest Additions CD image
	
	sudo /mnt/VBoxLinuxAdditions.run
	
	
**virtualbox vm putty connection**	
**1. Install and start SSH on the VM**
	**select network bridge**
	**On the Rocky Linux VM:**
	
	sudo dnf install -y openssh-server
	sudo systemctl enable --now sshd
	sudo systemctl status sshd
	
	2. Allow SSH through the firewall
	
	sudo firewall-cmd --permanent --add-service=ssh
	sudo firewall-cmd --reload


