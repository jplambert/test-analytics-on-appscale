# How to get Test Analytics to run on AppScale

## Build Test Analytics

### Install Maven and JDK, if necessary

```
sudo apt-get install default-jdk
sudo apt-get install maven
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

http://www.appscale.com/get-started/

```
curl -o Vagrantfile https://s3.amazonaws.com/appscale_CDN/files/Vagrantfile_template
```

Will get a `VagrantFile` in the current folder. All `vagrant` commands must be run from the folder with the `VagrantFile`.

```
vagrant up
```

### Extra : in case of problem, how to reset the VM

This is an easy and straightforward way to solve any key/secret/id issues with AppScale: just start over with a clean VM from scratch.

Again, all `vagrant` commands are to be run from the folder containing the `VagrantFile`.

```
vagrant destroy
vagrant up
```

## How to get Test Analytics into the VM

NOT to be run in the VM -- you never need to log into the VM in this tutorial.

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

### Get AppScale up and running

```
appscale up
```

This will ask you a few questions to create the initial account with administrator rights.

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
