# How to get Test Analytics to run on AppScale

This tutorial is to be run in Linux.

The AppScale tools are not available under Windows but you may give it a try if you are under MacOS.

If you are under Windows, I recommend using VMWare to virtualize a Linux instance as it allows nested virtualization:
a VM inside a VM. That way, your Linux virtual machine will be able to run the Vagrant VM properly.
Obviously in that case you should allow quite a lot of memory to your VM, as the AppScale Vagrant VM alone requires 4GB of RAM.

Another option is to use Docker instead of Vagrant, which should be a more lightweight solution.
AppScale documentation: http://www.appscale.com/get-started/

## Build Test Analytics

### Install Maven and JDK, if necessary

```
sudo apt-get install default-jdk maven -y
```

### Add local gwt-dnd-3.1.1 JAR in Maven

```
mvn install:install-file -DgroupId=com.google.code.gwt-dnd -DartifactId=gwt-dnd -Dversion=3.1.1 -Dpackaging=jar -Dfile=gwt-dnd-3.1.1.jar
```

### Build Test Analytics

To be run from the `testanalytics_frontend` folder (where the `pom.xml` file is).

```
mvn clean install
```

## Setup Appscale VM with Vagrant

### Install Vagrant, if necessary

https://www.vagrantup.com/downloads.html

```
curl -o vagrant.deb https://releases.hashicorp.com/vagrant/1.8.1/vagrant_1.8.1_x86_64.deb
```

You'll need to update the previous command as newer versions of Vagrant become available.
Please check https://www.vagrantup.com/downloads.html to get the latest version of Vagrant.

Then install the `.deb` file you just downloaded:

```
sudo dpkg -i vagrant.deb
```

### Create the AppScale Vagrant VM

http://www.appscale.com/get-started/

```
curl -o Vagrantfile https://s3.amazonaws.com/appscale_CDN/files/Vagrantfile_template
```

Will get a `VagrantFile` in the current folder. All `vagrant` commands must be run from the folder with the `VagrantFile`.

```
vagrant up
```

### Extra: in case of problem, how to reset the VM

This is an easy and straightforward way to solve any key/secret/id issues with AppScale: just start over with a clean VM from scratch.

Again, all `vagrant` commands are to be run from the folder containing the `VagrantFile`.

```
vagrant destroy
vagrant up
```

## Alternative to Vagrant: setup Appscale Docker container

### Install Docker Engine, if necessary

For Ubuntu Linux: https://docs.docker.com/engine/installation/linux/ubuntulinux/

The following set of comands are for Ubuntu Trusty 14.04 (LTS).

```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates -y
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo rm /etc/apt/sources.list.d/docker.list
sudo sh -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list'
sudo apt-get update
sudo apt-get purge lxc-docker
apt-cache policy docker-engine
sudo apt-get update
sudo apt-get install linux-image-extra-$(uname -r) -y
sudo apt-get install apparmor -y
sudo apt-get update
sudo apt-get install docker-engine -y
sudo service docker start
sudo docker run hello-world
```

### Create the AppScale Docker container

http://www.appscale.com/get-started/

```
sudo docker pull appscale/appscale:latest
```

### Start the AppScale Docker container and configure SSH daemon

```
sudo docker run -i -t appscale/appscale:latest /bin/bash
```

This starts the Docker container and also logs you into it. The following commands are to be run in this Docker container session.

https://docs.docker.com/engine/examples/running_ssh_service/

```
apt-get update && apt-get install -y openssh-server
mkdir /var/run/sshd
echo 'root:docker' | chpasswd
sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
echo "export VISIBLE=now" >> /etc/profile
/usr/sbin/sshd -D
```

## How to get Test Analytics into the VM

NOT to be run in the VM or container. Run it in the host machine, near to the application code.

### Install AppScale Tools

https://github.com/AppScale/appscale-tools/wiki/Installing-the-AppScale-Tools-on-Linux

```
sudo apt-get install python-pip -y
sudo pip install appscale-tools
```

### Configure AppScale for the application

Go into the `testanalytics_frontend` folder (where the `pom.xml` file is) before proceeding with the rest of this tutorial.

```
appscale init cluster
```

This creates a `AppScaleFile` in the current folder.
All the other `appscale` commands must be run from the folder with the `AppScaleFile`.

You can configure how you want your application deployed in the `AppScaleFile`.
In particular you'll find the IP address of the AppScale VM that'll run your application.
However, the default configuration of the AppScale Vagrant VM matches the defaults in the `AppScaleFile`, so you don't need to change anything in this file.

On the other hand, if you are relying on the AppScale Docker container, you'll have to update the IP to match the Docker container, namely 172.17.0.2 by default.

### Get AppScale up and running

```
appscale up
```

You will be prompt for the root password in the AppScale VM/container. Default password for a Vagrant VM is `vagrant`. The code in this tutorial set the password the the Docker container as `docker`.

Afterwards this will ask you a few questions to create the initial account with administrator rights.

### Get Test Analytics running into AppScale

One more time, all `appscale` commands are to be run from the folder containing the `AppScaleFile`.

```
appscale deploy target/test-analytics-1.0-SNAPSHOT/
```

### Enjoy!

Take your favorite browser and go to: http://192.168.33.10:8080

You should see Test Analytics in action.
You can use the "Create Test Project" button to check quickly that everything is working fine.

You can also monitor AppScale at the following address: https://192.168.33.10:1443/status

## Appendix: how to run app locally, in dev mode

### Install GAE

```
mvn gae:unpack
```

### Run App in dev mode

```
mvn gae:run
```
