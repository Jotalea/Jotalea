# How to install Wine on Linux

to do: more descriptive tutorial

## For Debian (and Debian-based) distro

sudo dpkg --add-architecture i386

apt update

apt -y install gnupg2 software-properties-common

curl -fsSL https://dl.winehq.org/wine-builds/winehq.key | gpg --dearmor -o /etc/apt/trusted.gpg.d/winehq.gpg

apt-add-repository 'deb https://dl.winehq.org/wine-builds/debian/ $(lsb_release -cs) main'

apt update

apt install -y --install-recommends winehq-stable