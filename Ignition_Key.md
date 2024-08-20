Use Cases:
This script will install useful applications on a fresh Linux install preparing it for use.

```bash
#!/bin/bash
#   This script will install useful applications on a fresh Linux install preparing it for use.

# Define colors...

RED=`tput bold && tput setaf 1`

GREEN=`tput bold && tput setaf 2`

YELLOW=`tput bold && tput setaf 3`

BLUE=`tput bold && tput setaf 4`

NC=`tput sgr0`


function RED(){

    echo -e "\n${RED}${1}${NC}"

}

function GREEN(){

    echo -e "\n${GREEN}${1}${NC}"

}

function YELLOW(){

    echo -e "\n${YELLOW}${1}${NC}"

}

function BLUE(){

    echo -e "\n${BLUE}${1}${NC}"

}

  

# Testing if root...

if [ $UID -ne 0 ]

then

    RED "You must run this script as root!" && echo

    exit

fi

  
  
  

BLUE "Updating repositories..."

sudo apt update

  

BLUE "Installing git..."

sudo apt install -y git

  

BLUE "Installing Sublime Text..." # according to https://www.sublimetext.com/docs/3/linux_repositories.html-

wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

sudo apt install -y apt-transport-https

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

sudo apt update

sudo apt install -y sublime-text

  

BLUE "Installing terminator..."

sudo apt install -y terminator

  

BLUE "Setting terminator as the default terminal emulator..."

sed -i s/Exec=gnome-terminal/Exec=terminator/g /usr/share/applications/gnome-terminal.desktop

  

BLUE "Forcing a color prompt in ~/.bashrc..."

grep "export PS1" ~/.bashrc

if [ $? -eq 1 ]

then

    echo "export PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> ~/.bashrc

fi

  

BLUE "Installing SimpleScreenRecorder..."

echo "" | sudo add-apt-repository ppa:maarten-baert/simplescreenrecorder

sudo apt update

sudo apt install -y simplescreenrecorder

  

BLUE "Installing task..."

sudo apt install -y taskwarrior

  

BLUE "Installing pip..."

sudo apt install -y python-pip

  

BLUE "Removing boilerplate home directories..."

rmdir ~/Desktop ~/Documents ~/Downloads ~/Music ~/Pictures ~/Public ~/Templates ~/Videos

  

BLUE "Installing guake..."

sudo apt install -y guake

  

BLUE "Installing openvpn..."

sudo apt install -y openvpn
 

BLUE "Installing nmap..."

sudo apt install -y nmap

  

BLUE "Installing docker..."

sudo apt install -y docker.io

sudo groupadd docker

sudo usermod -aG docker `logname`

  

BLUE "Installing curl..."

sudo apt install -y curl

  

BLUE "Installing pinta..."

sudo apt install -y pinta

  

BLUE "Installing exiftool..."

sudo apt install -y exiftool

  

BLUE "Installing Python PIL..."

sudo apt install -y python-pil

  

BLUE "Installing sqlitebrowser..."

sudo apt install -y sqlitebrowser

  

BLUE "Installing Wireshark..."

sudo apt install -y wireshark

  

BLUE "Install Real VNC Viewer..."

wget "https://www.realvnc.com/download/file/viewer.files/VNC-Viewer-6.17.1113-Linux-x64.deb" -O vnc_viewer.deb

dpkg -i vnc_viewer.deb

rm vnc_viewer.deb

  

BLUE "Install Real VNC Connect (Server)..."

wget 'https://www.realvnc.com/download/file/vnc.files/VNC-Server-6.2.1-Linux-x64.deb' -O vnc_server.deb

dpkg -i vnc_server.deb

rm vnc_server.deb

  

BLUE "Adding VNC Connect (Server) service to the default startup /etc/rc.local..."

grep "vncserver-x11-serviced.service" /etc/rc.local

if [ $? -eq 1 ]

then

    echo "systemctl start vncserver-x11-serviced.service" >> ~/etc/rc.local

fi

  

BLUE "Installing Atom..."

wget "https://atom.io/download/deb" -O atom.deb

dpkg -i atom.deb

rm atom.deb

  

BLUE "Installing python-requests..."

pip install requests

  

BLUE "Installing idle..."

sudo apt install -y idle

  

BLUE "Installing xclip..."

sudo apt install -y xclip

grep "alias xclip" ~/.bashrc

if [ $? -eq 1 ]

then

    echo "alias xclip='xclip -selection clipboard'" >> ~/.bashrc

fi

  

BLUE "Installing Python flask..."

sudo pip install flask

  

BLUE "Installing Python flask-login..."

sudo pip install flask-login

  

BLUE "Installing Python colorama..."

sudo pip install colorama

  

BLUE "Installing Python passlib..."

sudo pip install passlib

  

BLUE "Installing Spotify..."

sudo snap install spotify


BLUE "Installing Binwalk..."

sudo apt install -y binwalk

  

BLUE "Installing Tesseract..."

sudo apt install -y tesseract-ocr

  

BLUE "Installing foremost..."

sudo apt install -y foremost

  

BLUE "Installing rot13..."

sudo apt install -y bsdgames    

  

BLUE "Installing hexedit..."

sudo apt install -y hexedit

  

BLUE "Installing Python pwntools..."

sudo pip install pwntools

  

BLUE "Installing Go..."

sudo apt install -y golang-go

BLUE "Adding GOPATH and GOBIN to .bashrc, so future installs are easy.."

grep "export GOPATH" ~/.bashrc

if [ $? -eq 1 ]

then

    echo "export GOPATH=\$HOME/.go/" >> ~/.bashrc

fi

grep "export GOBIN" ~/.bashrc

if [ $? -eq 1 ]

then

    echo "export GOBIN=\$HOME/.go/bin" >> ~/.bashrc

    echo "export PATH=\$PATH:\$GOBIN" >> ~/.bashrc

fi

  

BLUE "Installing sqlite..."

sudo apt install -y sqlite  

  

BLUE "Installing nikto..."

sudo apt install -y nikto

  

BLUE "Installing zbarimg..."

sudo apt install -y zbar-tools  

  

BLUE "Installing qrencode..."

sudo apt install -y qrencode

  

BLUE "Installing pdfcrack..."

sudo apt install -y pdfcrack

  

BLUE "Installing Virtualbox..."

sudo apt install -y virtualbox-qt

  

BLUE "Installing Vagrant..."

sudo apt install -y vagrant

  

BLUE "Installing Hopper..."

wget "https://d2ap6ypl1xbe4k.cloudfront.net/Hopper-v4-4.3.14-Linux.deb"

dpkg -i Hopper-v4-4.3.14-Linux.deb

rm Hopper-v4-4.3.14-Linux.deb

  
  

BLUE "Installing Oracle Java 8..."

echo "" | sudo add-apt-repository ppa:webupd8team/java

sudo apt update

sudo apt install -y oracle-java8-installer

  

BLUE "Downloading stegsolve.jar..."

wget "http://www.caesum.com/handbook/Stegsolve.jar" -O "stegsolve.jar"

chmod +x "stegsolve.jar"

  

BLUE "Installing fcrackzip..."

sudo apt install -y fcrackzip

  

BLUE "Installing unrar..."

sudo apt install -y unrar

  

BLUE "Installing steghide..."

sudo apt install -y steghide

  

BLUE "Installing ffmpeg..."

sudo apt install -y ffmpeg

  

BLUE "Installing Python library netifaces..."

sudo pip install netifaces

  

BLUE "Installing Python library iptools..."

sudo pip install iptools

  

BLUE "Installing Python library OpenSSL..."

sudo pip install pyopenssl

  
  

BLUE "Installing Python library pydispatch..."

sudo pip install pydispatch

  

BLUE "Installing GIMP..."

sudo apt install -y gimp

  

BLUE "Installing cmake..."

sudo apt install -y cmake

  

BLUE "Installing mplayer..."

sudo apt install -y mplayer

  
  

BLUE "Installing sshpass..."

sudo apt install -y sshpass

  

BLUE "Installing tcpflow..."

sudo apt install -y tcpflow

  

BLUE "Installing Python scapy..."

sudo pip install scapy



BLUE "Installing and setting default shell to zsh..."

sudo apt install zsh && chsh -s $(which zsh)  



BLUE "Installing the thing that 7z2john.pl needs..."

sudo apt install libcompress-raw-lzma-perl



BLUE "Installing Bloodhound..."

sudo apt install bloodhound



BLUE "Installing dos2unix..."

sudo apt install libcompress-raw-lzma-perl



BLUE "Installing Seclists..."

sudo apt install seclists



BLUE "Installing chisel..."

sudo apt install chisel



BLUE "Install sshuttle..."

sudo apt install sshuttle



BLUE "Adding enhanced matrix viewing application..."

sudo apt install cmatrix



BLUE "Generating TOOLS folder..."

# Check if the TOOLS directory exists
if [ ! -d "TOOLS" ]; then
    # Create the TOOLS directory if it doesn't exist
    mkdir TOOLS
fi

# Change to the TOOLS directory
cd ~/TOOLS
# cp /usr/share/windows-resources/mimikatz/Win32/mimikatz.exe mimikatz32.exe .
cp /usr/share/windows-resources/mimikatz/x64/mimikatz.exe mimikatz64.exe .
# Download tools using curl
curl -O https://github.com/jpillora/chisel/releases/download/v1.9.1/chisel_1.9.1_windows_amd64.gz
# curl -O <tool2_download_link>
# curl -O <tool3_download_link>
# curl -O <tool4_download_link>
# curl -O <tool5_download_link>
# curl -O <tool6_download_link>
cd ../



BLUE "Now for SCRIPTS..."

# Create the TOOLS directory if it doesn't exist
if [ ! -d "SCRIPTS" ]; then
    mkdir SCRIPTS
fi

cd ~/SCRIPTS

cp /usr/share/powershell-empire/empire/server/data/module_source/management/powercat.ps1 .

cp /usr/share/powershell-empire/empire/server/data/module_source/situational_awareness/network/powerview.ps1 .

cp /usr/lib/bloodhound/resources/app/Collectors/SharpHound.ps1 .
```



