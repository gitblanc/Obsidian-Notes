- We will use the vpn **protonvpn**:
````
wget https://protonvpn.com/download/protonvpn-stable-release_1.0.1-1_all.deb

dpkg -i protonvpn-stable-release_1.0.1-1_all.deb

apt-get update

apt-get install protonvpn-cli

protonvpn-cli login "username"

protonvpn-cli c #select a connection

protonvpn-cli s #check you have a new ip
````