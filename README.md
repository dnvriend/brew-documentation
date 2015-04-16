# brew-documentation
This is the documentation for use with OSX

* Brew Location: `/usr/local/Cellar`
* Cask location: `/opt/homebrew-cask/Caskroom`

## Bins
The launchers will be placed in `/usr/local/bin`, these point to where the application has been installed `/usr/local/Cellar/<appl>/<ver>/bin` or `/opt/homebrew-cask/Caskroom/<appl>/<ver>`  

## Homebrew:
* Install homebrew, please go to [http://brew.sh](http://bew.sh) and follow the instructions
* [Brew GitHub Page](https://github.com/Homebrew/homebrew/tree/master/share/doc/homebrew#readme)

## Homebrew-cask
* Install cask: please go to [http://caskroom.io](http://caskroom.io) and follow the instructions
* [Brew Cask Github Page](https://github.com/caskroom/homebrew-cask#learn-more)
* Install: `brew install caskroom/cask/brew-cask`
* All commands of homebrew-cask start with ‘brew cask'

## Homebrew-cask-versions
* For more info about the tap caskroom/versions please go to [https://github.com/caskroom/homebrew-versions](https://github.com/caskroom/homebrew-versions)
* Install: `brew tap caskroom/versions`

## Homebrew tab completion:
* Create a directory for all your bash tab completions, eg: `mkdir ~/.bash`, this is handy for future extensions
* Add the following line to `~/.bash_profile` 

```bash
source `brew --repository`/Library/Contributions/brew_bash_completion.sh
```

# My brew script

```bash
# Brew
brew update
brew upgrade
brew install scala
brew install sbt
brew install typesafe-activator
brew install maven
brew install boot2docker
brew install docker-compose
brew install mc

# Brew cask:
brew cask update
brew cask install iterm2
brew cask install gimp
brew cask install yed
brew cask install sublime-text3
brew cask install virtualbox
brew cask install vagrant
brew cask install intellij-idea
brew cask install pgadmin3
brew cask install java
brew cask install java6
brew cask install java7
```

Note: IntelliJ needs Java6:
https://github.com/caskroom/homebrew-cask/issues/4500

## Some commands

```bash
# upgrade all packages
brew update && brew upgrade
```

## docker-compose
docker-compose the release candidate has some nice features, when you wish to install that you will have to do that manually.

### Instructions for v1.2.0rc4
```bash
sudo mkdir -p /opt/docker-compose/1.2.0rc4
sudo chmod -R 777 /opt/docker-compose/1.2.0rc4/
curl -L https://github.com/docker/compose/releases/download/1.2.0rc4/docker-compose-`uname -s`-`uname -m` > /opt/docker-compose/1.2.0rc4/docker-compose
chmod +x /opt/docker-compose/1.2.0rc4/docker-compose
rm /usr/local/bin/docker-compose 
ln -s  /opt/docker-compose/1.2.0rc4/docker-compose /usr/local/bin/docker-compose
docker-compose —version
```

### Instructions forv1.2.0rc3:
```bash
sudo mkdir -p /opt/docker-compose/1.2.0rc3
sudo chmod -R 755 /opt/docker-compose/1.2.0rc3/
curl -L https://github.com/docker/compose/releases/download/1.2.0rc3/docker-compose-`uname -s`-`uname -m` > /opt/docker-compose/1.2.0rc3/docker-compose
chmod +x /opt/docker-compose/1.2.0rc3/docker-compose
rm /usr/local/bin/docker-compose 
ln -s  /opt/docker-compose/1.2.0rc3/docker-compose /usr/local/bin/docker-compose
docker-compose —version
```

## Boot2Docker
__Note:__ Boot2docker is deprecated

* Launching boot2docker: `ln -sfv /usr/local/opt/boot2docker/*.plist ~/Library/LaunchAgents`

## Handling multiple Java versions
OSX has the handy `java_home` command, so you could place the following three lines in your `~/.bash_profile` and 
comment the one out that you want to use. Then execute the `~/.bash_profile` script again with the command `source ~/.bash_profile`, you don't have to shut down your terminal session.

```bash
#export JAVA_HOME=`/usr/libexec/java_home -v 1.6`
#export JAVA_HOME=`/usr/libexec/java_home -v 1.7`
export JAVA_HOME=`/usr/libexec/java_home -v 1.8`
```

## Java directories
Brew cask will install Java to:

```
/opt/homebrew-cask/Caskroom/java6/1.6.0_65
/opt/homebrew-cask/Caskroom/java7/1.7.0_76
/opt/homebrew-cask/Caskroom/java/1.8.0_31
/opt/homebrew-cask/Caskroom/java/1.8.0_40
```

## Uninstall fig and boot2docker
```bash
brew unlink fig
brew install boot2docker
```

## Install postgres with brew
* [Source](http://www.moncefbelyamani.com/how-to-install-postgresql-on-a-mac-with-homebrew-and-lunchy/)

```bash
brew install postgresql
psql -h boot2docker -p 5432 -d security_bus -U security_bus -W security_bus
```
## Uninstall postgres from OSX
When you, like me, have run postgres natively on OSX and you want to get rid of it, because, of Docker, then you can do so using the uninstaller. Depending on the version(s) you have installed, the uninstaller is available in the following directory:

```bash
sudo /Library/PostgreSQL/9.1/uninstall-postgresql.app
open /Library/PostgreSQL/9.1/uninstall-postgresql.app
```

It will ask for the administrator password and run the uninstaller. I had multiple versions installed, the base dir was `/Library/PostgreSQL` but I had to replace the version `9.1` with `9.2` and uninstall that version also.

Because the database files will not be removed, you will have to do that yourself. These are available in the same directory as the database version, but because I uninstalled both versions, I just removed the whole base dir and got rid of all the junk: `sudo rm -rf /Library/PostgreSQL`

* There is also an ini file, to remove that: `sudo rm /etc/postgres-reg.ini`

* Remove the PostgreSQL user using System Preferences -> Users & Groups.

* Restore your shared memory settings: `sudo rm /etc/sysctl.conf`

# On Ubuntu
On Linux there is a great port of Homebrew called [Linuxbrew](https://github.com/Homebrew/linuxbrew). I use Ubuntu 14.10 Q6600/8G/256GSSD/9800GT, a quite old computer I may say.

```
sudo apt-get install build-essential curl git m4 ruby texinfo libbz2-dev libcurl4-openssl-dev libexpat-dev libncurses-dev zlib1g-dev
sudo apt-get install python-setuptools
```

## Virtualbox and extensions
Download and install the .deb from the Virtualbox site, and download and install the extension pack.

## docker
I installed docker, docker-machine and docker-compose with brew. Worked great.

# docker-machine
The first machine I created didn't work. docker-machine waited forever. I did the following

* Reboot the computer
* Resetted the computer, it waited on a VMWare network card (its a PC I get it),
* Removed the old machine: `docker-machine rm dev`
* Created a new machine: `docker-machine create dev`

After this it worked. 

## ~/.bashrc
To make the config look more like my Mac, I added a `~/.bash_profile` and added the following to it:

```bash
export PATH="$HOME/.linuxbrew/bin:$PATH"
export MANPATH="$HOME/.linuxbrew/share/man:$MANPATH"
export INFOPATH="$HOME/.linuxbrew/share/info:$INFOPATH"
export ACTIVATOR_HOME=~/Downloads/activator-1.3.2
export BREW_HOME=$HOME/.linuxbrew/bin
export PATH=$PATH:$HOME/.linuxbrew/opt/go/libexec/bin
export PATH=$PATH:$ACTIVATOR_HOME:$BREW_HOME

source $HOME/.linuxbrew/etc/bash_completion.d/docker
source $HOME/.linuxbrew/etc/bash_completion.d/docker-compose

cd projects
$(docker-machine env dev)
```
