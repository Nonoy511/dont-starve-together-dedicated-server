# Description
This page describes how to stand up a Don't Starve Together server manually.

# Prerequisites
* Use Ubuntu 18.x or higher.
* Verify that these ports are open:
	* 8768, 8769
	* 10889
	* 11000, 11001
	* 27018, 27019

# Install and Launch Don't Starve Together server manually
1. Update/install necessary packages/dependencies.
```bash
sudo dpkg --add-architecture i386 && sudo apt -y update && sudo apt-get -y update && sudo apt-get -y upgrade && sudo apt-get -y install libstdc++6:i386 libgcc1:i386 libcurl4-gnutls-dev:i386 && sudo apt-get -y install unzip
```

2. Install steamcmd.
```bash
mkdir -p ~/steamcmd/

cd ~/steamcmd/

wget "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz"

tar -xvzf steamcmd_linux.tar.gz
```

3. Download and install DST server configurations.
```bash
cd ~
wget https://github.com/Nonoy511/dont-starve-together-dedicated-server/raw/master/MyDediServer-charmeleon.zip

mkdir -p ~/.klei/DoNotStarveTogether/

unzip MyDediServer-charmeleon.zip -d ~/.klei/DoNotStarveTogether/

wget https://accounts.klei.com/assets/gamesetup/linux/run_dedicated_servers.sh -P ~/
```

4. Download and install mods (AKA workshops AKA plugins).
```bash
wget -O dedicated_server_mods_setup.lua https://github.com/Nonoy511/dont-starve-together-dedicated-server/raw/master/dedicated_server_mods_setup.lua -P ~/dontstarvetogether_dedicated_server/mods/

wget https://github.com/Nonoy511/dont-starve-together-dedicated-server/raw/master/modoverrides.lua -P ~/
cp ~/modoverrides.lua ~/.klei/DoNotStarveTogether/MyDediServer/Caves
cp ~/modoverrides.lua ~/.klei/DoNotStarveTogether/MyDediServer/Master

wget https://github.com/Nonoy511/dont-starve-together-dedicated-server/raw/master/mods-aka-workshops.zip -P ~/
unzip ~/mods-aka-workshops.zip -d ~/dontstarvetogether_dedicated_server/mods
```

5. Launch the DST server.
```bash
chmod u+x ~/run_dedicated_servers.sh

~/run_dedicated_servers.sh
```
	
# Resources
* [DST guide to installing dedicated servers](https://forums.kleientertainment.com/forums/topic/64441-dedicated-server-quick-setup-guide-linux/)

* [How to install/configure mods](https://steamcommunity.com/sharedfiles/filedetails/?id=591543858)

# Remarks / Notes
* On windows, here are the DST directories:
	* C:\Program Files (x86)\Steam\steamapps\common\Don't Starve Together\mods
	* %USERPROFILE%\Documents\Klei\DoNotStarveTogether\94346078\Cluster_1\Master\modoverrides.lua
* DST is a single threaded game and we ran into CPU usage limits when hosting 7 people on an AWS t3.xlarge EC2 instance. Swithing to C5.large, which as a beefier CPU, seems to fix the problem.
* In the case where mods needs to be updated, these steps worked for me:
	1. Download the mods into my windows machine, and place the new files in mods-aka-workshops.zip
	2. On the DST server, execute te following (maybe purge the existing files/folders for good measure).
```bash
wget https://github.com/Nonoy511/dont-starve-together-dedicated-server/raw/master/mods-aka-workshops.zip -P ~/
unzip ~/mods-aka-workshops.zip -d ~/dontstarvetogether_dedicated_server/mods
```



