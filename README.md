# My setup of Pop!_OS 20.04

# First

Using Rufus
1. Connect an thumb drive into your PC. 
2. Go to the system 76 Pop!_os download page, https://pop.system76.com/. 
3. Download Rufus, Please use this site to download: https://rufus.ie/en/
4. Open Rufus Imager and choose the required OS from the list presented. Please be sure to 'Choose' the SD card you wish to write your image to. 
5. Review your selections and click 'WRITE' to begin writing data to the SD card. (you will get a warning about the own of the ISO not being part of part of the group allowed to make ISO with MBR partitions and will have to use DD instead, just say "yes" or "ok".
6. Once this is done please remove the thumb drive.
7. Insert the thumb drive into the PC that is being imaged.
8. Turn the PC on and boot into the PC Bios with either F2, F12, or Delete key.
9. Make sure to specify the USB drive in boot and continue.
10. Please choose your language, keyboard layout and country
11. Please choose wheather your installing on a new/clean installation, an existing installation or custome.
12. Then choose your Hard Disk drive.
13. Please choose your name/username
14. Please choose your password
15. Then install
16. Then wait for the system to install and fishish before the PC will reboot into your installation.

## To enable Wi-Fi / Ethernet (if not installed during setup)


``

    #Find the file named “50-cloud-init.yaml” and open it in a text editor. 
    #
    #`sudo nano /etc/netplan/50-cloud-init.yaml`
    #
    #    version: 2
    #    ethernets:
    #       eth0:
    #          dhcp4: true
    #	  optional: true
    #    wifis:
    #      wlan0:
    #        dhcp4: true
    #	optional: true
    #	access-points:
    #	  "YOUR_WIFI_NAME":
    #	    password: "YOUR_WIFI_PASSWORD"
    #
    #
    #
    # A few things to pay attention to:
    #
    # 1. Make sure the indentation is exactly 2 spaces. No tab, no 4 spaces.
    # 2. Replace YOUR_WIFI_NAME with your actual Wi-Fi name. Keep the quotes “”.
    # 3. Replace YOUR_WIFI_PASSWORD with the password for the Wi-Fi. Keep the quotes “”.

``

To fix my laptops network drops I had to use the following command, as I have a Broadcom brcm4313 wifi card:

`$sudo apt install broadcom-sta-dkms`

# Setting up Ubuntu remotely

You will need to install ssh server

`$sudo apt install openssh-server ssh`

Now you should now be able to ssh into your laptop/desktop remotely from a Windows machine using putty or Linux from the command line.

Please log using the following: 
username:
`You entered during setup`
password:
`You entered during setup`

Once logged in you will be asked to change your password please do so.  Once this is done the connection will be be reset and you will need to log back into the system using the username: ubuntu and your new password.

Once log into please do the following:

`sudo apt update && sudo apt upgrade -y`

Then reboot the system

`sudo reboot`

Once log into please add the user1 user

`sudo adduser user1 -m -s /bin/bash -c "Administrative User"`

Below is the output.  Please enter a password and then confirm it and press enter through the rest of the questions, for expedency, or answer if you like.

    Enter new UNIX password: 
    Retype new UNIX password: 
    passwd: password updated successfully
    Changing the user information for username
    Enter the new value, or press ENTER for the default
	    Full Name []: 
	    Room Number []: 
	    Work Phone []: 
	    Home Phone []: 
	    Other []: 
    Is the information correct? [Y/n] 

Inaddition please add the user1 user to the sudoers so if we need to have super user privilages we can do so.

`sudo usermod -aG sudo,adm,docker user1`

Once this is done please logout and back in for changes to take effect.

If the password screen did not appear simply type the following:

`$passwd user1`

You should no see the following:

``

    Enter new UNIX password: 
    Retype new UNIX password: 
    passwd: password updated successfully
    
``


# Set Up Automatic Security Update

``

    $sudo apt install unattended-upgrades
    $sudo dpkg-reconfigure --priority=low unattended-upgrades
``

# Install APT package Manager

- synaptic

``

    $sudo apt install synaptic
    
``


# Installing some addition apps

- sysmontask

``

    $sudo add-apt-repository ppa:camel-neeraj/sysmontask
    $sudo apt install nvidia-smi
    $sudo apt install python3-pip
    $sudo pip3 install -U psutil
    $sudo apt install sysmontask
    

``
   
Usage:

`$sysmontask`

- Gaming setup


``

    $pip3 install LibreGaming
    $LibreGaming -a
    
``

LibreGaming: command not found.

This error can be solved by setting up the PATH in your shell you can do this by entering these lines in your shell file(.bashrc or .zshrc)

* Note that the LibreGaming Script is saved in ~/.local/bin directory by default.

``

    ### PATH
    if [ -d "$HOME/.local/bin" ] ;
       then PATH="$HOME/.local/bin:$PATH"
    fi
``


- Application Image Installer

``

    $sudo add-apt-repository ppa:appimagelauncher-team/stable
    $sudo apt-get update
    $sudo apt install appimagelauncher

``
   
- MyPaint

``

    $wget https://github.com/mypaint/mypaint/releases/download/v2.0.0/MyPaint-v2.0.0-1.AppImage
    $chmod +x MyPaint-v2.0.0-1.AppImage

``
   
Usage:

`$./MyPaint-v2.0.0-1.AppImage`


- sabaki

``

    $https://github.com/SabakiHQ/Sabaki/releases/download/v0.52.0/sabaki-v0.52.0-linux-x64.AppImage
    $chmod +x sabaki-v0.52.0-linux-x64.AppImage

``
   
Usage:

`$./sabaki-v0.52.0-linux-x64.AppImage`


- cheat Sheet

``

    pip install --user glances
    pip install --user 'glances[action,browser,cloud,cpuinfo,docker,export,folders,gpu,graph,ip,raid,snmp,web,wifi]'
    
``
   
Usage:

`$glances`


- cheat Sheet

``

    $sudo apt install rlwrap
    $curl https://cht.sh/:cht.sh | sudo tee /usr/local/bin/cht.sh
    $chmod +x /usr/local/bin/cht.sh
``
   
Usage:

`$cht.sh go reverse a list`


- bpytop

``

    $sudo apt install python3-pip
    $sudo pip3 install psutil --upgrade
    $pip3 install bpytop --upgrade   

or

    $sudo apt install bpytop
``

Usage:

`$byptop`


- Speedtest

``

    $sudo apt install speedtest-cli
``
    
Usage:

    `$speedtest`


- lolcat

``

    $sudo apt install lolcat
    or
    $sudo snap install lolcat
``

Usage:

    `$speedtest | lolcat`
    

- lsdir

Go to the release page at https://github.com/Peltoche/lsd/releases and very the lastest release date to download.

``

    $wget https://github.com/Peltoche/lsd/releases/download/0.20.1/lsd_0.20.1_arm64.deb
    $sudo dpkg -i lsd_0.20.1_arm64.deb
``


Use a text editor and edit ~/.bashrc

``

$nano ~/.bashrc

replace 

alias ls='ls --color=auto'

with

alias ls='lsd'

``

Usage:

 `$ls`


- Additional Apps

Just some apps I think are inportant

``

    $sudo apt install ubuntu-restricted-extras
    $sudo apt install libdvd-pkg
    $sudo dpkg-reconfigure libdvd-pkg
    $sudo apt install VLC GIMP kdenlive Audacity rar xarchiver gnome-tweak-tool Trash-cli Youtube-dl neofetch htop ncdu speedtest-cli -y
    $sudo apt install mosh neofetch git nixnote2 guake qmmp synaptic p7zip-full cheese ntfs-3g ffmpeg ettercap-graphical yersinia -y
    
``

From the Pop Shop install the following:


``

    OBS Studio
    Lutris
    Steam + proton
    Chromium
    Firefox
    Krusader
    timeshift
    Cool-Retro-Term
    Wireshark
    discord
    skype
    zoom-client
    teams-for-linux
    nmap
    handbrake
    solitaire
    code
    rpi-imager
    mumble
    GameHub
    
``

    

From The Firefox web browser go to https://extensions.gnome.org/
In the top tooltip "Click here to install browser extension." Click and install the extensions plugin.

``

    Here install:
    dash to dock
    dash to panel
    User theme
    Application Menu
    etc.

``

# exFat update (https://github.com/arter97/exfat-linux)

``

    sudo add-apt-repository ppa:arter97/exfat-linux
    sudo apt update
    sudo apt install exfat-dkms
``

   
# Angry IP scanner

``

    $wget https://github.com/angryip/ipscan/releases/download/3.7.2/ipscan_3.7.2_amd64.deb
    $sudo dpkg -i ipscan_3.7.2_amd64.deb
``

- cockpit (KVM)

``

    $sudo apt install cockpit
    $sudo apt install cockpit cockpit-machines pcp cockpit-pcp packagekit cockpit-packagekit virt-viewer -y
    $sudo systemctl enable cockpit
    $sudo systemctl start cockpit
    $sudo systemctl enable pmcd
    $sudo systemctl enable pmlogger
    $sudo systemctl start pmcd
    $sudo systemctl start pmlogger
    $sudo systemctl status cockpit
    $sudo systemctl status pmcd
    $sudo systemctl status pmlogger
``
   
Usage:

`https://your_ip:9090`

or

- virtualbox

`$sudo apt install virtualbox virtualbox-ext-pack`

or if that does not work

``

    $wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
    $wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
    $echo "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | \
         sudo tee -a /etc/apt/sources.list.d/virtualbox.list
    $sudo apt update
    $sudo apt install virtualbox-6.1
    $wget https://download.virtualbox.org/virtualbox/6.1.8/Oracle_VM_VirtualBox_Extension_Pack-6.1.8.vbox-extpack
    $sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.8.vbox-extpack
    
    
``


- Katrain

``

    $sudo apt update && sudo apt upgrade
    $sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget
    $sudo apt install build-essential libssl-dev libffi-dev python3-dev xclip xsel python3.6 python-pip3 cython3 -y
    $sudo apt install libsdl2-dev libsdl2-2.0-0 -y
    $sudo apt install libmikmod-dev libfishsound1-dev libsmpeg-dev liboggz2-dev libflac-dev libfluidsynth-dev libsdl2-mixer-dev libsdl2-mixer-2.0-0 -y
    $sudo apt install ffmpeg libavcodec-dev libavdevice-dev libavfilter-dev libavformat-dev libavutil-dev libswscale-dev\
         libswresample-dev libpostproc-dev libsdl2-dev libsdl2-2.0-0 libsdl2-mixer-2.0-0 libsdl2-mixer-dev python3-dev
    $sudo apt install libjpeg-dev libwebp-dev libtiff5-dev libsdl2-image-dev libsdl2-image-2.0-0 -y
    $sudo apt install libfreetype6-dev libsdl2-ttf-dev libsdl2-ttf-2.0-0 -y
    $sudo apt-get install python3-pip build-essential git python3 python3-dev ffmpeg libsdl2-dev libsdl2-image-dev\
         libsdl2-mixer-dev libsdl2-ttf-dev libportmidi-dev libswscale-dev libavformat-dev libavcodec-dev zlib1g-dev\
         libgstreamer1.0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good libpulse\
         pkg-config libgl-dev opencl-headers ocl-icd-opencl-dev
    $sudo apt install software-properties-common
    $sudo add-apt-repository ppa:deadsnakes/ppa
    $sudo apt update
    $python3 -m pip install ffpyplayer
    $python3 -m pip install clipboard
    $python3 -m pip install pygame
    $python3 -m pip install -U katrain
    $python3 -m pip uninstall kivy
    $python3 -m pip install --no-binary kivy kivy==2.0.0rc2
    
    *python3.6 -m venv my_env
    
    $python3 -m katrain
    
``

This is the end for now, but as there is always more todo and see the list will continue to grow I am sure.
