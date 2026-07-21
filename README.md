# VirtualBox - Virtualbox Drag &amp; Drop Setting - On the Rocky Linux 8

**Network Setup on Virtual Box VM	ping google.com**
**nmcli device connect enp0s3	ip addr**

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
	
	
**VirtualBox VM Putty Connection**	

	**select network bridge**

	
	1. Install and start SSH on the VM
	
	sudo dnf install -y openssh-server
	sudo systemctl enable --now sshd
	sudo systemctl status sshd
	
	2. Allow SSH through the firewall
	
	sudo firewall-cmd --permanent --add-service=ssh
	sudo firewall-cmd --reload

	
	**Fix: force Ruby to load logger first  :: For Ruby 3.3.0 with Rail**

	ruby -rlogger -e "require 'rails/cli'" 2>&1 | head -5
	
	export RUBYOPT="-rlogger"
	
    rails -v


	
	
**Fix: force Ruby to load logger first**

Quick one-off test:

bash
ruby -rlogger -e "require 'rails/cli'" 2>&1 | head -5

Actual fix — set RUBYOPT so every Ruby process requires logger before anything else runs:

bash
export RUBYOPT="-rlogger"

rails -v

If that works, make it permanent by adding it to your shell config:

bash
echo 'export RUBYOPT="-rlogger"' >> ~/.bashrc   # or ~/.zshrc if you use zsh

source ~/.bashrc

Then confirm:

bash
rails -v

# should print: Rails 6.1.7.6
Why this works
Ruby 3.3's rubygems no longer implicitly pulls in logger as part of its core loading process the way older Ruby versions did. Rails 6.1's activesupport (all patch versions, including 6.1.7.6) references Logger::Severity directly without ever calling require "logger" itself — it always depended on something else loading it first. RUBYOPT="-rlogger" patches that gap globally for your shell/rbenv version.

**Inside an actual Rails app**

Once you get past rails -v and start building an app (rails new myapp), also add this to the generated Gemfile so it works for anyone else running bundle exec rails without your shell's RUBYOPT set:

ruby
gem "logger", "~> 1.4.2"

Then:
bash
bundle install


