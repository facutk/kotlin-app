# kotlin-app
kotlin starter app

## Local

### Dependencies install for Mac

```sh
# prepare brew
brew update

# jvm install
brew install --cask temurin

# add this to your .zshrc
# https://www.yippeecode.com/topics/upgrade-to-openjdk-temurin-using-homebrew/
export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)

# gradle install
brew install gradle

# https://skryvets.com/blog/2017/08/21/install-gradle-and-configure-gradle-home-on-a-mac/#configure-gradle_home
# add this to your .zshrc
export GRADLE_HOME=/usr/local/opt/gradle/libexec
export PATH=$GRADLE_HOME/bin:$PATH

# kotlin install
# https://kotlinlang.org/docs/command-line.html#homebrew
brew install kotlin

# start your own gradle app by running
# gradle init
```

### Run locally
```sh
gradle run
```

## Remote

### Dokku Install
```
# ssh into your dokku instance
ssh dokku@<server>

# update dependencies
sudo apt update
sudo apt upgrade

# add swapfile
sudo swapon --show
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
sudo cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# Dokku install
# Get latest from here https://dokku.com/docs/getting-started/installation/
wget https://raw.githubusercontent.com/dokku/dokku/v0.26.8/bootstrap.sh;
sudo DOKKU_TAG=v0.26.8 bash bootstrap.sh

dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
dokku apps:create 00-default # to show nicer default pages

# create dokku app
dokku apps:create kpop
dokku letsencrypt:auto-renew kpop
```

### Deployment
```sh
# git remote add dokku dokku@<server>:kpop
git push dokku
```

### Container Debug
```
docker ps
docker exec -it e628307fa2fa bash
```

#### Usefull Links
- https://code.visualstudio.com/docs/java/java-build
- https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-gradle
- https://medium.com/@agavatar/programming-with-kotlin-in-visual-studio-code-1d745d6b4ad1
- https://docs.gradle.org/current/samples/sample_building_java_applications.html